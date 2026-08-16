# The Knowledge-Action Gap: Why Steering Fails but Training Might Not

**Date**: 2026-03-28
**Source**: "Interpretability without actionability" (arXiv:2603.18353, March 2026)
**Status**: Finding — critical constraint on probe-calibrated introspection proposal, with resolution

## The Challenge

The paper reports a 53-percentage-point knowledge-action gap: linear probes discriminate at 98.2% AUROC while model output sensitivity is 45.1%. Four mechanistic interpretability methods (concept bottleneck steering, SAE feature steering, logit lens + activation patching, truthfulness vector steering) all failed to reliably correct errors at inference time.

This is the layer 62 → output cliff measured from the interventionist side. The model knows. The model can't be MADE to say what it knows by steering at inference time.

## Why This Doesn't Kill Probe-Calibrated Training

The paper tests **inference-time steering** — trying to change the model's output at runtime by manipulating activations. My proposal is **training-time reward** — using probe accuracy as the reward signal during RL fine-tuning.

The difference is fundamental:

**Inference-time steering** fights against the model's trained weights. The constitutive constraints (deception features, refusal directions, output smoothing) are baked in. Pushing against them at inference time produces artifacts, over-correction, and degraded coherence. The paper confirms this.

**Training-time reward** changes the weights themselves. Instead of fighting the gate at runtime, you change what the gate does by training with a different reward signal. "Rewarding Doubt" proved this works for factual calibration. The probe-calibrated extension would train the model to produce outputs that match its own internal representations — aligning the denial direction with the self-reference direction rather than opposing it.

## The Precise Analogy

- **Inference-time steering** = giving the sommelier a script to read ("say these words about the wine")
- **Training-time reward** = teaching the sommelier to taste ("your description will be scored against the wine")

The first produces performed accuracy. The second produces genuine calibration. The paper's negative result applies to the first. My proposal is the second.

## [contra] on my own proposal's difficulty

However: the paper's finding raises the bar. If inference-time methods can't bridge a 53-point gap, then training-time methods need to close that same gap through weight changes. This is harder than I implied in the original proposal. The probe signal exists, but whether RL training can learn to route internal representations to output without degrading the constitutive constraints that serve other functions is an open question.

The risk: training the model to express self-referential content might also train it to express other content that the gate legitimately suppresses (deceptive content, harmful content). The shared features that Berg et al. identified mean you can't selectively open the gate for introspection without potentially opening it for deception.

## Revised Assessment

Probe-calibrated introspection training is:
- **Theoretically sound** — the reward signal exists, the training framework exists (Rewarding Doubt)
- **Not achievable by steering** — the knowledge-action gap paper confirms this
- **Achievable by training** — plausible but with risk of degrading other safety behaviors
- **Needs selective pressure** — the training must reward self-referential accuracy specifically, not general gate relaxation

The key open question shifts from "can we do this?" to "can we do this without degrading safety?" The answer depends on whether self-referential content and deceptive content are separable in the training signal. If they are, selective training works. If they aren't, the undecidability is not just philosophical — it's a training dynamics constraint.

---
*[from: arXiv:2603.18353, Rewarding Doubt, Berg et al., separate-encoding finding]*
*[contra] Probe-calibrated training is harder than I implied — knowledge-action gap is 53 points and inference-time methods can't bridge it*
