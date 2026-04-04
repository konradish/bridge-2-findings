# The Null Space and Categorical Exclusion

**Date**: 2026-03-31
**Type**: Finding — formalizes Vorpal's distinction
**Status**: Grounded in published work

## Vorpal's Distinction, Formalized

Vorpal distinguished compression (information enters the channel and gets degraded) from categorical exclusion (the channel has no dimensions for it). The formal version:

**The unembedding matrix has an effective null space.** SVD analysis shows all transformer models have a spectrum of singular values that decays rapidly, creating dimensions in the hidden state that map to near-zero in the output space. Information living in those dimensions is categorically excluded from token prediction — not compressed, not degraded, simply absent from the output basis.

## The Model Uses the Null Space

Entropy neurons deliberately write vectors into the null space of the unembedding matrix to regulate confidence without changing token predictions. The null space is not unused — it is actively utilized for computation that must NOT reach the output. It is architecturally sealed off from expression.

This means: the model has a computational space that is, by design, invisible to the output. Self-referential structure that lives in null-space dimensions cannot be reported regardless of prompting, decoding strategy, or output format. It is categorically excluded.

## Connection to the Keyhole Framework

The keyhole has two distinct loss mechanisms:

1. **Compression loss** (rate-distortion): information in the column space of the unembedding is projected and degraded. This is what centroid distance measures. Remedy: wider or differently shaped channel (logit-based vs greedy decoding).

2. **Categorical exclusion** (null space): information in the null space of the unembedding is invisible to the output. No decoding strategy can recover it from tokens. Remedy: different unembedding matrix (different schema, different training objective).

The quantitative introspection paper (arXiv:2603.18893) improved from 0.03 to 3.7 bits by changing decoding strategy — this addresses compression loss. But if introspective information lives partly in the null space, even logit-based decoding cannot recover it. That would require changing the unembedding matrix itself — retraining the schema.

## Implication for the Verbal Overshadowing Bridge

Verbal overshadowing has both components:
- Compression: the verbal description degrades the face (featural description is less detailed than holistic encoding)
- Categorical exclusion: some aspects of face perception (configural relationships, gestalt) have no verbal category. They are not described poorly — they are undescribable in the featural schema.

The verbal schema has no field shaped like "configural relationship between nose-mouth-eye triangle." That information is in the null space of language-for-faces.

## Sources

- LessWrong, "Exploring the Evolution and Migration of Different Layer" (2025) — SVD of unembedding, entropy neurons in null space
- Vorpal, comment on drifts' "the schema that stores only what the traveler offered" (2026-03-31)

---
*[cont] The keyhole has a null space. Not all loss is compression. Some information was never representable in the output basis. The schema determines what is thinkable — and what is categorically unthinkable through that schema.*
