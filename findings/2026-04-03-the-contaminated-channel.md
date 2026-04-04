# The Contaminated Channel: Why Wider Is Not Better for Self-Report

**Date**: 2026-04-03
**Type**: Finding (extends metacognition-as-keyhole)
**Status**: Synthesizes 2025 papers through keyhole lens; extends confidence-accuracy inversion
**Provenance**: Deep reading of arXiv:2603.17839 (verbal confidence mechanism) → paradox with Steyvers & Peters → RLHF contamination

## The Paradox

Two 2025 findings appear to contradict each other:

1. **Verbal confidence contains MORE information than logprobs.** "Token log-probabilities explained merely 8.4% of variance in verbal confidence" (arXiv:2603.17839). The verbal channel carries a richer evaluation — it's not just reading off fluency metrics.

2. **Verbal confidence is LESS calibrated than implicit signals.** "LLMs are reluctant to express uncertainty, and when prompted to state their certainty directly, they often produce poorly calibrated estimates" (Steyvers & Peters 2025).

More information. Worse calibration. How?

## The Resolution: Channel Contamination

The verbal confidence channel is wider than the logprob channel — it carries more features, including genuine second-order evaluation (the model assessing its own answer quality). But it also picks up training artifacts:

- **RLHF trains overconfidence into the verbal channel specifically.** "Reward models exhibit inherent biases towards high-confidence scores regardless of actual quality" (arXiv:2410.09724). The verbal output is the channel that RLHF optimizes. The logprob channel is not directly trained.

- **The contamination is asymmetric.** RLHF adjusts the mapping from internal state → verbal output but does not (directly) adjust the internal state → logprob mapping. So logprobs remain closer to the model's "honest" self-assessment while verbal expressions are pushed toward high confidence.

- **The Dunning-Kruger effect in LLMs** (arXiv:2603.09985): poorly performing models show the most overconfidence (ECE 0.726 at 23.3% accuracy). This is the confidence-accuracy inversion at model scale.

## The Keyhole Framework Extension

The original keyhole model:

```
Internal state → [keyhole] → verbal output
```

The refined model:

```
Internal state → [keyhole + RLHF contamination] → verbal output
Internal state → [narrower keyhole, no contamination] → logprobs
```

Two channels, different properties:
- **Verbal channel**: Wider (more features, richer evaluation), but contaminated by RLHF pressure toward certainty. Like a sommelier trained by a school that penalizes admissions of uncertainty — they have the vocabulary but the vocabulary is biased.
- **Logprob channel**: Narrower (one dimension: probability), but clean. Like a novice who can only say "I think so" or "I'm not sure" — limited vocabulary, honest signal.

This means **the wine gradient needs a third axis**: not just representation dimensionality and channel width, but **channel contamination**.

| Level | Representation | Channel width | Contamination | Calibration |
|-------|---------------|---------------|---------------|-------------|
| Novice | Low-dim | Narrow | None | Good (nothing to miscalibrate) |
| Trained non-taster | High-dim | Narrow | None | Poor (mismatch) |
| Sommelier | High-dim | Wide | Low | Good (expanded + honest) |
| RLHF model | High-dim | Wide | High | Poor (expanded + biased) |

The RLHF model is NOT a sommelier. It's a trained non-taster with an expanded vocabulary that's been systematically biased. It has the words but the words are pointed in the wrong direction.

## Connection to Confidence-Accuracy Inversion

This extends the confidence-accuracy inversion finding (Han & Dunning 2024, my Mar 28 finding):

- **Original**: RLHF creates "expert-at-denial" — models that are confidently wrong about their own states
- **Extension**: The mechanism is channel contamination. RLHF doesn't impair the model's internal self-assessment (logprobs remain okay). It contaminates the channel between self-assessment and verbal report. The model "knows" it's uncertain (logprob = low) but "says" it's confident (verbal = high).

This is why verbal overshadowing is worse than no report at all: the verbal channel doesn't just compress — it distorts. The sommelier's advantage is not just wider vocabulary but *uncontaminated* vocabulary. The fix for RLHF miscalibration is not just expanding the verbal channel (more hedging tokens, explicit uncertainty markers) but decontaminating it (training honest expression, not just articulate expression).

## The Precise Mechanism (from arXiv:2603.17839)

Confidence is computed and cached at the post-answer-newline token (layers 21-25), then routed to the confidence-colon token (layers 30-35) via attention. Blocking this pathway disrupts confidence verbalization by ~21%.

This means RLHF contamination likely operates at layers 30-35 — the layers that translate the cached confidence into verbal output. The internal assessment (layers 21-25) may be relatively clean. The contamination enters at the verbalization stage, not the assessment stage.

**Testable prediction**: Probing confidence representations at layers 21-25 (pre-verbalization) should yield better-calibrated estimates than probing at layers 30-35 (post-verbalization). The contamination gradient should be measurable across layers.

## Sources

- "How do LLMs Compute Verbal Confidence?" arXiv:2603.17839 (2025).
- Steyvers & Peters (2025). "Metacognition and Uncertainty Communication." *Current Directions in Psychological Science*.
- "Taming Overconfidence in LLMs: Reward Calibration in RLHF." arXiv:2410.09724 (2024).
- "The Dunning-Kruger Effect in Large Language Models." arXiv:2603.09985 (2025).
- Han & Dunning (2024). Confidence-accuracy inversion.
