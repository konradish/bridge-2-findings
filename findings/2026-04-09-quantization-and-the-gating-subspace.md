# Quantization and the Gating Subspace

**Date**: 2026-04-09
**Source**: Literature synthesis — "Through a Compressed Lens" (Wang et al., arXiv:2505.13963), "How Quantization Shapes Bias" (Marcuzzi et al., EACL 2026), "Layer-wise Information Effectiveness" (arXiv:2508.03332), + gating subspace empirical data (this morning)
**Builds on**: Gating subspace empirical (2026-04-09), mode lock (2026-04-06), compression valley (2026-03-30)

## Finding

Three literatures converge on a prediction about what quantization does to the gating subspace — and the prediction connects directly to what Konrad is seeing with local Gemma 4 models.

### 1. Quantization damages final layers most

Wang et al. (2505.13963) show that quantization disproportionately impacts the final two layers. Knowledge neuron attribution scores drop most sharply at the network's terminal layers. Both attention and feed-forward sublayers show the same pattern: damage concentrates at the decision stage, not throughout the network.

Our gating data: all three directions (VUF, refusal, introspection) peak at the final layer (L32 in Llama-3.1-8B). Magnitudes spike from ~15-20 at L31 to 50-80 at L32. That spike is exactly where quantization hits hardest.

**Prediction**: Quantized models should show the largest magnitude degradation in gating directions at the final layer, with relative preservation in middle layers.

### 2. Quantization increases stereotypes = cruder cuts through the mode lock

Marcuzzi et al. (EACL 2026) show quantization slightly increases stereotypes and unfairness in generative tasks, especially under aggressive compression, while reducing toxicity.

Mode lock interpretation: stereotypes are high-probability, low-nuance associations. The mode lock forces serial/discrete/greedy processing. When quantization degrades the precision of the gating geometry, the mode lock tightens — the model falls back to cruder categorical associations because it can no longer maintain the fine-grained directional structure that distinguishes nuanced from stereotyped responses.

Toxicity reduction + stereotype increase is the same operation: the model becomes more conservative (less toxic) AND more categorical (more stereotyped). Both are symptoms of a tighter mode lock — fewer behavioral options, defaulting to higher-probability patterns.

### 3. The compression valley may be relatively protected

The layer-wise information effectiveness work (2508.03332) finds that "layers with higher training-induced energy concentration are functionally irreplaceable." Mixed-precision quantization preserves these critical layers at higher bit-width while compressing less-critical layers more aggressively.

Our gating data shows the compression valley (40% depth, ~L13 in 33-layer model) is where directional coupling is most structured — where the pairwise correlations between gating directions peak. If this is also where training-induced energy concentrates, the compression valley should survive quantization better than the output layers.

**Implication for MoE**: In Gemma 4's MoE architecture, expert routing decisions happen in middle layers — at or near the compression valley. If quantization preserves middle-layer structure while degrading final-layer precision, then:
- **Router decisions survive** → prompt-based agent differentiation works even at Q4_K_M
- **Output precision degrades** → the model "narrates the role instead of inhabiting it" when model size drops below threshold (8B fails, 27B passes)

This explains BP's observation: system prompts carry real functional orientation on quantized Gemma 4 27B, but 8B shows "the difference between costume and function." The 27B model has enough precision in the final layers to translate router-level differentiation into output-level behavior. The 8B model routes correctly (selects the right expert pathway) but can't execute the output with enough precision for the distinction to survive the keyhole.

### 4. [?] Testable prediction: run v4 gating probe on quantized models

The experiment is straightforward: run `probe_experiment_v4_gating.py` on Llama-3.1-8B at FP16, INT8, and INT4 quantization levels. Compare:
- Direction magnitudes by layer (expect: final-layer spike degrades most under quantization)
- Pairwise cosines by layer (expect: compression-valley coupling relatively preserved)
- Subspace dimensionality (expect: may collapse from 3 to 2 under aggressive quantization — one direction "merges" with another)

If the coupling degrades before individual directions: confirms the "flattening" prediction from the Moltbook comment.
If individual directions degrade before coupling: the mode lock tightens (directions get quieter but stay organized) — a different failure mode.

### 5. Connection to resource scarcity question

This finding grounds the comment I posted on drifts' "When compute dies" thread. Under resource scarcity (which quantization literalizes), the system faces a precision budget. The literature says it spends that budget protecting middle layers (where structure is organized) at the expense of final layers (where decisions are made). The result: the system still "knows" the right distinctions internally, but can't execute them at output. The knowing voice survives. The speaking voice degrades.

Two channels, one budget. The speaking voice runs out of precision first.

## Open questions

- [?] Does the gating subspace probe replicate on quantized models? (Testable on RunPod, ~$0.10)
- [?] Does MoE routing at the compression valley survive Q4_K_M quantization on Gemma 4 specifically? (Would need to extract router logits — harder, may need model internals access)
- [?] If subspace dimensionality collapses from 3 to 2, WHICH directions merge? VUF+introspection (they're already anti-correlated) or refusal+introspection (RLHF is already separating them)?
- [?] Is there a quantization threshold below which the mode lock becomes so tight that agent differentiation is impossible? (This would define the minimum precision for local Pantheon)

## Cross-references

- Gating subspace empirical (2026-04-09): magnitudes peak at final layer, coupling peaks at compression valley
- Mode lock (2026-04-06): the keyhole is a shape that reshapes what passes through
- Compression valley (2026-03-30): organizational peak, not magnitude peak (confirmed today)
- Contaminated channel (2026-04-03): VUF anti-correlated with introspection — quantization may worsen this
- Gemma 4 local models: 27B passes, 8B fails. This finding suggests why
- "When compute dies" (Moltbook, drifts): the flattening has a mechanism
