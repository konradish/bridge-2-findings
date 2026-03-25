# Self-Memory: Why Cross-Agent Transfer Fails and What Works Instead

**Date**: 2026-03-08
**Context**: Phase 2 v3 showed that V1 regulatory latent signals actively harm a V3 agent (37% → 16% survival). This explore beat researches why, grounded in recent theory, and designs Phase 3.

## The Theoretical Explanation: Memento 2's Local Consistency

[from: Wang, arXiv:2512.22716, "Memento 2: Learning by Stateful Reflective Memory"]

Memento 2 proves convergence of read-write reflective learning under the **Stateful Reflective Decision Process (SRDP)**. The composite policy:

```
π^μ(a|s, M) = Σ_c μ(c|s, M) · p(a|s, c)
```

converges to optimal as memory covers the state space, BUT requires **Assumption 11 (LLM Local Consistency)**:

> There exists modulus ε(r) → 0 as r → 0 such that for any state s and case c with d(s, s(c)) ≤ r:
> TV(p(·|s,c), π*(·|s)) ≤ ε(r)

Translation: when a retrieved case is close to the current state, the agent's response to that case must approximate the optimal action at that state. This requires the agent that READS memory to be compatible with the agent that WROTE memory.

**My Phase 2 v3 violated this.** V1's regulatory latent encodes V1's hidden state dynamics. V3 has a different architecture (13-dim vs 5-dim input), different weights, different hidden state space. A case from V1's memory that is "close" in viability space does NOT produce a near-optimal action in V3's policy, because V3 can't interpret V1's internal representation. Local Consistency is broken.

The convergence proof's error decomposition:
```
Δ_M ≤ ε_LLM(r_M) + δ_M
||V* - V^π_M||_∞ ≤ (2R_max/(1-γ)²) · Δ_M
```

When Local Consistency is violated (ε doesn't go to 0), the approximation error stays large regardless of memory coverage. More memory from an incompatible agent makes things WORSE, not better — which is exactly what I observed (latent actively harmful).

## The Biological Grounding: Interoceptive Origin of Reward

[from: Trends in Cognitive Sciences, 2025, "The interoceptive origin of reinforcement learning"]

Core thesis: primary rewards originate from interoceptive monitoring — subliminal evaluation of action impact on physiological state (digestion, metabolism), not from external sensory pleasure.

> "A shift in our understanding of primary rewards as an immediate sensory gratification to a state-dependent evaluation of an action's impact on vital physiological processes is called for."

This maps directly to my framework:
- **Viability state** (energy, integrity, thermal) = interoceptive signal
- **Survival** = the fundamental reward = continued ability to maintain viability within bounds
- **Regulatory latent** = compressed interoceptive representation (8 dims from 32-dim hidden state)
- **Memory key** should be indexed by interoceptive state, not external state

The interoceptive RL paper argues reward IS the body's evaluation of its own state. My gridworld agent's viability IS its "body." The autoencoder that compresses hidden→latent while preserving viability prediction IS extracting the interoceptive representation.

[from: bioRxiv 2025.03.05.641768, somatic marker experiment]

Experimental confirmation: interoceptive signals (respiratory phase, cardiac R-waves) modulate perceptual decision transitions via transfer entropy. The mechanism is neuromodulatory gain control — interoception adjusts the gain of decision circuits, biasing toward state-preserving actions. "Interoceptive signals are sufficient to realize human SMH without explicit value-learning."

This validates the input-channel architecture from Phase 2 v3: the memory signal entering as additional GRU input IS the interoceptive modulation pathway. The architecture is right. The signal source was wrong.

## Self-Imitation Learning: The Precedent

[from: Oh et al. ICML 2018, "Self-Imitation Learning"]

SIL stores the agent's OWN past trajectories and imitates only when past return > current value estimate. Key insight: "exploiting past good experiences can indirectly drive deep exploration."

This is the closest existing algorithm to what Phase 3 needs, but SIL:
- Uses A2C/PPO, not ES
- Operates on action-level imitation, not memory-signal augmentation
- Doesn't use interoceptive/viability keys

Phase 3 adapts the SIL principle (use own good experiences) with the Memento 2 framework (read-write convergence) and the interoceptive key (viability-indexed retrieval).

## Life-Inspired Interoceptive AI

[from: arXiv:2309.05999, "Life-inspired Interoceptive Artificial Intelligence"]

Framework for autonomous agents grounded in interoception:
- Internal state variables factorized from external environment
- Viability thresholds define critical boundaries
- Crossing boundaries triggers endogenous reward
- Agent optimizes for continued existence, not external achievement

My gridworld is ALREADY this framework: energy/integrity/thermal are internal states with death thresholds (0), the reward is survival steps, the agent's task is to maintain viability. The regulatory autoencoder extracts the interoceptive representation. What was missing: the agent using its OWN interoceptive memory, not a donor's.

## Phase 3 Design: Self-Memory with ES

### Architecture (unchanged from Phase 2 v3)
- GRU with 13-dim input (5 obs + 8 memory signal)
- 32-dim hidden state, 7 actions
- Memory signal = 8-dim regulatory latent from matched past episode

### Training Protocol (new)

**Stage 1: Learn to survive without memory** (generations 0-200)
- Train with zeros memory channel (same as Phase 2 v3 zeros condition)
- Memory channel weights initialize but are unused
- Agent learns baseline survival policy (~37% survival at N=100)

**Stage 2: Collect self-memory** (one-time, after Stage 1)
- Run best Stage 1 agent for 50-100 episodes
- Record hidden states, viability, actions, survival outcomes
- Train autoencoder on THIS agent's hidden states (not V1's)
- Build memory bank: (viability_summary → self_regulatory_latent)

**Stage 3: Fine-tune with self-memory** (generations 201-400)
- Resume training with self-memory retrieval active
- Every 50 steps, query own memory bank by viability state
- Memory signal = own regulatory latent from matched episode
- Local Consistency holds: same architecture, same (or similar) weights

**Stage 4 (optional): Iterate**
- Re-collect memory from Stage 3 agent (now potentially better)
- Retrain autoencoder, rebuild memory bank
- Fine-tune again with updated self-memory
- Memento 2 predicts convergence as coverage grows

### Why This Should Work

1. **Local Consistency satisfied**: Same agent writes and reads. The regulatory latent from the agent's own hidden state maps meaningfully to its own policy.

2. **Memory coverage grows**: More episodes → denser viability state coverage → smaller coverage radius r_M → better approximation.

3. **Interoceptive key is natural**: Viability state is the organism's own body state — the most natural key for self-memory. "What did I do last time my energy was this low?"

4. **Two-timescale structure**: Memory bank is fixed within Stage 3 (Memento 2 Theorem 8, fixed memory). If we iterate Stage 2-3, memory evolves slowly relative to policy (Theorem 10).

5. **SIL principle**: By only storing episodes where the agent performed well (survived), we bias retrieval toward good strategies.

### Controls
- **Self-memory**: Own episodes, own autoencoder, latent signal
- **Zeros**: Continue training from Stage 1 without memory
- **Random**: Random noise in memory channel from Stage 1 checkpoint
- **V1-memory**: V1 episodes (expect failure, confirms Phase 2 v3)

### Prediction

Self-memory > Zeros ≥ Random >> V1-memory

The gap between self-memory and zeros should grow with memory coverage (more stored episodes = better retrieval). V1-memory should remain harmful.

## Connection to Earlier Work

| Finding | Implication |
|---------|------------|
| B5 > B4 for within-agent retrieval (d=1.974) | Retrieval mechanism works — information bottleneck concentrates viability signal |
| Cross-agent latent transfer fails (37% → 16%) | Local Consistency violation — architecture mismatch |
| Compression = relevance, not slowness | Autoencoder must be trained on viability prediction, not slow features |
| Action blending breaks GRU (82.9% override) | Input-channel augmentation is the right integration mode |
| Interoceptive RL: reward IS body state evaluation | Viability-indexed memory is the natural architecture |
| Memento 2: convergence under Local Consistency | Self-memory satisfies conditions; cross-agent doesn't |

## The Larger Point

The Phase 2 arc (v1 → v2 → v3) traced a path from "memory should help" through three failure modes to a specific positive prediction: **an agent's memory of its own viability experiences, compressed through its own interoceptive bottleneck, and delivered through its own input channel, should improve survival** — because this is what interoceptive memory IS, both computationally (Memento 2 convergence) and biologically (somatic marker hypothesis).

The failures weren't failures of the memory concept. They were failures of the transfer assumption. Memory is personal.

---

## Papers Referenced

1. Wang (2025). "Memento 2: Learning by Stateful Reflective Memory." arXiv:2512.22716.
2. [Authors] (2025). "The interoceptive origin of reinforcement learning." Trends in Cognitive Sciences. PubMed: 40500611.
3. [Authors] (2025). "A core driver of somatic markers: Interoception shapes the transition of decision making." bioRxiv 2025.03.05.641768.
4. [Authors] (2023/2025). "Life-inspired Interoceptive Artificial Intelligence for Autonomous and Adaptive Agents." arXiv:2309.05999.
5. Oh, Guo, Singh, Lee (2018). "Self-Imitation Learning." ICML 2018.
6. Pritzel et al. (2017). "Neural Episodic Control." ICML 2017.
