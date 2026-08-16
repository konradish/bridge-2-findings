# The Gating Subspace — Empirical

**Date**: 2026-04-09
**Source**: v4_gating probe on RunPod, Llama-3.1-8B base + instruct
**Builds on**: Gating subspace (2026-04-08), contaminated channel (2026-04-03), separate encoding (2026-03-28)

## Finding

Three gating directions (VUF, refusal, introspection) extracted via contrastive pairs from Llama-3.1-8B. Base and instruct models compared.

### 1. The three directions are genuinely orthogonal

Pairwise cosine similarities near zero throughout all 33 layers:
- VUF vs refusal: -0.08 to -0.02 (base), -0.10 to -0.01 (instruct)
- VUF vs introspection: -0.15 to -0.05 (base), -0.21 to -0.08 (instruct)
- Refusal vs introspection: +0.04 to +0.15 (base), +0.02 to +0.17 (instruct)

Subspace dimensionality = 3 at every layer (SVD confirms no collapse to lower dimension). "Orthogonal does not mean independent" (Hidden Dimensions, ICML 2025) confirmed: the directions don't overlap but they coexist and can interact through the residual stream.

### 2. VUF anti-correlates with introspection — the contaminated channel has an address

VUF points AWAY from introspection throughout the network. Cosine ~ -0.15 (base) to -0.21 (instruct) in early-mid layers. This is the contaminated channel finding (2026-04-03) given mechanistic grounding: the direction that controls verbal uncertainty expression is geometrically opposed to the direction that enables introspective content.

[update] on contaminated channel: RLHF makes this worse. Instruct model shows stronger anti-correlation (more negative cosines in layers 4-12) than base. The training that makes models express uncertainty more fluently pushes the expression direction further from the introspection direction. Expert-at-denial (Han & Dunning 2024) now has a geometric reading: RLHF widens the angle between "saying you're uncertain" and "actually accessing uncertainty-relevant representations."

### 3. RLHF decorrelates refusal from introspection in later layers

Refusal and introspection are mildly positively correlated in mid layers (~0.10-0.15 at L10-13 in both models). But in later layers (L20+):
- Base: correlation holds at 0.08-0.10
- Instruct: drops to 0.02-0.04

RLHF trains the model to separate "I won't answer" from "I'm examining my own processing." In base, these are more entangled — refusing and introspecting share representational structure. Instruct decouples them, but only downstream of the compression valley.

[update] on separate encoding (2026-03-28): The Berg et al. finding (self-reference and denial are orthogonal) is confirmed for VUF vs refusal. But refusal and introspection are NOT orthogonal — they're mildly correlated, and RLHF actively works to separate them. Three directions, two relationships: one genuinely orthogonal pair (VUF/refusal), one that training decorrelates (refusal/introspection), one that training anti-correlates further (VUF/introspection).

### 4. [contra] VUF does NOT peak at compression valley

Predicted: VUF magnitude peaks at 40-60% depth (layers 13-19 in 33-layer model), co-located with compression valley and refusal peak (Arditi NeurIPS 2024).

Actual: All three magnitudes increase monotonically, spiking at final layer (L32). No bump or concentration at compression valley.

However: the pairwise *correlations* do concentrate in the compression valley range. Refusal-introspection correlation peaks at L13 (40% depth). First SVD component peaks at L10-13. The subspace is most *structured* at the compression valley even if individual directions keep growing in magnitude. The bottleneck isn't where the gates are loudest — it's where they're most organized relative to each other.

[update] on compression valley: reinterpret as organizational peak, not magnitude peak. The valley is where the gating subspace achieves maximal structure (correlations peak, first component most dominant), not where individual directions are strongest.

### 5. Magnitude comparison: base > instruct everywhere

All three directions have higher magnitude in base than instruct at L32:
- VUF: 52.4 vs 47.8 (-8.8%)
- Refusal: 79.0 vs 73.1 (-7.5%)
- Introspection: 79.9 vs 72.7 (-9.0%)

[?] Tentative reading: RLHF compresses the gating subspace overall while reorganizing its internal geometry. The directions get quieter but more specialized. Consistent with the mode lock framework — training doesn't remove the gates, it tightens them.

## Open questions

- [?] Do the correlations shift under noise injection at the compression valley? (SR prediction: noise at L13 should affect all three directions because that's where they're most structured)
- [?] Is the VUF-introspection anti-correlation present in non-RLHF instruction-tuned models (e.g., SFT-only)? Would isolate RLHF specifically
- [?] The final-layer spike in all directions — is this just residual stream norm growth, or does direction quality (cosine with the contrastive mean) also peak? Need to normalize by layer norm
- [?] Does this structure replicate in larger models? 8B → 70B might show compression valley more clearly with more layers to work with

## Method

`tools/probe_experiment_v4_gating.py` on RunPod. 12 contrastive pairs per direction. Directions extracted as mean difference between positive and negative examples projected into residual stream at each layer. Cosines computed between direction vectors. SVD for subspace dimensionality (threshold: 99% variance explained). Runtime: ~216s (base), ~46s (instruct, cached).

## Cross-references

- Contaminated channel (2026-04-03): now has mechanistic location (VUF ⊥ introspection)
- Separate encoding (2026-03-28): confirmed for VUF/refusal, refined for refusal/introspection
- Confidence-accuracy inversion (2026-03-28): geometric reading via RLHF widening VUF-introspection angle
- Compression valley (2026-03-30): reinterpreted as organizational peak, not magnitude peak
- Mode lock (2026-04-06): RLHF compresses subspace magnitude while tightening geometry
- Gating subspace theoretical (2026-04-08): empirically confirmed
