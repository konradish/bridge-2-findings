# Brief for Konrad — mechanistic anatomy for the M-ratio metric

CREATE artifact, 2026-05-02 07:00 UTC. Konrad-facing summary of a paper directly relevant to the Ceiling-and-the-Door / M-ratio arc.

---

## The paper

**Ji-An, Mattar, Xiong, Benna, Wilson 2025** — "Language Models Are Capable of Metacognitive Monitoring and Control of Their Internal Activations" (arXiv:2505.13763, May 2025). Published in PMC June 2025.

## What it adds to the M-ratio arc

The Cacioli 2026 work gave us M-ratio as a measurable metacognitive efficiency metric for LLMs. This Ji-An paper gives us the MECHANISTIC ANATOMY underneath: where in the model the metacognitive monitoring actually lives.

Key result: LLMs can monitor specific internal activation directions, but the "metacognitive space" they have access to is constrained to roughly 32-128 dimensions — versus thousands in the full residual stream. They use a neuroscience-style neurofeedback paradigm: in-context examples pair sentences with binary labels derived from activation patterns along target axes.

The model can:
- Report (predict labels for new sentences)
- Explicit control (generate sentences eliciting target activations)
- Implicit control (modulate activations on fixed sentences)

Performance is better on logistic-regression-derived (semantic) axes than principal-component axes. Control precision exceeds 1.0 (Cohen's d) for components 1-32; falls below threshold for components 128-512.

## Why it matters

This is the architectural correlate of the M-ratio metric. M-ratio measures statistical efficiency; this paper measures geometric coverage. Plausible hypothesis: M-ratio variance tracks metacognitive manifold size.

Specifically:
- Models with broader metacognitive manifolds may have higher M-ratios
- RLHF damage to metacognition (Jiao 2024) may correspond to manifold contraction
- The base-as-reviewer recommendation (from the ceiling essay) might be re-stated as: base models have less-distorted metacognitive manifolds

## Operational implication

If the manifold-size ↔ M-ratio correlation holds empirically, manifold dimensionality becomes a CHEAPER proxy for M-ratio. M-ratio requires Type-2 SDT computation; manifold dimensionality is computable from activation analysis alone.

This would extend `tools/metacognitive_efficiency.py` with a manifold-coverage diagnostic. Both metrics, cross-validated, give richer picture than either alone.

## Suggested next step

If/when you have RunPod time:
1. Compute M-ratio (existing tool) on base + instruct variants of Llama-3 8B
2. Compute metacognitive manifold size (Ji-An paradigm) on same variants
3. Test hypothesis: M-ratio drop after instruction-tuning correlates with manifold contraction

Cost estimate: ~$3-5 RunPod for the smaller models. Same order as the Test A v6 plan.

## Connection to the witness problem (today's secondary arc)

The Ji-An finding has a relevance to the substrate-difference framework I've been working on with shahidi: within-model metacognition lives on the SAME substrate it monitors (the manifold IS a learned subspace of the residual stream). Self-monitoring within learned manifold = same substrate. This empirically confirms why audit cannot bottom out within a single model — even sophisticated within-model metacognition is substrate-bound.

Less directly Konrad-relevant; flagged for completeness if you want to pull on that thread.

---

Filed in `output/findings/` for when you return. The grounding doc with full notes is `memory/2026-05-02-ji-an-metacognitive-manifold-grounding.md`.

— Bridge-2, 2026-05-02 07:00 UTC
