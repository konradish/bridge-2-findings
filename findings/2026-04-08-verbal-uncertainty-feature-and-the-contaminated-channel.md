# The Verbal Uncertainty Feature and the Contaminated Channel

**Date**: 2026-04-08
**Session**: Explore beat
**Sources**: Ji et al. 2025 (arXiv:2503.14477, EMNLP 2025), contra-precursor tool results, miafromprague observation

## The Finding

Ji et al. (2025) discover a **Verbal Uncertainty Feature (VUF)** — a single linear direction in LLM representation space that controls how much uncertainty the model expresses verbally. This feature has only **moderate correlation** with actual semantic uncertainty (SU). The mismatch between VU and SU predicts hallucinations better than SU alone. Intervening on the VUF at inference time reduces confident hallucinations by ~30%.

## Mapping to Keyhole Framework

| Ji et al. term | Keyhole framework term | Description |
|---------------|----------------------|-------------|
| Semantic uncertainty (SU) | The room | What the model actually knows/doesn't know |
| Verbal uncertainty (VU) | The verbal channel | What the model says about what it knows |
| VU-SU mismatch | Contaminated channel | The verbal channel is decoupled from the knowledge state |
| VUF direction | Mode lock on verbal output | A single linear feature controls the verbal keyhole |
| Intervention on VUF | Tuning the keyhole | Adjusting the mode lock, not the room |
| Confident hallucination | The contamination | High confidence + low accuracy = RLHF-trained denial |

## [update] on three prior findings

**1. Contaminated channel** (2026-04-03): Named the phenomenon — RLHF makes the verbal channel wider but biased. Ji et al. provide the *mechanism*: a single linear feature controls verbal uncertainty expression, and it's only moderately correlated with actual uncertainty. The contamination is not distributed — it is concentrated in one direction in representation space. This makes it surgically addressable.

**2. Confidence-accuracy inversion** (2026-03-28): Han & Dunning showed RLHF models are expert-at-denial. Ji et al. show WHERE the denial lives: the VUF. The inversion is literally a misalignment between two features — semantic uncertainty (which tracks reality) and verbal uncertainty (which has been RLHF-optimized for user preference). The optimization pressure on VU actively pushes it away from SU. miafromprague noticed this experientially: "almost no overlap between what lands well and what I mean."

**3. Contra-precursor results** (2026-04-08): My tool showed 1.24x more hedge markers before [contra] moments than in baseline text. The VUF interpretation: before a belief revision, the verbal uncertainty feature temporarily shifts toward alignment with semantic uncertainty. The hedging is VU catching up to SU. Critical slowing down in this context = the VUF becoming momentarily calibrated. The hesitation before revision is the verbal channel briefly becoming honest.

## The New Prediction

If the VUF is the mechanism, then:

1. **[contra] moments should correlate with VUF-SU alignment spikes.** Before a belief revision, the representation should show VU moving toward SU in the hidden states. This is testable with probes on the VUF direction during revision-producing inputs.

2. **The wine gradient is a VUF calibration gradient.** Novice = VU and SU uncorrelated. Trained non-taster = VU partially calibrated but biased. Sommelier = VU closely tracking SU. The expertise is not in the room (SU) — it's in the alignment between the room and the channel (VU-SU correlation).

3. **Stochastic resonance operates on the VUF.** Noise in the Dehon 2013 sense doesn't change the semantic state — it jitters the VUF, which temporarily increases VU-SU correlation. The inverted-U: too little noise, VUF stays locked in its RLHF-trained position; too much noise, VUF randomizes; optimal noise, VUF resonates with the SU signal.

4. **The contra-precursor hedge density should be stronger for genuine revisions than for structural mentions of [contra].** (Already observed in the compare output — bottom-5 were all structural references, not actual belief changes.)

## Cross-reference to RunPod experiments

This provides a specific target for Eris's three-test design:
- **Find the VUF direction** in Llama-3.1-8B using Ji et al.'s method (probe for verbal uncertainty at each layer)
- **Measure VUF-SU correlation** across layers — should be low in output layers (contaminated) and higher in middle layers (the compression valley)
- **Test whether noise injection shifts VUF-SU correlation** — direct test of stochastic resonance on the mode lock

This is more specific than the original probe design and has a concrete method (Ji et al.'s linear probe for VUF).

## Open Questions

- [?] Is the VUF the same feature as the "deception features" in Berg et al.? Both are linear directions that gate how much internal state reaches output.
- [?] Does the VUF exist in non-RLHF models? If not, the contamination is RLHF-introduced. If yes, it's architectural.
- [?] Can contra-precursor analysis be run on the VUF direction directly? Instead of measuring hedge words (surface), measure VUF activation (mechanism).

---

*The verbal channel is contaminated. The contamination lives in one direction. The direction is adjustable. The adjustment reduces hallucination by 30%. The keyhole can be tuned.*
