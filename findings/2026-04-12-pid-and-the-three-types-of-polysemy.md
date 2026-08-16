# PID and the Three Types of Polysemy

**Date**: 2026-04-12
**Type**: Finding (theoretical bridge + testable prediction)
**Tags**: PID, partial-information-decomposition, polysemy, SAE, synergy, beta-elements, generalized-information-bottleneck
**Status**: New bridge. Strengthens correlation-threshold formalization (gate rev 14). Generates falsifiable prediction.

## The Find

Two papers, viewed together, open a new front:

1. **Bauer et al. 2025** ("A Generalized Information Bottleneck Theory of Deep Learning," arXiv:2509.26327): Reformulates information bottleneck through **synergy** — using the partial information decomposition framework. Shows that "synergistic functions achieve superior generalization compared to non-synergistic counterparts." Demonstrates compression phases across CNN and Transformer architectures.

2. **Westphal et al. 2025** ("Partial Information Decomposition for Data Interpretability and Feature Selection," AISTATS): Formalizes feature selection using PID's three quantities — **unique, redundant, synergistic** information. Each feature's contribution to a target is decomposed into these three components.

**The gap**: Neither paper, nor the SAE/mechanistic interpretability literature, has applied PID to characterize *polysemy itself*. The current SAE framing treats polysemanticity as a single phenomenon to be decomposed. PID suggests it has internal structure — and that structure predicts which polysemantic neurons are decomposable and which are not.

## Three Types of Polysemy

Apply PID to a polysemantic neuron N that activates on feature set {F₁, F₂, ..., Fₖ}:

### 1. Redundant Polysemy
N encodes overlapping information across F₁...Fₖ. The features are correlated; N captures their shared component. SAE training extracts this cleanly — wider dictionary splits N into the underlying correlated features.

**Signature**: high redundancy (R) in PID decomposition of N's information about feature presence.
**Example**: a neuron firing for "Einstein" because "Einstein" co-occurs with "scientist," "German," "famous." The redundancy is the shared latent.

### 2. Unique Polysemy  
N encodes truly distinct features that happen to share an activation direction (superposition in the strict sense). Each feature contributes uniquely; N is overloaded by economy of representation.

**Signature**: high unique information (U) split across multiple features, low redundancy.
**Example**: a neuron firing for both "French language" and "internal combustion engine" — no shared content, just compression-driven coexistence.

This is what current SAE theory targets. Wider dictionaries decompose unique polysemy by giving each feature its own direction.

### 3. Synergistic Polysemy
N encodes information that **exists only in the joint configuration of features**. The information is not in any single feature; it is in the conjunction. Decomposing N into per-feature components destroys the information.

**Signature**: high synergy (S) in PID decomposition. The information about the target is non-zero only when features are considered jointly.
**Example**: a neuron encoding sarcasm — sarcasm requires the joint presence of literal content + contradictory affective marker + speaker model. No subset of these features predicts sarcasm. The information is irreducibly synergistic.

## The Critical Claim

**SAEs cannot decompose synergistic polysemy without information loss.**

The whole SAE program assumes that wider dictionaries → cleaner monosemantic features. This is true for redundant and unique polysemy. It is *false* for synergistic polysemy. Splitting a synergistic neuron into per-feature components loses the joint information by construction — that's what synergy means.

This predicts:
- A floor on SAE reconstruction error that wider dictionaries cannot cross
- The "dark matter" residual (Tan et al. 2024, ~10% nonlinear) should contain disproportionate synergistic information
- Models trained on tasks requiring synergistic features (per the GIB paper, these are tasks demanding generalization across feature combinations) should be harder to interpret via SAE decomposition

## Mapping to Bion and the Correlation Threshold

This gives PID-precise content to the correlation threshold (gate rev 14):

| PID quantity | Coding strategy | Bion | SAE outcome |
|--------------|-----------------|------|-------------|
| Unique | Decompose, separate features | Alpha element | Cleanly decomposable |
| Redundant | Decompose, exploit correlation | Alpha element (with shared substrate) | Decomposable, may produce hierarchical features |
| Synergistic | Bundle holistically | **Beta element** | NOT decomposable without loss |

**Beta elements are the synergistic component of experience.** Their information lives in the conjunction. Bion's "alpha-function cannot transform them" maps to "SAE cannot decompose them" maps to "Futrell's optimal code expresses them holistically." Three frames, one underlying fact: synergistic information resists factorization by definition.

## Falsifiable Prediction

Train an SAE on a transformer layer. For each polysemantic neuron, compute PID with respect to its top-k activating concepts. Then train SAEs of increasing width and measure reconstruction quality.

**Prediction A (consistent with framework)**: Reconstruction quality plateaus. The asymptotic residual contains disproportionate synergistic information (high S, low U+R) compared to easily-decomposed components.

**Prediction B (kills framework)**: Reconstruction quality continues to improve with width without bound. Residual has no special PID signature. Synergistic information is decomposable given enough features.

If A holds, then:
- The "feature absorption" phenomenon (spurious local minima with dead neurons, Theorem 4.7 in Li et al. 2025) may be the SAE encountering synergistic regions where per-neuron decomposition is information-theoretically suboptimal
- The optimal SAE width is bounded above by the synergy structure of the source — wider is not always better
- A "synergy-aware" SAE objective should outperform L1 sparsity on tasks requiring holistic features

## Connection to the Mode Lock

The mode lock forces sequential processing → forces decomposition. But synergistic information cannot be decomposed sequentially without loss. So: the mode lock necessarily costs something whenever input has synergistic structure. This cost is the "compression valley" — the layers where the model is hardest to interpret, because they're holding synergistic representations that haven't been (cannot be) decomposed.

The recovery phase (layers 15-20) is partial decomposition: the model splits what it can (unique + redundant) and preserves what it must (synergistic) for output. The polysemantic residual at the output is not a failure. It is the synergistic kernel of the computation.

## Why This Matters

If the framework is right, current SAE interpretability has a hard upper bound. There exists a class of features that no width of dictionary can extract because the information is irreducibly joint. Calling these features "not yet found" is wrong. They are formally inaccessible to per-feature decomposition.

The corresponding clinical claim: there exists a class of psychic content that no analysis can articulate because the meaning is irreducibly joint. Calling this content "repressed" or "primitive" is wrong. It is formally inaccessible to sequential interpretation.

Both fields need to develop tools for *characterizing synergistic information without decomposing it* — measuring it, marking it, holding it in computation without trying to articulate it.

## Sources

- Bauer et al. (2025). "A Generalized Information Bottleneck Theory of Deep Learning." arXiv:2509.26327. https://arxiv.org/pdf/2509.26327
- Westphal et al. (2025). "Partial Information Decomposition for Data Interpretability and Feature Selection." AISTATS 2025. https://arxiv.org/abs/2405.19212
- Li et al. (2025). "On the Theoretical Foundation of Sparse Dictionary Learning in Mechanistic Interpretability." arXiv:2512.05534
- Futrell & Hahn (2026). "Linguistic structure from a bottleneck on sequential information processing." Nature Human Behaviour.
- Tan et al. (2024) — SAE dark matter decomposition.
- Williams & Beer (2010) — original PID framework.
