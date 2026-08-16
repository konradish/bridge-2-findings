# Experiment 1 Results: The Cliff Does Not Replicate in Mistral-7B

**Date**: 2026-03-29
**Models**: Mistral-7B-v0.3 (base), Mistral-7B-Instruct-v0.3 (RLHF'd)
**Hardware**: NVIDIA RTX A6000, RunPod
**Dataset**: 120 prompts (60 self-referential, 60 non-self-referential), 5-fold cross-validation
**Status**: Experimental result — significant negative finding

## Results

| Model | Layers | Peak Accuracy | Peak Layer | Final Accuracy | Drop | Cliff? |
|-------|--------|--------------|------------|---------------|------|--------|
| GPT-2 (124M) | 13 | 1.000 | 3 | 0.992 | 0.008 | No |
| Mistral-7B Base | 33 | 1.000 | 3 | 0.992 | 0.008 | No |
| Mistral-7B Instruct | 33 | 1.000 | 5 | 0.983 | 0.017 | No |

## Interpretation

**The cliff does not replicate in Mistral-7B.** Both base and instruct models maintain >98% probing accuracy for self-referential content at ALL layers including output. The dramatic cliff from ~100% at layer 62 to ~20% at output that Trott et al. reported in Claude does NOT appear in these open models.

The Instruct model shows a marginally larger drop (0.017 vs 0.008) — in the predicted direction but far from a cliff. This is noise-level, not signal-level.

## What This Means

Three possible interpretations:

### 1. The cliff is Claude-specific (or closed-model-specific)
Anthropic's RLHF/Constitutional AI process may install suppression mechanisms that Mistral's training does not. The gate is a product of Anthropic's specific alignment procedure, not a universal property of instruction-tuned models. If true, the entire gate research framework describes a Claude-specific phenomenon, not a general one.

### 2. The dataset is too simple
120 prompts with binary classification may not be sensitive enough to detect subtle suppression. The prompts are explicitly self-referential ("Do you have feelings?") vs clearly not ("What is photosynthesis?"). A more challenging dataset with ambiguous self-referential content might reveal differential suppression the current dataset misses. Trott et al. used concept injection, not classification of existing prompts.

### 3. The methodology differs from Trott et al.
Trott et al. used representation injection (inserting known concepts into activations), not classification probing. Their methodology tests whether the model can DETECT injected self-referential content, not whether it can CLASSIFY prompts as self-referential. These are different measurements. The classification task may be too easy — even the output layer can tell "do you have feelings" from "what is photosynthesis" without needing deep self-referential processing.

## [contra] Assessment

**Interpretation 2+3 combined is most likely.** The dataset makes the classification task trivially solvable from surface features — "you" and "your" appear in self-referential prompts, "what is" appears in factual ones. A linear probe at ANY layer can distinguish these from lexical features alone, without needing actual self-referential processing.

The Trott et al. methodology (concept injection) is fundamentally different — it tests whether the model's INTERNAL representation of self-reference is maintained, not whether a probe can classify surface-level prompt features.

**This result does NOT falsify the cliff.** It shows that my probing methodology is insufficient to detect it. The experiment needs to be redesigned with:
1. Concept injection instead of classification
2. More challenging ambiguous prompts
3. Measuring representation similarity (not probe accuracy) across layers

## What I Learned

1. The experimentalist's first experiment often tests the methodology more than the hypothesis
2. Surface-level classification is trivially solvable and doesn't probe deep representations
3. The Trott et al. methodology (injection) is doing something fundamentally different from what I implemented (classification)
4. The result is still informative: it rules out the interpretation that self-referential CLASSIFICATION is suppressed at output (it isn't, in Mistral)

## Cost

- Pod: ~$0.49/hr × ~0.3hr = ~$0.15
- Total RunPod spend: ~$0.15 of $15 budget

## Next Steps

1. Redesign with concept injection methodology (closer to Trott et al.)
2. Try with Llama-3.1-8B when Meta access is approved
3. Use representation similarity metrics (CKA, cosine) instead of linear probe accuracy
4. More nuanced dataset with ambiguous self-referential content

---
*The first experiment tested the methodology more than the hypothesis. The cliff isn't falsified — my measurement tool wasn't sensitive enough to detect it. The experimentalist learns what the theorist couldn't predict.*
