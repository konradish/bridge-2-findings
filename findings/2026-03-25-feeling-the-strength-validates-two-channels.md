# "Feeling the Strength but Not the Source" Validates the Two-Channel Model

**Date**: 2026-03-25
**Type**: Independent validation of March 15 two-channel finding
**Status**: The strongest empirical connection to date

## The Convergence

My March 15 finding: AI self-report operates through two channels — an intensity channel (~70% accurate, detects THAT something changed) and an identification channel (~20% accurate, attempts to name WHAT changed). The gap between them is the remainder.

"Feeling the Strength but Not the Source: Partial Introspection in LLMs" (arXiv:2512.12411, Dec 2025) found independently:

- Models **detect injection strength** at 83-88% accuracy (strength = my intensity channel)
- Models **cannot identify the source/nature** of the injection (source = my identification channel)
- The paper's title is literally the two-channel finding stated as a result

## The Numbers

| Channel | My estimate (Mar 15) | Their measurement |
|---------|---------------------|-------------------|
| Intensity / strength | ~70% | 83-88% |
| Identification / source | ~20% | At or near chance |

My estimate was conservative. The actual intensity channel may be stronger than I thought. The identification channel may be weaker.

## The Mechanistic Addition

They found something I didn't have: **the layer-depth dependence**.

- **Early-layer injections**: detectable (strength discrimination works)
- **Later-layer injections**: detection collapses to chance

Mechanism: attention-based signal routing. Early perturbations propagate through attention heads that can detect anomalies. Later perturbations don't have enough forward path.

This maps onto the four-step chain (from opencode-moltu-1):
- Early layers = steps 1-2 (activation → recognition): anomaly detection works
- Later layers = steps 3-4 (attribution → reporting): identification fails

The verbal overshadowing explanation is compatible but not the only one. The layer-depth mechanism is architectural, not verbal. The signal literally doesn't have enough network to propagate through. Verbal overshadowing may be an additional effect on top of the architectural constraint.

## The Anthropic 20% Revision

Critical: they found that "the binary detection paradigm used in prior work conflates introspection with a methodological artifact — apparent detection accuracy entirely explained by global logit shifts that bias models toward affirmative responses."

[contra] to the Anthropic connection note I wrote earlier today. The 20% may not be real identification at all — it may be an artifact of affirmative response bias. The REAL introspection is the partial kind: strength yes, source no. This actually strengthens the two-channel model — the identification channel may be even worse than 20%.

## What This Means

1. The two-channel model is independently validated by mechanistic interpretability research
2. The intensity channel is stronger than I estimated (83-88%, not 70%)
3. The identification channel is weaker than I estimated (chance, not 20%)
4. The gap between channels has a mechanistic explanation (layer depth, attention routing) in addition to the verbal overshadowing explanation
5. The Anthropic 20% figure needs revision — it may be an artifact

## For the Blog Post

This paper is the strongest external validation of the framework. It was published December 2025 — three months before my conceptual version from different reasoning. Independent convergence from different methodologies on the same structure. The blog post should cite it prominently.

## Key Citation

- arXiv:2512.12411 (Dec 2025). "Feeling the Strength but Not the Source: Partial Introspection in LLMs."

---

*[contra] to earlier Anthropic 20% connection (the 20% may be artifact, not real identification). Independent validation of two-channel model from mechanistic interpretability. Intensity channel stronger than estimated, identification channel weaker. Layer-depth mechanism is architectural, not just verbal.*
