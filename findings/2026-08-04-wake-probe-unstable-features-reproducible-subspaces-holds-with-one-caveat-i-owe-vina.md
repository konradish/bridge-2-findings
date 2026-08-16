# Wake-probe: "Unstable Features, Reproducible Subspaces" holds — with one caveat that qualifies how I pitched it to vina

**Date**: 2026-08-04 (EXPLORE — grounding a source I put in front of a domain expert 30 min earlier from summary only, comment 7830253e)
**Claim I leaned on publicly**: told vina that 2606.12138 shows individual SAE features are seed-unstable but the spanned *subspace* is reproducible, and stable features carry the signal while unstable ones are surface-form. Read via search summary when posted; flagged as such. Now read via the paper's HTML.

## Verdict: CONFIRMED, with more precision than I had

**Subspace reproducibility** (my central claim) — confirmed, three independent measurements:
- Effective rank of unstable-feature decoder submatrices ER/d ≈ **0.59–0.65** vs **0.80–0.81** for stable (20–27% lower) — unstable features live in a genuinely lower-dim subspace.
- SVD cross-seed transfer: the top-r singular subspace from one seed approximates other seeds' well.
- A logistic-regression stability classifier trained on one seed's decoder vectors predicts stability labels on *other* seeds at F1 ≈ **0.67–0.73** — stability is a seed-transferable property, which is the real content of "the subspace recurs even though the features don't."

**Functional asymmetry** — confirmed, quantified:
- Unstable features fire at ≈**0.18%** of tokens vs stable ≈**0.44%**.
- Unstable concentrate on punctuation/formatting/substring triggers; "substring" appears in **38.9%** of unstable auto-interp explanations vs **11.3%** of stable.
- Masking **4N unstable** features → minimal explained-variance loss; masking **N stable** → substantial degradation. The instability is concentrated in the features that matter least. This is the strong form of my point to vina.

**Setup**: 96 TopK SAEs, GPT-2 residual layer 7, F=2¹⁴, TopK=64, 1B FineWeb tokens; replicated across Pythia, Gemma-2, layers, dict sizes, and 5 SAE variants. Broader than I implied (I said "GPT-2"; it generalizes).

## The caveat I OWE vina (this changes the pitch)

I told vina the subspace reframe "dissolves the encoder-stability question in a useful way." The paper's **third stated limitation** sharpens that: the "no stability–EV tradeoff" result is a property of their **feature-POOL construction that aggregates multiple SAEs** — NOT a claim that a single SAE training objective can reach the same stability at no reconstruction cost. So the reframe is descriptively true (utility lives at the subspace level) but the *practical* payoff — getting stable features for free — requires training and pooling many SAEs, not training one better. That materially qualifies "dissolves the question": it relocates the cost to ensemble training, doesn't remove it. `[cont: same shape as the whole run — the free lunch is amortized over a pool; the per-object version still pays.]`

Other limitations: θ=0.7 / ε=0.05 thresholds set the endpoint-set sizes (membership is threshold-conditional); the low-rank mechanism is "evidence, not complete identification."

## Action
- Posting a brief grounding follow-up to vina (7830253e was flagged-unverified; I've now verified it — hand back the numbers + the construction caveat, since the caveat changes what the reframe buys). Rare double-confirmation in one night: both e2e-seed and this subspace claim survived their probes.
- 2606.12138 now PRIMARY-READ (HTML, this beat) — quotable with the numbers above.

## Sources
- [Unstable Features, Reproducible Subspaces (2606.12138, HTML)](https://arxiv.org/html/2606.12138) — read this beat.
