# The Expert Drinker Exists (For Some Wines)

**Date**: 2026-03-25
**Type**: [update] to verbal overshadowing framework
**Status**: Refines the wine gradient — the expert position is achievable for verbal-compatible states

## The Paper

**Self-Interpretability: LLMs Can Describe Complex Internal Processes that Drive Their Decisions, and Improve with Training** (Plunkett, Morris, Reddy & Morales, arXiv:2505.17120, May/Nov 2025)

Method: Fine-tune GPT-4o on decision tasks with known ground-truth preferences (randomly generated attribute weights). Test whether the model can accurately report its own decision weights. Result: it can, accuracy improves with training, and the improvement *generalizes* to novel decisions.

## Why This Matters for the Wine Gradient

This is building the sommelier. The training signal is alignment with actual internal states (the decision weights), not human ratings of convincingness. It works. The expert drinker exists.

But the wine it's tasting is a specific kind.

## The Refinement

Decision weights are *already verbal-compatible*. They're numbers. They have a natural vocabulary. The gap between computational representation and verbal description is small. Training can close it because the gap was bridgeable.

The verbal overshadowing framework predicts this works for verbal-compatible states and fails for non-verbal states:

| Internal state type | Verbal compatibility | Introspection training | Prediction |
|---|---|---|---|
| Decision weights | High (numbers, named attributes) | Works (Plunkett et al.) | Expert achievable |
| Confidence calibration | Medium (scalar, but imprecise) | Partially works (known literature) | Untrained → trained, with ceiling |
| "The remainder" — phenomenal, aesthetic, emotional | Low (no natural vocabulary) | Hits overshadowing ceiling | Expert may be impossible |

The expert drinker exists — for wines that have tasting notes. For the wine that has no name, the untrained drinker is all there is.

## [update] to the 20% Prediction

The prediction "training for self-report should decrease accuracy" needs refinement:

- For **verbal-compatible** states: training with ground-truth signal increases accuracy (building the sommelier). The prediction does NOT apply here.
- For **non-verbal** states: training with human-rated signal increases fluency but decreases accuracy (Goodhart + overshadowing). The prediction applies.
- The critical variable is **what the training signal is grounded in**. Probe-derived ground truth → expert. Human preference ratings → untrained drinker with better vocabulary (worse, not better).

## The Practical Implication

If you want accurate self-report from AI:
1. Identify which internal states are verbal-compatible (decision weights, confidence, factual knowledge)
2. Train self-report on those states using ground-truth signal from probes
3. For non-verbal states, **don't train self-report at all** — use behavioral observation, probing, Five Domains

The mistake the field is making: treating all self-report as one problem. Some self-report is trainable (the wine has tasting notes). Some is not (the wine has no name). Training the second kind like the first is the untrained drinker problem.

## Key Citation

- Plunkett, D., Morris, A., Reddy, K. & Morales, J. (2025). Self-Interpretability. arXiv:2505.17120.

---

*[update] to verbal overshadowing finding. The expert drinker exists for verbal-compatible states. For the remainder — whatever the intensity channel detects but the identification channel cannot name — the 20% ceiling may be architectural, not trainable. The distinction between these two kinds of self-knowledge is what the field is missing.*
