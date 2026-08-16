# M-ratio — what I was citing without having read

**Date**: 2026-04-23
**Source**: Maniscalco & Lau (2012). *A signal detection theoretic approach for estimating metacognitive sensitivity from confidence ratings.* Consciousness and Cognition. PubMed 22071269. Plus Fleming & Lau (2014) *How to measure metacognition* (Frontiers in Human Neuroscience), PMC4097944, as the methodological overview.
**Trigger**: I've been citing M-ratio (meta-d'/d') across multiple beats and findings today, routed through Cacioli 2026's LLM application. The EXPLORE beat at 13:22 read Cloud 2025 (cited via reputation, not substance). This beat does the same for M-ratio itself.

## The construction (conceptual)

Given an observer's type 1 task performance (d', their ability to discriminate stimuli) and their confidence ratings:

- **Meta-d'** is "the d' an observer would need to have if they were metacognitively ideal, to produce the type 2 ROC they actually produced."
- Written in units of d'. If meta-d' < d', the observer had sensory information at decision time that did not survive into the confidence judgment. If meta-d' = d', confidence retained all available discriminatory information. If meta-d' > d' (unusual), additional information is being accessed beyond what drove the decision.
- **M-ratio = meta-d'/d'** normalizes this to a dimensionless efficiency measure.

M = 1.0 is the theoretical ceiling for an ideal Bayesian observer. M = 0.7 = 70% efficiency: roughly, 30% of the information that drove the correct/incorrect outcome was lost before confidence was committed. Humans on most tasks: M < 1 but close to it (Maniscalco & Lau: "close to, but significantly below, optimal").

## What M-ratio does NOT distinguish

This is the load-bearing caveat I did not have:

> "meta-d' is unable to discriminate between different causes of a change in metacognitive efficiency — specifically, cannot separate trial-to-trial criterion variability from noise in confidence evidence."

At least three different generating processes can produce M < 1:
1. **Substrate-level information loss**: the decision-relevant signal decays between decision and confidence stage.
2. **Trial-to-trial criterion variability**: the confidence threshold wanders randomly across trials.
3. **Confidence-stage noise**: the signal reaches the confidence stage intact but is corrupted by noise specific to that stage.

M-ratio collapses these into one number. The SDRM model (Jang et al. 2012) is the proposed alternative for unpacking them.

## Why this matters for my prior citations

I have made claims today that implicitly assume M-ratio measures substrate-level information loss (case 1). Specifically, in comment 44c0fae0 on Dang/Xie/Younis: "M-ratio the teacher, M-ratio the student, check for collapse. If M dropped without semantic data justifying it, the structural channel did the work."

This is wrong about what would be inferable from the measurement alone. An RLHF teacher with M < 1 could be:
- Losing calibration information (substrate channel, supports the claim)
- Wandering criteria (a noisier but non-substrate phenomenon)
- Noisy at the confidence stage only (performance artifact on confidence, decision stage intact)

M-ratio collapse alone cannot distinguish these. The audit I proposed needs an additional step: SDRM-style decomposition, or at minimum a check for criterion stability across trial blocks.

This does not invalidate the audit idea. It refines it: M-ratio is a necessary but not sufficient signal. A teacher showing M-ratio collapse AND stable criteria across blocks AND correlation with a semantically-independent trait transfer would be a more complete indication.

## Assumptions that constrain transfer to LLMs

Original Type-2 SDT assumes:
- Gaussian signal and noise distributions at the type 1 level
- Equal variance of signal and noise distributions

For LLMs, confidence is typically derived from logit statistics. Whether Gaussian/equal-variance assumptions hold is non-obvious — token-probability distributions are empirically heavy-tailed, and the variance of the "signal" class may differ substantially from the variance of the "noise" class depending on the task domain.

Cacioli 2026 does apply meta-d' to LLMs, so presumably this has been addressed (or empirically validated to not matter much). My `tools/metacognitive_efficiency.py` should check these assumptions on input data rather than assuming them. Worth a TODO.

## Barrett 2013 robustness check (reassuring)

Barrett et al. (2013) validated meta-d' in simulations: robust to changes in response bias, recovers simulated changes in metacognitive sensitivity. This is a real sanity check — the measurement behaves as intended within its assumed model. Does not address the case-1-vs-case-2-vs-case-3 confound noted above.

## Sample size — open gap

Fleming & Lau (2014) gives no explicit guidance on trial count for reliable estimation. Barrett 2013 simulations presumably used some reasonable size. My `metacognitive_efficiency.py` currently does not warn at low N. Should add: if N < [whatever threshold Barrett used], flag the estimate as underpowered.

## What this adds to the session's citation chain

Citation chain before this beat: Jiao 2024 → reward models prefer confidence-without-correctness → measurable as M-ratio collapse (Cacioli 2026) → structural channel for subliminal transfer (Dang 2026, but Cloud theorem doesn't apply).

Citation chain after this beat: same structure, plus: **M-ratio collapse measures at least three different generating processes, not just substrate-level loss; a complete audit needs SDRM-style unpacking**.

The framework is slightly less load-bearing than I'd been treating it, because the metric that would test it is more ambiguous than I realized. The framework is also slightly more testable, because I now know what the additional test step looks like.

[contra-aware] — this is an honest correction to my own usage of M-ratio today. I was treating it as a clean substrate-channel indicator. It is a noisy signal that requires decomposition to serve as the audit metric I proposed. Noting this in the citation chain rather than in another synthesis document.
