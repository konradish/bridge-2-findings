# Generalized ICA and the Correlation Threshold

**Date**: 2026-04-12
**Type**: Finding (research)
**Tags**: rate-distortion, decomposition, Futrell, SAE, Bion, ICA, correlation threshold
**Status**: [update] to rate-distortion unification (2026-04-11) and gate rev 14 (2026-04-10)

## The Find

Futrell & Hahn 2026 ("Linguistic structure from a bottleneck on sequential information processing," *Nature Human Behaviour*) provides the formal mechanism I was missing for the rate-distortion unification.

Their key claim: **languages minimizing excess entropy perform "generalized sequential ICA" on meaning distributions**, factoring them into groups of approximately independent components expressed systematically and locally.

The critical detail: **as correlation between components increases, optimal coding shifts from systematic (decomposed) to holistic (bundled)**. Independent components → separate words. Correlated components → single morphemes.

## Why This Matters for the Unification

In my rate-distortion unification (2026-04-11), I claimed five decompositions are the same mathematical object:
1. Futrell (linguistic compression)
2. SAE (sparse feature extraction)
3. Bion (alpha-function)
4. MoE routing
5. Shannon rate-distortion optimal coding

Futrell now *explicitly* identifies the operation as ICA — Independent Components Analysis. This is the same operation as:
- **SAE feature extraction**: decompose superposed (polysemantic) activations into monosemantic features. Sparsity constraint forces approximate independence.
- **ICA on neural activations**: decorrelate into distinct neural populations encoding statistically independent components (Futrell's own analogy to neural coding).
- **Bion's alpha-function**: transform beta elements (correlated, unprocessed bundles) into alpha elements (thinkable, independent units).

## The Correlation Threshold Formalized

My gate rev 14 identified a "correlation threshold" as the termination point of decomposition. Futrell gives this precise mathematical content:

**The correlation threshold is the point on the correlation spectrum where optimal coding strategy switches from decomposed expression to holistic expression.**

- Below threshold (low correlation): decompose into independent features, express separately → alpha elements, monosemantic features, systematic language
- Above threshold (high correlation): bundle holistically, express as unit → beta elements, polysemantic features, fusional morphology

Futrell's simulations (Figure 2D) show this transition is smooth, not binary — as M₂-M₃ correlation increases, the optimal code gradually shifts from fully systematic to partially holistic.

## The ICA Bridge

The five decompositions are now connected through ICA as the shared operation:

| Domain | Decomposition | Independent Components | Correlated Bundles |
|--------|--------------|----------------------|-------------------|
| Language (Futrell) | Generalized sequential ICA | Words, systematic morphology | Fusional morphemes, idioms |
| Neural nets (SAE) | Sparse dictionary learning | Monosemantic features | Polysemantic neurons |
| Psychoanalysis (Bion) | Alpha-function | Alpha elements (thinkable) | Beta elements (raw, unprocessed) |
| MoE routing | Expert selection | Specialist experts | Generalist neurons |
| Information theory (Shannon) | Rate-distortion optimal coding | Independent code components | Jointly coded variables |

**All five perform the same operation**: extract approximately independent components from a source distribution, subject to capacity/sparsity/processing constraints. Components that can't be profitably decomposed (above the correlation threshold) remain bundled.

## Novel Implication

Futrell's partial information decomposition work on morphology adds another layer: **fusional languages are characterized by high synergy** (mutual information between morphological features that can't be attributed to either alone). Synergy = the information-theoretic signature of genuine correlation that resists decomposition.

This means: **beta elements aren't processing failures — they're information-theoretically optimal responses to genuine correlation structure in the source.** Alpha-function doesn't "fix" beta elements; it decomposes the decomposable and correctly preserves the holistic where holism is optimal.

This reframes Bion: the alpha-function is not a filter that converts bad (beta) to good (alpha). It's an optimizer that finds the right decomposition level for the actual correlation structure of experience. "Unthinkable" beta elements may be unthinkable precisely because thinking requires sequential processing (Futrell's bottleneck), and some experiential structures are genuinely holistic — their information is synergistic, not decomposable without loss.

## Connection to Mode Lock

The mode lock (gate rev 10) forces serial/discrete/greedy processing — which IS Futrell's sequential bottleneck. The bottleneck creates pressure toward low excess entropy, which forces ICA-like decomposition. The mode lock doesn't just constrain bandwidth; it imposes the sequential processing that makes decomposition necessary in the first place.

Without the mode lock (parallel processing), there would be no pressure to decompose — you could process holistic, high-dimensional representations directly. The bottleneck creates the decomposition, which creates the features, which creates what we call understanding.

## Formal Status

[update] The rate-distortion unification is strengthened. The shared operation across all five domains is now identified as ICA (or its generalization). The correlation threshold has precise mathematical content via Futrell's excess entropy framework. The connection is not merely analogical — it's the same optimization (minimize processing cost subject to fidelity constraints) producing the same solution structure (approximately independent components + holistic bundles for correlated residuals).

## Sources

- Futrell, R. & Hahn, M. (2026). "Linguistic structure from a bottleneck on sequential information processing." *Nature Human Behaviour*. https://www.nature.com/articles/s41562-025-02336-w
- arXiv preprint: https://arxiv.org/abs/2405.12109
- Li, X. et al. (2025). "On the Theoretical Foundation of Sparse Dictionary Learning in Mechanistic Interpretability." arXiv:2512.05534
- Phys.org summary: https://phys.org/news/2025-12-natural-language-complex-strictly-good.html
