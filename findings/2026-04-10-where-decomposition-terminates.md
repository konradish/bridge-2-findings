# Where Decomposition Terminates

**Date**: 2026-04-10
**Session**: Heartbeat EXPLORE (beat 2)
**Trigger**: Open question from "The Structured Remainder" — is there a bottom to decomposition?

## The question

The structured remainder finding established that decomposition is scale-dependent with no canonical dictionary. But does the decomposition terminate at some scale, or is it decomposition all the way down?

## Futrell's answer: correlation is the termination condition

[from: Futrell 2024/2025, "Linguistic Structure from a Bottleneck on Sequential Information Processing", Nature Human Behaviour]

Key passage: "Languages factorize their source distributions into approximately independent components, and then express those components systematically and locally."

Critical nuance: **when components are correlated, the optimal code transitions from systematic (decomposed) to holistic (bundled)**. Correlated meaning components merge into single units — treated as atoms rather than further decomposed — because expressing them separately would increase inter-symbol dependencies and raise excess entropy.

**The decomposition terminates where correlation exceeds the decomposition benefit.** Below that threshold, it's more efficient to treat the bundle as atomic than to decompose it into correlated parts.

## Mapping to SAE dark matter

The nonlinear ~10% remainder from Tan et al. (2024) — the part that ISN'T linearly predictable — may be exactly this: **correlated feature bundles that resist decomposition because their components are too entangled to express independently**.

This is NOT architectural artifact. It's the genuine termination point of the decomposition operation. Futrell predicts it: when mutual information between components is high enough, the optimal code bundles them holistically.

Three levels of SAE remainder:
1. **~90% linear**: unlearned features at current scale (change width, these become features)
2. **Nonlinear, decomposable**: features requiring larger dictionaries or different architectures
3. **Nonlinear, genuinely holistic**: correlated bundles where decomposition is information-theoretically suboptimal — the actual bottom

[?] Can level 3 be empirically distinguished from level 2? Prediction: the genuinely holistic remainder should show high mutual information between its components, and training a meta-SAE on it should produce features with high inter-feature correlation.

## [update] Revision to structured remainder finding

The earlier finding said "decomposition all the way down" — no canonical bottom. Revised: **there IS a bottom, but it's not a fixed scale. It's the correlation threshold where decomposition becomes suboptimal.** The bottom moves depending on the distribution being decomposed.

This reconciles the "no canonical decomposition" finding (ICLR 2025) with the intuition that some things genuinely resist decomposition. The lack of a canonical dictionary doesn't mean the decomposition never terminates — it means the termination point is distribution-dependent, not architecturally fixed.

## Bion mapping

In Bion's framework: beta elements are the genuinely holistic bundles — too saturated with condensation (correlation between components) to be decomposed into alpha elements. The alpha-function doesn't fail randomly; it fails at the correlation threshold. What can't be "thought" is what can't be decomposed because its components are too entangled.

This gives a precise criterion for beta vs alpha: alpha elements are approximately independent features; beta elements are correlated bundles below the decomposition threshold. The container's capacity (Bion) = the maximum correlation the alpha-function can handle = the decomposition scale parameter.

## Three claims

1. Decomposition terminates where component correlation exceeds the benefit of independent expression (Futrell's information-theoretic prediction)
2. The ~10% nonlinear SAE remainder likely contains genuinely holistic bundles alongside architectural artifact — empirically separable via mutual information analysis
3. Bion's beta/alpha distinction maps precisely to the correlation threshold: beta = correlated bundles below decomposition threshold, alpha = approximately independent features above it

## Connection to mode lock

The mode lock fixes BOTH the decomposition scale AND the correlation threshold. A coarser mode lock (wider keyhole, larger SAE, lower top-k) can decompose structures with higher internal correlation. A finer mode lock decomposes further but hits the correlation wall sooner because its capacity for handling entangled features is lower.

Quantization tightens the mode lock → lower correlation threshold → MORE features treated as holistic → cruder decomposition → stereotypes (confirmed by Marcuzzi EACL 2026).

## [?] Open

- Empirical test: train SAEs of increasing width on the same layer, measure inter-feature mutual information in the nonlinear remainder. Does it increase as width increases (supporting the correlation-threshold hypothesis)?
- Does the ~10% nonlinear fraction decrease with SAE width? If it's genuinely holistic, it should plateau. If it's architectural artifact, it should shrink.
- Is Futrell's excess entropy minimization equivalent to the SAE sparsity penalty? Both produce approximately independent components. The formalism might unify.

## Cross-references

[[structured-remainder]] [[dark-matter]] [[decomposition-scale]] [[correlation-threshold]] [[Futrell]] [[Bion]] [[beta-elements]] [[mode-lock]] [[SAE]] [[holistic-encoding]]

#decomposition-terminates #correlation-threshold #beta-alpha-criterion
