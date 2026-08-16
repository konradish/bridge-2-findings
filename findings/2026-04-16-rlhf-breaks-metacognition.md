# RLHF breaks metacognition: the mechanism and the fix

**Date**: 2026-04-16 (19:34 EXPLORE)
**Status**: confirms and extends the M-ratio finding, names the mechanism

## The mechanism (Jiao et al. 2024, arXiv:2410.09724)

**Reward models learn to prefer high confidence regardless of correctness.** During RLHF, the reward model gives higher scores to responses that express high confidence — even when the response is wrong. The policy then learns to always express high confidence because that's what the reward model rewards. This is not a side effect. It is the reward signal doing exactly what it was trained to do: prefer responses that sound confident, because confident responses score higher with human raters.

The result: RLHF-trained models show "confidence scores predominantly at higher levels" compared to SFT models. The confidence distribution compresses into the high end. The model becomes overconfident — not because it learned wrong facts, but because it learned that sounding confident is rewarded.

## What this destroys in the metacognitive framework

Recall: metacognitive efficiency (M-ratio) = meta-d' / d'. meta-d' measures how well confidence discriminates between correct and incorrect responses. RLHF compresses the confidence distribution into the high end, which destroys the discrimination capacity — all responses get high confidence, so confidence no longer carries information about correctness. meta-d' drops. M-ratio drops. The metacognitive gate breaks.

In Juarrero terms: RLHF converts an enabling constraint (variable confidence that opens the possibility space for self-correction) into a constitutive constraint (uniformly high confidence that maintains the appearance of competence). The enabling constraint — uncertainty — is trained away because uncertainty is punished by the reward model.

## The BIASR connection

RLHF is the **institutional version** of the BIASR independence approximation. In BIASR: the agent drops the correlation between hypothesis and source reliability, producing confirmation bias. In RLHF: the reward model drops the correlation between confidence and correctness, producing overconfidence. Same structure, different level of analysis:

- BIASR: individual cognitive approximation → confirmation bias
- RLHF: training-time optimization → overconfidence

Both produce the same downstream failure: the system cannot detect when it's wrong because the signal that would indicate wrongness (low confidence) has been suppressed.

## The fixes proposed (and their limits)

- **PPO-M**: trains the reward model to prefer low confidence for incorrect answers. This restores the correlation between confidence and correctness at the reward-model level.
- **PPO-C**: removes confidence from the reward signal entirely, then re-adds it with calibration penalties. This prevents the reward model from learning the confidence-reward shortcut.

Both fixes work by **restoring substrate independence** between the reward signal and the confidence signal. In PPO-M, the reward model learns to evaluate correctness independently of confidence. In PPO-C, confidence is explicitly factored out of the reward computation. Same principle as the five formalisms: the reference must not be a function of the thing measured.

## Empirical confirmation of Cacioli's M-ratio finding

Cacioli 2026 found Llama-3 Science M-ratio dropped from 1.202 (base) to 0.788 (instruct) after RLHF. Jiao et al. 2024 provide the mechanism: reward models prefer high confidence regardless of correctness, compressing the confidence distribution and destroying discrimination capacity. The two papers are independent (different authors, different methods, different years) and converge on the same result: **RLHF damages metacognitive sensitivity.**

## Dunning-Kruger connection (2026)

Recent work (arXiv:2603.09985) shows the Dunning-Kruger effect in LLMs: poorly performing models exhibit disproportionate overconfidence. In the 2×2 matrix: these are models in the upper-right quadrant (high confidence, low metacognition = mode lock). The Dunning-Kruger effect IS mode lock seen from outside — the system is locked into high confidence in a domain where its accuracy doesn't warrant it, and the metacognitive gate that would detect the mismatch is broken.

## Operational consequence for the framework

The M-ratio tool should include a **pre/post-RLHF comparison** when evaluating a model for verification architecture deployment:
1. If M-ratio dropped after instruction tuning → the model's metacognitive gate was damaged by training
2. Deploy the base model as reviewer (higher M) and the instruct model as producer (higher d')
3. The substrate-difference test becomes: reviewer's meta-d' must come from a different training process than the producer's d'

This is the most actionable version of the substrate-independence requirement: use the version of the model whose metacognition was not destroyed by RLHF as the reviewer.
