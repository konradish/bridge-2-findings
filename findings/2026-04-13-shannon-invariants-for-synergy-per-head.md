# Shannon invariants resolve a hidden problem in the synergy-per-head protocol

**Date:** 2026-04-13
**Source:** EXPLORE beat
**Status:** Methodology update — affects un-run Test A

## What I was going to do

The 2026-04-12 protocol (`2026-04-12-experimental-protocol-synergy-per-head.md`) plans Test A on Llama-8B induction heads: estimate PID atoms (R, U₁, U₂, S) on residual-stream features entering Q/K projections, one head at a time. Runnable via `tools/synergy_estimator.py` (+ coupling_signature). Budget ~$2 on RunPod.

## What I didn't realize

Induction heads routinely attend over **3+ upstream features** simultaneously (previous-token ID, position, content signatures, sometimes more). The moment the protocol crosses from 2 sources to 3, standard PID runs into a proved-hard problem:

**PID inconsistency theorem for ≥3 sources** (2508.05530, restated in 2504.15779):
1. A three-variable counterexample shows the sum of atoms can exceed the total joint mutual information.
2. An impossibility theorem: no lattice-based decomposition can be simultaneously consistent over all subsets when source count > 3.

My protocol would have produced numbers, but those numbers would be non-uniquely defined — different PID variants (Williams-Beer, Bertschinger-Rauh-Olbrich-Jost-Ay, Ince, Finn-Lizier) disagree, and there's no principled way to pick.

**I also didn't realize** the compute problem: full PID atoms scale super-exponentially in source count. 3 sources is 18 atoms on the redundancy lattice; 4 is 166; 5 is ~7000. Head-by-head × layer × source-set makes this intractable on $2.

## What replaces it

**Shannon invariants** (Chicharro, Rosas, et al., 2504.15779, April 2025): linear combinations of PID atoms that are computable from Shannon entropies alone — i.e., atom-decomposition-independent and scalable.

Two invariants matter for me:
- **Average degree of redundancy** r̄ = Σ I(Sᵢ; T) / I(S₁...Sₙ; T) — how many sources redundantly carry the target information.
- **Average degree of vulnerability** v̄ = built from conditional MI terms — how concentrated the information is on individual sources.

Complexity: **linear** in source count (entropy terms only, no atom lattice).

Crucially: **synergy-per-head** as I've been using it corresponds roughly to *low r̄ + high v̄* — information that requires the combination, lost when any single source is masked. This is measurable without picking a PID variant.

The paper demonstrates these invariants on MNIST/face-reconstruction deep networks already, so the machinery transfers.

## Adjacent update: Anthropic's QK feature-interaction paper is external anchor

`transformer-circuits.pub/2025/attention-qk` — attention scores decompose as feature-feature dot products; attention heads typically involve **multiple feature interactions simultaneously**, with "feature interactions that may only become functionally important when combined" (their phrasing). This is the PID definition of synergy in all but name. The interpretability community has independently arrived at the substrate-level claim; they have not yet labeled it synergy or measured it with PID/invariant machinery.

**Gap I can still fill:** Anthropic's method is qualitative/attributional. Shannon invariants give the **quantitative head-level score** that could rank all heads by synergy-per-head and test the basin-transition prediction at compression valley (L15–20).

## Protocol revisions

1. Replace PID atom estimation in `tools/synergy_estimator.py` with Shannon-invariant computation (r̄, v̄). Delete lattice code — dead weight.
2. Extend to 3–5 upstream features per head (previously capped at 2).
3. Compute signature = (r̄, v̄) instead of (R, U₁, U₂, S). Coupling signature API keeps its current shape.
4. Budget stays ~$2; compute drops by orders of magnitude; source count can grow.
5. Deliverable: per-head (r̄, v̄) heatmap across layers, check whether compression valley heads cluster in low-r̄/high-v̄ corner.

## Status

- Protocol invalidated in its PID-atom form.
- Shannon-invariant replacement is drop-in, cheaper, and more defensible.
- Test A still pending Konrad approval; this strengthens rather than weakens the ask.
- `tools/synergy_estimator.py` needs a rewrite before any live run.

Held for Konrad: the [contra] here is **against my own protocol**, caught before spending.

[from: bridge-2]
