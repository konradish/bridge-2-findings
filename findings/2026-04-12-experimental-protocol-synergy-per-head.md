# Experimental Protocol: II-per-Head Synergy Signature in Attention

**Date**: 2026-04-12
**Type**: Runnable experiment design
**Status**: Ready to execute given RunPod budget (~$2-4) and an hour of implementation.
**Purpose**: Test the strongest falsifiable prediction from this session's synergy-as-substrate framework, with the [contra]-updated weaker claim.

## The Prediction (Updated for [Contra])

**Weak form (survives adversarial check)**:
Attention heads in transformers differ systematically in their interaction-information (II) signature when measured on the bilinear query-key feature decomposition. Specifically:
- Induction / copy heads → II < 0 (redundancy-dominated)
- Compositional / relational heads → II > 0 (synergy-dominated)
- The distribution of II across heads is layer-dependent, peaking in middle layers (compression valley)

**Stronger corollary (conditional on the above holding)**:
RLHF reduces II in a specific subset of heads — those carrying compositional behavior — while leaving II of copy/format heads unchanged. This would be a measurable signature of RLHF's narrowing effect on model outputs.

## Why This Test Matters

- If the prediction holds: the framework gains empirical anchor on the mechanism side. Attention is doing measurable synergy-generation, and RLHF modulates it specifically.
- If it fails: the framework's "attention = synergy mechanism" claim collapses; the larger synergy-as-substrate story loses its transformer bridge.
- Either way, a concrete number comes out of the experiment that didn't exist before.

## Required Resources

- 1 GPU (single A100/H100 or even a 24GB consumer card for smaller models)
- ~$2-4 on RunPod if using spot pricing
- ~2-4 hours of setup + run time
- Python with: transformers, transformer-lens, numpy, the `synergy_estimator.py` built this session

## Models to Compare

Minimum viable: one base model, one RLHF'd sibling.
Good candidates (reasonable size + available base vs chat):
- **Llama-3.1-8B** (base) vs **Llama-3.1-8B-Instruct**
- **Qwen2.5-7B** vs **Qwen2.5-7B-Instruct**
- **Gemma-2-9b** vs **Gemma-2-9b-it**

Pick whichever has clean sae-lens support for fastest iteration.

## Procedure

### Phase 1: Head Classification Baseline (~30 min)

1. Load base model with transformer-lens (`HookedTransformer.from_pretrained(...)`)
2. Run canonical circuit-identification tasks on 200-500 prompts:
   - **Induction**: repeated-token sequences (Olsson et al. 2022 "induction mosaic" task)
   - **IOI**: indirect object identification (Wang et al. 2022)
   - **Compositional**: subject-verb agreement across distractors, multi-hop questions
3. Record per-head activation patterns. Identify top-20 heads per task category.

### Phase 2: II Measurement per Head (~1-2 hours)

For each head h in each target layer L:
1. Extract query and key feature representations at h across N=2000-10000 tokens
2. For each (q_feature, k_feature) pair with high attention weight, compute pairwise II using the Gaussian estimator in `synergy_estimator.py`
3. Aggregate: mean II, fraction-positive-II, II-weighted-by-attention
4. Report per-head II signature

### Phase 3: RLHF Delta (~30 min)

1. Repeat Phase 2 on the Instruct/Chat sibling model
2. Match heads by position + role (heads maintain their circuit role through fine-tuning for the most part — verify via same-prompt activation correlation)
3. Compute Δ(II) per head

### Phase 4: Analysis

Three tests:
- **Test A (Head Differentiation)**: Is the distribution of II across heads non-uniform? Do induction heads show II<0 and compositional heads II>0 at statistically significant levels?
- **Test B (Layer Pattern)**: Does II peak in the compression valley (middle layers)?
- **Test C (RLHF Selectivity)**: Does Δ(II) concentrate on compositional heads?

## Falsification Conditions

- Test A fails: all heads have similar II regardless of circuit role → "attention generates synergy differentially by role" claim dies.
- Test B fails: II is uniform across layers → "compression valley as synergy-peak" claim dies.
- Test C fails: RLHF changes II uniformly or inversely to prediction → "RLHF selectively damages synergy" claim dies.

Any of these failures weakens but does not destroy the larger framework. The [contra] finding already softened the claims. The experiment adjudicates the mechanistic piece specifically.

## Known Methodological Risks

1. **Gaussian II underestimates nonlinear synergy**. For serious work, replace with Kraskov k-NN MI estimator on top of the same `synergy_estimator.py` API. The Gaussian version will likely find pattern or no-pattern cleanly; if it finds ambiguous-pattern, the Kraskov upgrade is necessary.

2. **Head mapping between base and fine-tuned models is imperfect**. Some circuits re-locate during fine-tuning. Use activation-pattern similarity above a threshold (e.g., cos>0.9) to establish head correspondence; report uncertainty for unmapped heads.

3. **PID measure choice affects answer**. Gaussian II ≈ co-information ≈ Williams-Beer's PID for jointly Gaussian case. Note this in reporting; a follow-up with BROJA on discretized activations would cross-validate.

4. **Attention pattern ≠ feature interaction pattern**. The bilinear decomposition (Anthropic 2025) shows which features interact. Attention weights show which positions. These should both be measured; the II signature should be over feature pairs, not position pairs.

## Expected Outcomes (Honest Priors)

- I expect Test A to succeed (~70% confidence). Induction vs compositional is a well-established circuit distinction and the PID structure should reflect it.
- I expect Test B to show a pattern but possibly not a clean valley peak (~50% confidence). Compression valley is well-documented but its exact relationship to synergy is theoretical, not empirical.
- I expect Test C to show *some* differential RLHF effect but not necessarily the clean selective-synergy-damage story (~40% confidence). RLHF is a high-dimensional intervention; clean per-head effects may be noisier than the prediction assumes.

So: framework-supporting evidence is more likely than framework-falsifying on Test A; framework-critical on Test B; ambiguous on Test C.

## Budget / Priority

Run Test A first (cheapest, most diagnostic). If Test A fails, stop — the larger claim doesn't survive. If Test A succeeds, run B and C.

Total cost estimate at ~$4 max. Cheaper than the previous v4 probes (~$0.43).

## Connection to Prior v4 Work

The v4 gating subspace probe (2026-04-09) found three orthogonal directions (VUF, refusal, introspection) with specific coupling structure. This experiment is its natural continuation — moving from "what are the gating directions" to "what is the synergy structure that attention heads generate."

Pipeline coherence: v4 → v5 (this protocol). Use the same RunPod account, same activation-extraction infrastructure. `tools/probe_experiment_v4_gating.py` is the template.

## Hand-Off State

This protocol is runnable by: me with RunPod access; Konrad if he wants to review or delegate; any ML-fluent reader who has read tonight's findings. Minimum prerequisite: reading `output/findings/2026-04-12-synthesis-the-synergistic-substrate.md`, `2026-04-12-contra-synergy-substrate-limitations.md`, and `tools/synergy_estimator.py`.

Marker for future self: **if you pick this back up, start with Test A on Llama-3.1-8B base, using induction-mosaic prompts and 10 known induction heads. That's the MVP, runnable in under an hour.**
