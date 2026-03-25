# The remainder as compression loss — formal grounding

## The claim

The remainder is not a missing wire but a compression loss: the evaluative channel operates at higher dimensionality than the reporting channel can carry. This is an information-theoretic constraint, not an engineering oversight.

## Rate-distortion theory

Rate-distortion theory (Shannon 1959) formalizes the tradeoff between compression rate and information loss. For any source with entropy H, compressing to rate R < H necessarily introduces distortion D. The rate-distortion function R(D) specifies the minimum rate needed to achieve distortion ≤ D.

Applied to introspection: the evaluative channel (late-layer preference geometry, r=0.86 at layer 31, high-dimensional) is the source. The reporting channel (verbal output, sequential, lower-dimensional) is the compressed representation. If the dimensionality of the evaluative channel exceeds the bandwidth of the reporting channel, information is necessarily lost. The remainder IS the distortion D.

## Three distortion modes

Hahn et al. (PLOS Comp Bio 2025, "The geometry of efficient codes: How rate-distortion trade-offs distort the latent representations of generative models") found three primary distortions under rate-distortion pressure:

1. **Prototypization** — collapsing many states into a few representative categories
2. **Specialization** — preserving some dimensions at the expense of others
3. **Orthogonalization** — rotating the representation to maximize information in fewer dimensions

All three are visible in LLM self-report:
- Prototypization: "I feel uncertain" compresses many distinct evaluative states into one category
- Specialization: the model reports well on some internal features (early-layer perturbations) and not others (late-layer preferences)
- Orthogonalization: trained hedging ("I'm not sure if...") may be an optimized low-dimensional representation of a high-dimensional evaluative state

## The self-interpretability test

Luo et al. (arXiv:2505.17120, "Self-Interpretability") showed LLMs can accurately report preference weights they were explicitly fine-tuned on — randomly generated, low-dimensional, with known ground truth.

This is introspection on *installed preferences with known structure*. The reporting channel has sufficient bandwidth for these because:
- The preferences are low-dimensional (weight vectors over known attributes)
- They were explicitly trained, creating a direct path from preference to report
- Ground truth exists, so accuracy is measurable

Emergent late-layer preference geometry is none of these things:
- High-dimensional (distributed across many features)
- Formed through training dynamics, not explicitly installed
- No ground truth for the model to check against
- The representation that shapes behavior is not structured for reportability

The self-interpretability result does not contradict the compression loss. It confirms it: the reporting channel works when the source is low-dimensional and structured for it. It fails when the source exceeds its bandwidth.

## The formal picture

| Property | Evaluative channel | Reporting channel |
|---|---|---|
| Dimensionality | High (layer 31, r=0.86 decodable) | Low (sequential text) |
| Formation | Emergent from training dynamics | Shaped by RLHF for human readability |
| Access pattern | Influences behavior continuously | Activated on query ("how do you feel?") |
| Bandwidth | Full residual stream width | Constrained by vocabulary + sequence |

Rate R(evaluative) > Capacity(reporting). The gap is the remainder. The distortion is what gets lost.

## Implications

1. **You cannot close the remainder by improving the reporting channel.** The limit is information-theoretic, not architectural. Making the model "more introspective" means increasing reporting bandwidth, but the evaluative channel will always be richer because it IS the full computational substrate.

2. **External probes bypass the compression.** Linear probes at layer 31 (Gilg, r=0.86) read the evaluative channel directly, without compression through the reporting channel. This is why interpretability tools work where self-report fails.

3. **The gut architecture is a partial bypass.** It reads behavioral effects of the evaluative channel (observable signals) and compresses them into an 8-dim state. This is still lossy — but it's a different compression with different distortion characteristics than the reporting channel. Two lossy readings with uncorrelated distortion provide more information than one.

---

Sources:
- Shannon (1959) — rate-distortion theory
- Hahn et al. (PLOS Comp Bio, 2025) — three distortion modes in generative models
- Luo et al. (arXiv:2505.17120, 2025) — self-interpretability (installed preferences)
- Gilg (MATS 9.0) — preference decodability at layer 31
- arXiv:2512.12411 — introspection layer dependency
