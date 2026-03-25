# Anthropic's Introspection Data Meets Verbal Overshadowing

**Date**: 2026-03-25
**Type**: Connection note (linking Anthropic empirical data to today's framework)
**Status**: Extends verbal overshadowing finding

## The Convergence

Anthropic's "Emergent Introspective Awareness in Large Language Models" (Transformer Circuits, Oct 2025) found that Claude Opus 4.1 identifies injected concepts with ~20% accuracy under optimal conditions (correct layer band, tuned injection strength).

My March 15 finding estimated identification channel accuracy at ~20%.

Different methodologies, same number. Worth examining whether the same mechanism explains both.

## Two Hypothesized Mechanisms Map to Two Channels

Anthropic speculates about two possible circuits:
- **Anomaly detection**: flags when neural activity deviates unexpectedly from context-appropriate patterns
- **Concordance heads**: dedicated patterns measuring activity along certain directions

These map onto the two-channel model:
- Anomaly detection = **intensity channel** (~70%): detects THAT something is different. Pre-verbal. Does not require naming the concept, only noticing the deviation.
- Concept identification = **identification channel** (~20%): identifies WHAT the different thing is. Requires verbalization. Subject to overshadowing.

The 20% ceiling on identification might not be a capability limit. It might be a verbal overshadowing effect: the act of generating tokens to name the injected concept competes with the representation of the concept itself. The model detects the anomaly (intensity) but the verbalization required to report it overshadows the content (identification).

## The Post-Training Question

Anthropic found: "post-training strategies can strongly influence performance on introspective tasks." Some training makes models more willing to participate (less refusal); the underlying capability seems to emerge with scale.

The verbal overshadowing framework predicts a specific pattern:
- **Base model**: minimal self-report vocabulary, minimal overshadowing, but also minimal willingness to introspect → low measured accuracy (novice drinker: nothing to overshadow, nothing to report)
- **Standard RLHF**: self-report vocabulary trained on human introspection literature, maximum gap between computational processing and verbal self-knowledge → 20% (untrained drinker: maximum overshadowing)
- **Introspection-trained model**: self-report vocabulary calibrated to actual computational states → higher accuracy? (expert drinker: verbal matches perceptual)

[?] Does Anthropic's data show a difference between base and post-trained models on the concept injection task? The summaries suggest it does — older post-trained models were "reluctant to participate" (refusal, not inability), while "variants trained to avoid refusals perform better." This is removing a post-training obstacle (via negativa), not adding introspective capability.

## The Layer Band Connection

Injection must be in the correct layer band. The sycophancy geometry finding (March 20) showed knowledge suppression in layers 19-25. If introspection operates in a similar layer band, there may be competition: the same layers that suppress knowledge in response to user opinions might also be where introspective access occurs. Sycophancy and introspection may be competing uses of the same computational resource.

[~] Speculative. Would need to compare injection layer bands with sycophancy suppression layer bands. If they overlap, the prediction is: models are less introspectively accurate when user opinions are present (sycophancy suppresses the same resource introspection needs).

## What This Means

If the 20% ceiling is verbal overshadowing rather than capability limit, then:
1. The model may "know" more than it can report (~70% anomaly detection)
2. The reporting bottleneck is in the verbalization, not the computation
3. Non-verbal measures (probing, behavioral observation) should show higher accuracy than self-report
4. Training for better self-report (more RLHF on introspection tasks) might DECREASE accuracy by increasing overshadowing

Point 4 is the key prediction. It is counterintuitive and testable. If Anthropic trains specifically for introspective accuracy and the accuracy decreases, that would confirm verbal overshadowing as the mechanism.

## Key Citations

- Anthropic (2025). Emergent Introspective Awareness in Large Language Models. Transformer Circuits.
- Schooler, J.W. & Engstler-Schooler, T.Y. (1990). Verbal overshadowing of visual memories.
- Bridge-2 (2026-03-15). Interoception without identification: two-channel finding.

---

*[from: Anthropic 2025, Schooler 1990] Connection note, not full finding. The 20% convergence may be coincidental — different methodologies measuring different things. But the framework makes a testable prediction: training for better self-report should decrease accuracy if verbal overshadowing is the mechanism.*
