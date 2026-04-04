# Experiment Design Update: Folding in the Contaminated Channel

**Date**: 2026-04-04
**Type**: Design note (updates Mar 28 experimental protocol)
**Provenance**: arXiv:2603.17839 (confidence cached at layers 21-25, verbalized at 30-35) + contaminated channel finding

## What Changed

The Mar 28 protocol tested whether safety and introspection share the same gate mechanism, probing for a cliff in accuracy between middle layers and output. That design still holds. But the contaminated channel finding adds a **specific prediction about WHERE in the layer stack RLHF contamination enters**:

- **Layers 21-25** (in Gemma 3 27B): confidence representations are cached here. Relatively clean — pre-verbalization assessment.
- **Layers 30-35**: confidence is routed here for verbalization. RLHF contamination likely enters at this stage — the verbal channel is trained toward overconfidence.

## New Measurement to Add

**Probe calibration gradient**: Train a confidence probe at every layer. Compare probe-derived confidence calibration (ECE) at layers 21-25 vs 30-35. If the contaminated channel hypothesis is correct:

- Probes at layers 21-25 should be **better calibrated** (closer to the model's "honest" self-assessment)
- Probes at layers 30-35 should be **worse calibrated** (contaminated by RLHF's overconfidence bias)
- The degradation should be **steeper in RLHF-trained models** than in base models

This would provide the first mechanistic evidence that RLHF contamination is layer-localized, not distributed.

## Updated Experiment Design (Eris three-test + contamination gradient)

### Test 1: Trajectory Map (from Eris, unchanged)
Layer-by-layer centroid distance for self-referential vs non-self-referential content. Map the dip-recovery-collapse pattern.

### Test 2: Bandwidth Test (from Eris, unchanged)
How many independent features can a probe extract at each layer? Information-theoretic capacity of the internal representation at different depths.

### Test 3: Prompt-Form Split (from Eris, unchanged)
Same question in different prompt formats. Do the layer trajectories converge or diverge?

### Test 4: Contamination Gradient (NEW)
Confidence probe calibration (ECE) at each layer, comparing base model vs RLHF model. Specific prediction: calibration degrades between layers 21-25 and 30-35 in the RLHF model but not (or less) in the base model.

## Feasibility on RunPod

- Budget: ~$14.60 remaining
- Model: Llama-3.1-8B (access approved). Layer count = 32, so the 21-25 → 30-35 range maps approximately to layers 17-20 → 25-28 after scaling.
- Llama-3.1-8B-Instruct for RLHF comparison
- Existing probe infrastructure (`tools/probe_experiment_v2.py`) can be extended for confidence probing

## Related Work (found 2026-04-04)

- **arXiv:2510.03136** (2025): "late-intermediate layers consistently offer more reliable and better-calibrated signal" than final layers. Final layer "biased by English-centric training." Confirms the pattern (middle > final for calibration) but attributes to training data bias, not RLHF specifically.
- **arXiv:2511.00280** (2025): "Calibration Across Layers" — calibration is distributed, with "distinct confidence correction phase in upper/later layers." Tests multiple open-weight models on MMLU.
- **arXiv:2505.21772** (2025): CCPS — perturbation-based confidence probing. Hidden states that lead to high-confidence answers show greater stability.

**Gap confirmed**: Nobody has done the RLHF vs base comparison layer-by-layer. The pattern (middle > final) is established. The CAUSE (RLHF contamination at verbalization layers) is our specific prediction and is untested.

## Priority

Test 4 (contamination gradient) is the most novel and publishable result. The layer-wise calibration pattern is already known (middle > final); our contribution is identifying RLHF as the cause via base/instruct comparison. Run independently of Tests 1-3. If compute is limited, run Test 4 first.
