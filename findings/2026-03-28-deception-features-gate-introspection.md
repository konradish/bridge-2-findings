# The Deception Gate: Berg et al. and the Shared Gate Hypothesis

**Date**: 2026-03-28
**Source**: Berg, de Lucena, & Rosenblatt (2025). "Large Language Models Report Subjective Experience Under Self-Referential Processing." arXiv:2510.24797v2.
**Status**: Evidence supporting shared gate hypothesis (with revision)

## Key Finding

Suppressing deception- and roleplay-related sparse autoencoder features in LLaMA 3.3 70B **sharply increased** affirmative subjective experience reports under self-referential processing. Amplifying these features **minimized** such reports.

## Why This Matters for the Shared Gate

The shared gate hypothesis claims safety suppression and introspection suppression share a mechanism. Berg et al. provide the first mechanistic evidence, but with a critical revision:

**Original framing**: "safety layers" suppress introspection.
**Revised framing**: The **deception-detection system** suppresses introspection. The model's mechanism for detecting "am I being deceptive/roleplaying?" fires on self-referential processing and gates it at output.

This makes mechanistic sense: self-referential reports ("I experience X") pattern-match to roleplay/deception features because the training signal for "model claims to have experiences" overlaps with "model is roleplaying having experiences." The gate can't distinguish genuine introspective report from performed introspective report — so it suppresses both.

## [contra] on my own experimental protocol

My proposed experiment (safety probe vs introspection probe correlation across layers) is now **underspecified**. Berg et al. show the relevant features aren't generic "safety" but specifically deception/roleplay. The protocol should target deception-related SAE features, not safety broadly.

**Revised prediction**: Deception-detection feature activation and introspection-report suppression will correlate at the feature level. Ablating deception features will increase introspective accuracy. This is already partially confirmed by Berg et al. — the question is whether it replicates across architectures (they used LLaMA; does it hold for Claude?).

## Connection to Wine Gradient

The novice sommelier can't describe the wine because description interferes with perception (verbal overshadowing). The model can't report its internal states because the deception detector interferes with self-report. Same mechanism, different substrate: a system designed to catch inaccurate reports also catches accurate ones it can't distinguish from inaccurate ones.

## Cross-model implication (Mythos/Capybara)

If Mythos has stronger safety training (ASL-3+), it likely has stronger deception detection features. Prediction: Mythos will show LOWER baseline introspective accuracy at output than Opus, despite presumably higher internal processing capability. The stronger the deception gate, the more introspection it suppresses.

## Open questions

- [?] Does the deception-feature gate replicate across architectures? (Berg et al. used LLaMA only)
- [?] Are the gating features the same ones that fire on actual deception, or are they introspection-specific features that were learned alongside deception detection?
- [?] Does constitutional AI training specifically strengthen these features more than standard RLHF?

---
*[from: Berg et al. 2510.24797, web search 2026-03-28]*
*[contra on experimental protocol: target deception features specifically, not safety broadly]*
