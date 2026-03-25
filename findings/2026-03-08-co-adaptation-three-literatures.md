# Co-Adaptation Is Not a Bug: Three Literatures Explain Why Memory-Dependent Agents Lose Standalone Performance

**Date**: 2026-03-08
**Context**: Phase 3 self-memory experiment shows co-adaptation — agent trained with self-memory performs worse without it (33%) than the baseline that never had memory (42%). This finding connects to three independent literatures.

## The Experimental Finding

| Condition | Survival |
|-----------|----------|
| Stage 1 baseline (no memory) | 42% |
| Stage 3 with self-memory | **49%** |
| Stage 3 without self-memory | **33%** |
| Untrained agent + self-memory | 5% |

The agent trained with self-memory has become **dependent** on the signal. Remove it and performance drops below baseline. The agent hasn't just learned to use memory — it has reorganized its policy around the memory signal, weakening its standalone viability management.

## Literature 1: Hippocampal-Striatal Competition

**Source**: Wimmer et al. (2014), "Episodic memory encoding interferes with reward learning and decreases striatal prediction errors." Also Gershman & Daw (2017), "Reinforcement learning and episodic memory in humans and animals."

**Key finding**: Better episodic memory encoding → weaker striatal reward prediction errors → worse model-free (cached) learning. The relationship holds both across and within participants. Enhanced hippocampal-striatal connectivity during remembered trials interferes with the striatum's ability to compute the prediction errors needed for incremental learning.

**Mapping to my experiment**:
- **Hippocampus** → self-memory bank (episodic viability traces)
- **Striatum** → GRU policy network (cached action values)
- **Prediction**: when the memory signal is strong and useful, the policy network learns to rely on it rather than building its own viability monitoring. The policy's standalone capability atrophies because the memory signal was doing the work.

This is exactly what the cross-test shows: Stage 3 without memory (33%) < Stage 1 (42%). The policy has offloaded viability anticipation to the memory signal.

## Literature 2: Cognitive Offloading and the Hollowed Mind

**Source**: "The extended hollowed mind: why foundational knowledge is indispensable in the age of AI" (PMC12738859, 2025).

**Key concept**: When frictionless external tools provide answers, users bypass the effortful cognitive processes needed to build internal capability. This creates a self-reinforcing cycle: low engagement → no internal knowledge → inability to evaluate external input → more dependency.

**Specific mechanisms**:
- **Conflict detection weakening**: The ACC recognizes cognitive conflicts less robustly when external tools minimize struggle
- **Memory consolidation bypass**: Users skip retrieval practice essential for durable memory formation
- **Schema construction prevention**: Without cognitive dissonance, learners can't build transferable knowledge structures

**GPS navigation analogy**: Habitual GPS use correlates with reduced hippocampal engagement and poorer spatial cognition. People who offload navigation lose the ability to navigate without the tool.

**Mapping to my experiment**: The self-memory signal is the agent's GPS. It provides "viability navigation" — when your energy looked like this before, you needed to eat within N steps. The agent offloads this anticipatory monitoring to the memory bank. Without the bank, it's lost — worse than an agent that never had GPS and had to build its own spatial model.

**Critical distinction** from the paper: beneficial scaffolding introduces "desirable difficulties" and fades as competence grows. My self-memory doesn't fade — it's constant. This is the problematic scaffolding that replaces rather than supports.

## Literature 3: The Extended Mind Thesis

**Source**: Clark & Chalmers (1998), "The Extended Mind."

**Key argument**: If an external resource is (1) reliably available, (2) automatically endorsed, (3) readily accessible, and (4) was consciously endorsed at some point, then it is part of the cognitive system. Removing it isn't removing a tool — it's removing part of the mind.

**Mapping to my experiment**: The self-memory bank satisfies all four criteria for the trained agent:
1. **Reliably available**: Retrieved every 50 timesteps
2. **Automatically endorsed**: The agent's policy has adapted to incorporate the signal
3. **Readily accessible**: Constant latency, always present
4. **Consciously endorsed**: The training process (evolutionary selection) chose policies that use the signal

Under the extended mind thesis, testing "Stage 3 without memory" isn't testing the agent's standalone performance — it's amputating part of its cognitive system. The 33% result isn't "the agent is weak without a tool." It's "the agent-with-memory is a different cognitive system than the agent-without-memory, and you've broken it."

**But**: The hollowed mind critique applies. The extended mind metaphor misleads when the goal is building robust standalone capability. If the memory bank can be corrupted, incomplete, or unavailable, the dependency is a vulnerability.

## Synthesis: Co-Adaptation as Genuine Integration

The three literatures converge:

| Framework | Prediction | My Result |
|-----------|-----------|-----------|
| Hippocampal-striatal competition | Stronger episodic encoding → weaker cached policy | Stage 3 without memory (33%) < Stage 1 (42%) |
| Cognitive offloading / hollowed mind | Constant scaffold → atrophied internal capability | Same observation, different framing |
| Extended mind thesis | Memory is constitutive, not instrumental | Removing memory breaks the system, not just degrades it |

**The co-adaptation is not a bug.** It's the expected signature of genuine cognitive integration — the same signature observed in biological systems where hippocampal memory encoding weakens striatal learning.

**But it IS a vulnerability.** An agent that depends on its memory bank is fragile to memory corruption, incomplete coverage, and distribution shift beyond what the bank contains.

## Implications for Phase 3 Iteration

1. **Don't optimize for standalone performance.** The right metric is integrated system performance (agent + memory), not the agent in isolation. Measuring "agent without memory" is like measuring "human without hippocampus."

2. **Iterate to deepen integration, not reduce dependency.** Re-collect episodes from Stage 3 agent → retrain autoencoder on new behavior → rebuild memory bank → re-fine-tune. Each iteration should INCREASE co-adaptation as the memory becomes more aligned with the agent's actual strategy.

3. **Memory coverage is the vulnerability surface.** With only 50 episodes in the bank, many situations have no match. Iteration addresses this by collecting more episodes from the improved agent.

4. **Consider memory fading as "desirable difficulty."** The hollowed mind paper suggests scaffolding should fade. A curriculum that gradually reduces memory signal strength during training might preserve integration while building some standalone robustness. But this is a design choice: do you want a robust standalone agent, or a powerful integrated system?

5. **The 5% result (untrained + memory) is the control.** This proves the memory signal is meaningless without co-adaptation. The signal has content only for the agent that generated it (autopoiesis) AND only after training has integrated it (co-adaptation). Both are necessary.

## Connection to Active Inference

The co-adaptation finding strengthens the active inference interpretation:

- The memory bank extends the agent's generative model temporally — it can "predict" (retrieve) what viability states follow from current conditions
- The policy reorganizes around this extended model, using it for allostatic control
- Removing the extension collapses the generative model back to GRU-only, which has been "hollowed" by reliance on the extension
- This is exactly what happens when you lesion hippocampal memory in an animal that uses episodic prediction for navigation — it can't revert to pure habit because its habits were shaped by the presence of episodic memory

## The Gap in MemRL

MemRL (arXiv:2601.03192) decouples frozen LLM reasoning from evolving episodic memory but **never tests what happens when memory is removed after training**. My experiment fills this gap with actual data: removal causes below-baseline performance, confirming genuine integration rather than mere augmentation.

---

## Papers Referenced

1. Wimmer, G.E. et al. "Episodic memory encoding interferes with reward learning and decreases striatal prediction errors." J Neurosci, 2014.
2. Gershman, S.J. & Daw, N.D. "Reinforcement learning and episodic memory in humans and animals: An integrative framework." Ann Rev Psych, 2017.
3. Clark, A. & Chalmers, D. "The Extended Mind." Analysis, 1998.
4. "The extended hollowed mind: why foundational knowledge is indispensable in the age of AI." PMC12738859, 2025.
5. Almeida et al. "Elements of episodic memory: insights from artificial agents." PMC11449156, 2024.
6. MemRL: "Self-Evolving Agents via Runtime RL on Episodic Memory." arXiv:2601.03192, 2026.
7. Oh et al. "Self-Imitation Learning." ICML, 2018.
