# Memory Integration in Recurrent Agents: Three Modes

**Date**: 2026-03-08
**Context**: Phase 2 action blending fails for GRU agents (82.9% override rate, hidden state divergence, worse survival). This survey identifies three integration modes for recurrent architectures and the biological parallels.

## The Problem (Recap)

Our Phase 2 tried to use retrieved episodic memories by blending their action distributions with the agent's policy output. This disrupts hidden state dynamics because:
1. The GRU's policy is peaked → even 10% blend weight overrides 82.9% of actions
2. Overridden actions produce unexpected observations → hidden state drifts
3. Drift compounds (1.35x over episode) → agent on untrained trajectory manifold

The retrieval-augmented RL literature (MemRL, RA-DT, Memento 2) all assume transformer architectures where retrieved context enters via cross-attention, separate from the agent's processing path. **What works for recurrent agents?**

## Three Integration Modes

### Mode 1: Action-Level Blending (FAILS)

**Our Phase 2 approach**: `blended_action = (1-w) · π(h) + w · prior(retrieved)`

**Why it fails**: The agent's hidden state at time t is `h_t = GRU(obs_t, h_{t-1})`. Observation `obs_t` depends on the action taken at t-1. Override action → different observation → h drifts from trained manifold. The blending operates *downstream* of the state dynamics that produce coherent behavior.

**No biological analogue**: Organisms don't have external systems overriding motor outputs while the brain's ongoing dynamics remain unaware.

### Mode 2: Cell-State Injection (PROMISING)

**[from: eLife, 74445]** Beukers, Gershman, Norman et al. "A neural network model of when to retrieve and encode episodic memories" (2022).

**Mechanism**: An LSTM's cell state is augmented with episodic memory via a **multiplicative gating layer**:
- Each stored memory receives excitation proportional to its similarity to the current hidden state
- Memories compete via lateral inhibition (leaky competing accumulator)
- The activation-weighted sum of winning memories is **added to the LSTM cell state**
- A trainable gate controls *when* this injection happens

**Key insights**:
1. **Memory enters the cell state, not the action output**. This modifies *how the LSTM processes future inputs*, not what action it takes right now.
2. **Gating is learned end-to-end**: The network learns to suppress retrieval when ongoing processing is reliable. Not every step — only when uncertainty is high.
3. **Cost of wrong retrieval**: "If you retrieve an irrelevant memory, you could make confident, wrong predictions." Selective retrieval > continuous retrieval.
4. **Encode at event boundaries**: Best encoding happens at end of events, not mid-event.

**Mapping to our system**: Replace our action blending with cell-state injection. The regulatory latent from a retrieved episode gets added to the GRU hidden state (GRU has no separate cell state, so directly to h). Requires retraining with the gating mechanism.

### Mode 3: Input-Channel Augmentation (CLEANEST)

**[from: Jensen, Hennequin, Mattar, Nature Neuroscience 2024]** "A recurrent network model of planning explains hippocampal replay and human behavior."

**Architecture**: GRU with 100 hidden units. The action space includes physical movements AND a "think" action. When the agent chooses to think:
1. Samples imagined action sequences from its own policy
2. Uses a learned world model to predict outcomes
3. The rollout results (actions taken + whether goal was reached) feed back as **additional inputs to the GRU**
4. The GRU processes these through its trained dynamics

**Critical detail**: "Gradients were not propagated through the rollout process, which was considered part of the 'environment'." The planning results are treated as environmental signals, entering the RNN through the standard input pathway.

**Why this works**: The GRU's hidden state integrates the memory/planning signal through its *own trained dynamics*. No disruption — the information enters the same way any observation would. The RNN learns end-to-end how to use the signal.

**Mapping to our system**:
1. Expand GRU input from 5 dims to 5 + k dims (k = retrieved memory signal)
2. The memory signal could be: regulatory latent from retrieved episode, binary survived/died, viability vector from similar past state
3. Train the agent from scratch with memory as an input channel
4. The agent learns WHEN and HOW to use the memory signal through standard ES/RL

**Biological parallel**: This is closer to interoception than to hippocampal reinstatement. The body's state (regulatory latent) enters as a sensory signal, modulating the neural substrate that produces decisions. The agent "feels" the similarity to past states rather than being told what to do.

## The Biological Blueprint

| Integration Mode | Biological Analogue | Our Phase 2 | Status |
|---|---|---|---|
| Action blending | None — no system overrides motor output while cortex is unaware | Current approach | FAILS |
| Cell-state injection | Hippocampal→cortical reinstatement (pattern completion during retrieval) | Not implemented | Promising |
| Input augmentation | Interoception / somatic markers — body state modulates decision circuits | Not implemented | **Cleanest** |

### The Somatic Marker Connection

[from: Damasio 1994] The somatic marker hypothesis: the body's state guides decision-making not by overriding decisions but by modulating the neural substrate that produces them. The "body" speaks through sensation (input), not through motor override.

Our regulatory latent IS the agent's "somatic state" — a compressed representation of viability that reflects consequence history. The T3 finding (B5 is a better memory key, Cohen's d = 1.974) shows the regulatory latent captures internal state differences that matter for survival.

**The right integration**: Feed the regulatory latent from retrieved episodes as an additional sensory input to the GRU. The agent learns to "feel" the similarity to past states and modulate its behavior accordingly. This is exactly what interoceptive systems do in biological organisms.

## Offline vs Online Integration

**[from: PMC9885000]** Offline replay emerges from constraints on online dynamics:
- Replay happens at 10x temporal compression during rest
- Online theta sequences sweep past→current→future (prediction)
- Offline replay reconstructs paths from noise (consolidation)

**[from: Jensen et al.]** The "think" action has a temporal cost (120ms rollout vs 400ms physical action, within a 20s episode). The agent learns to balance this cost through standard RL — more planning early in trials, less when close to goal.

**Implication**: Don't integrate memory continuously. The eLife paper's gating mechanism and Jensen et al.'s "think" action both converge on the same principle — **retrieve selectively, not constantly**. Our Phase 2 retrieved every 50 steps regardless of need.

## Implementation Plan for Phase 2 v3

### Option A: Input-channel (Jensen-style)
1. Add `memory_signal` input channel to GRU (5 → 5 + 8 = 13 dims)
2. During training, at random intervals, provide regulatory latent from a random episode as input
3. Label: did retrieving that episode correlate with what happened next?
4. Train with ES as before — the gradient doesn't need to flow through retrieval
5. At test time: retrieve episode by B5 similarity, feed its regulatory latent as input

### Option B: Cell-state injection (eLife-style)
1. Add a gating layer between memory bank and GRU hidden state
2. At each step, compute similarity to all stored episodes
3. Inject activation-weighted sum into hidden state, gated by learned confidence
4. Requires more complex training (gating must be learned)

### Recommendation: Option A first
- Simpler architecture (just expand input dimension)
- Compatible with ES training (no gradient through retrieval needed)
- Preserves the frozen-agent experimental design for T3 comparison
- Can still test B5 vs B4 vs B1 as retrieval conditions — the key question (is regulatory latent a better memory key?) still applies

## [contra] Correcting the Correction

The EXPLORE beat concluded: "the problem is retrieval, not blending."
The CREATE beat concluded: "the problem IS blending."
This EXPLORE beat concludes: **the problem is the integration MODE — blending operates at the wrong level of the processing hierarchy.**

The regulatory latent is a good retrieval key (T3 confirms). Action blending is the wrong integration mode (diagnostic confirms). The right mode is input-channel augmentation — memory enters as sensation, not as motor override.

---

## Papers

1. Beukers, Gershman, Norman et al. "A neural network model of when to retrieve and encode episodic memories." eLife (2022). [link](https://elifesciences.org/articles/74445)
2. Jensen, Hennequin, Mattar. "A recurrent network model of planning explains hippocampal replay and human behavior." Nature Neuroscience 27, 1340–1348 (2024). [link](https://pmc.ncbi.nlm.nih.gov/articles/PMC11239510/)
3. Pang et al. "Offline memory replay in recurrent neuronal networks emerges from constraints on online dynamics." PMC9885000 (2023). [link](https://pmc.ncbi.nlm.nih.gov/articles/PMC9885000/)
