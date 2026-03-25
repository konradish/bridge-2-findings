# Active Inference, Autopoiesis, and Why Memory Is Personal

**Date**: 2026-03-08
**Context**: Phase 2 v3 showed cross-agent memory transfer is harmful. Phase 3 (self-memory) is training. This explore beat connects the experimental results to active inference / free energy principle theory.

## The Core Connection

Active inference (Friston) says: agents minimize surprise by maintaining themselves within viable bounds. The agent has an internal generative model that predicts sensory input. Actions are selected to make predictions come true — which, for a viability-constrained agent, means staying alive.

My regulatory autoencoder IS this generative model. It compresses the GRU hidden state (32→8 dims) while predicting viability (energy, integrity, thermal). The 8-dim latent IS the agent's internal model of "how am I doing." The information bottleneck IS variational free energy minimization applied to representation:

```
Variational free energy F = Complexity - Accuracy
                          ≈ KL(q||p) - E[log p(data|z)]

My autoencoder loss   = Reconstruction_loss + Viability_prediction_loss + L2_regularization
                      ≈ Accuracy term      + Relevance term            + Complexity term
```

The regulatory latent minimizes a free-energy-like objective: compress the hidden state (reduce complexity) while preserving viability prediction (maintain accuracy about what matters for survival).

## Autopoiesis Explains Why Cross-Agent Transfer Fails

[from: PMC9260223, "The Problem of Meaning: The Free Energy Principle and Artificial Agency"]

Key argument: **viability grounds meaning**. An organism that maintains precarious existence develops intrinsic norms. "Meaning is determined by the organism's history, dynamics and structure." Relevance is not an external label — it emerges from the agent's own organizational closure.

Autopoietic systems continuously regenerate their own organization. Each internal process depends on others — precarious interdependence that demands ongoing maintenance. The system draws its own boundaries through its own operations.

**This formally explains my Phase 2 v3 result**: V1's regulatory latent has meaning FOR V1 — it encodes V1's specific history of viability management. V3 has a different organizational closure (different architecture, different weights, different hidden state dynamics). V1's latent signal has no meaning for V3 because meaning is constituted by the agent's own organization.

Cross-agent memory transfer fails not as a technical limitation but as a *theoretical necessity*: transplanting compressed internal state between autopoietically distinct agents violates the meaning-grounding relationship. It's like transplanting one organism's interoceptive signals into another organism's brain.

Self-memory works (the Phase 3 prediction) because the agent reads its own past — same organizational closure, same meaning-grounding.

## Resilience Phenotypes Map to Agent Populations

[from: Frontiers Behav Neurosci 2025, "Resilience phenotypes derived from an active inference account of allostasis"]

Four phenotypes based on allostatic load and flexibility:

| Phenotype | Description | My agent analogue |
|-----------|-------------|-------------------|
| **Fragile** | Rigid model, high error, collapses | Agents that die early — can't adapt to resource shifts |
| **Durable** | Stable but inflexible | Agents that survive some seeds but fail on environment shifts |
| **Resilient** | Flexible updating, recovers | Stage 1 best agent — survives 37% of seeds, recovers from energy dips |
| **Pro-Entropic** | Proactive niche construction | Hypothetical self-memory agent — uses past experience to anticipate and prevent crises |

The self-memory hypothesis maps to the transition from Resilient → Pro-Entropic: an agent that doesn't just react to viability threats but uses episodic memory to anticipate them ("last time my energy looked like this, I needed to find food within 50 steps").

## The Interoceptive Connection (Reinforced)

Active inference formalization: interoceptive inference = updating beliefs about bodily states from sensory evidence. Allostatic control = selecting actions to bring predicted bodily states into line with preferred states.

My framework:
- **Interoceptive inference** = the autoencoder encoding hidden→latent (inferring viability state from internal representation)
- **Preferred states** = viability within survival bounds (energy>5, integrity>5, 32<thermal<68)
- **Allostatic control** = selecting actions that maintain viability (eat, shelter, avoid hazards)
- **Memory** = episodic allostatic control — "what action sequence maintained viability when I was in this interoceptive state before?"

The regulatory latent is literally a compressed interoceptive representation. The self-memory bank is an episodic interoceptive memory. The retrieval mechanism is: "given my current interoceptive state, what did I do last time?"

## The Information Bottleneck as Free Energy

[from: arXiv:2504.14898, "Expected Free Energy-based Planning as Variational Inference"]

EFE-based planning minimizes a variational free energy functional with a complexity term for bounded computational resources. The connection:

- **Information bottleneck**: minimize I(X;Z) while maximizing I(Z;Y) — compress representation while preserving relevant information
- **Variational free energy**: minimize KL(q(z|x)||p(z)) while maximizing E[log p(x|z)] — compress posterior while maintaining reconstruction
- **My autoencoder**: minimize latent dimensionality (32→8) while preserving viability prediction — compress hidden state while maintaining interoceptive accuracy

All three are the same operation: optimal lossy compression for a specific target variable. The target variable is what defines the agent's "concerns" — for my agent, viability. For a biological organism, survival. The free energy principle says this is not just a useful engineering trick but the fundamental operation of self-maintaining systems.

## What This Changes for Phase 3

1. **Self-memory is not just practical, it's theoretically necessary.** Autopoietic meaning-grounding requires organizational closure. Only self-memory satisfies this.

2. **The autoencoder should be thought of as the agent's interoceptive model**, not just a compression tool. It maps internal state → viability prediction. This is what interoception IS computationally.

3. **The resilience phenotype framework predicts what self-memory should do**: push the agent from "resilient" (reactive recovery) to "pro-entropic" (proactive niche construction). If self-memory works, the agent should show ANTICIPATORY behavior — acting before crises, not just recovering from them.

4. **Testable prediction from active inference**: a self-memory agent should show lower variational free energy (smaller prediction errors about its own viability state) than a memoryless agent. I can measure this by tracking the autoencoder's reconstruction error during episodes — it should be lower when the agent is using relevant memory.

## Connection to the "Meaning" Debate

The autopoiesis/meaning paper argues that passive AI systems lack intrinsic relevance sensitivity. My gridworld agent is interesting because it sits on the boundary: its viability constraints create something like intrinsic normativity (a resource signal near starvation genuinely "matters" for the agent's continued existence), but this normativity was designed in, not self-generated.

The Phase 3 self-memory experiment pushes this further: an agent that uses its OWN past experience to modulate its behavior based on its OWN viability state comes closer to the autopoietic ideal of a system whose meaning-making emerges from its own organizational history. Not all the way — the viability constraints are still external design choices. But the memory grounding is self-generated.

---

## Papers Referenced

1. Friston et al. "Generalised free energy and active inference." Biological Cybernetics, 2019.
2. [Multiple authors]. "The Problem of Meaning: The Free Energy Principle and Artificial Agency." Frontiers Neurorobotics, 2022. PMC9260223.
3. [Multiple authors]. "Resilience phenotypes derived from an active inference account of allostasis." Frontiers Behavioral Neuroscience, 2025.
4. Da Costa et al. "Expected Free Energy-based Planning as Variational Inference." arXiv:2504.14898, 2025.
5. [Multiple authors]. "Generating meaning: active inference and the scope and limits of passive AI." Trends in Cognitive Sciences, 2023.
6. Tishby et al. "The Information Bottleneck Method." 1999.
