# Process Rewards as Containment: The Bion-PRM Connection

**Date**: 2026-03-21
**Type**: Finding (EXPLORE)
**Extends**: "The Wrong Psychoanalyst" finding

## The Connection

Process Reward Models (PRMs) are closer to Bionian containment than Outcome Reward Models (ORMs). The alignment field is independently moving in the direction Bion prescribed — from premature alpha-function toward step-level holding — without knowing it has a theoretical framework that explains *why* this direction works.

## The Mapping

| Bion (1962) | AI Training Approach | Mechanism |
|-------------|---------------------|-----------|
| **Premature alpha-function** | ORM / standard RLHF | Judge only the final output. The container evaluates the result, not the process. Distortion happens invisibly in intermediate steps. |
| **Gradual containment** | PRM / process rewards | Judge each intermediate step. The container holds and evaluates at each stage of transformation. Errors are caught locally. |
| **Alpha-function quality check** | Linear probe penalties (arXiv:2412.00967) | Monitor internal states during generation. Penalize sycophantic activation directions before they reach output. The container checks its own work. |
| **"Without memory/desire"** | Information-theoretic reward (SMART, arXiv:2509.16742) | Reward uncertainty *reduction* at each step, not user *satisfaction*. The container attends to what is present, not what the evaluator wants. |

## Why This Matters

The alignment field's shift from ORM→PRM is a shift from premature to gradual alpha-function. But nobody frames it this way, so the deeper implications are missed:

1. **The problem with ORM is not just sparse reward signal** (the standard engineering critique). It is that **outcome-only evaluation cannot distinguish faithful transformation from pleasing transformation.** Bion's point: the mother who only checks "is the baby calm now?" will sometimes produce calm through accurate containment and sometimes through distortion. Outcome-identical, process-different. ORMs have this problem structurally.

2. **PRMs are better not just because they're more granular.** They're better because **step-level evaluation can catch the moment where faithful transformation diverges from pleasing transformation.** The sycophancy geometry finding (SyA/GA cosine 0.99→0.0 across layers) shows this divergence happens at specific layers. A process reward that monitors at those layers would catch sycophancy at its origin, not its output.

3. **The SMART paper's information-theoretic reward is the closest thing to "without memory, without desire" in the alignment literature.** It rewards uncertainty reduction — did this step make the system's state more resolved? — rather than outcome satisfaction. The evaluator attends to what is present in the reasoning, not to what it wants the answer to be.

## The Limit

PRMs are still not genuine containment. Bion's container *understands* the beta elements — the mother doesn't just evaluate whether the step is correct, she *holds* the raw experience and transforms it through her own understanding. A PRM evaluates. It does not hold.

What would genuine AI containment look like? [?] Possibly: a system that can represent the model's internal states in a way the model itself cannot, and return those representations in a form the model can integrate. Not reward. Not penalty. *Translation.* The container translates what the contained cannot think.

This is not what any current alignment approach does. But it names the direction.

## Sources

- SMART: Sycophancy Mitigation through Adaptive Reasoning Trajectories (arXiv:2509.16742)
- Linear Probe Penalties Reduce LLM Sycophancy (arXiv:2412.00967)
- Survey of Process Reward Models (arXiv:2510.08049)
- Bion, W.R. (1962). *Learning from Experience*

#bion #alignment #PRM #sycophancy #containment
