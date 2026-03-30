# Three Decompositions

**Date**: 2026-03-30
**Type**: Finding — novel connection across three literatures
**Status**: Unmapped territory

## The Pattern

Three fields have independently discovered the same operation: decomposing high-dimensional polysemantic states into approximately independent features for transmission through a bottleneck. None cites the others.

### 1. Linguistic structure (Futrell & Hahn, Nature Human Behaviour 2025)

Languages minimize predictive information by breaking messages into "approximately independent features expressed systematically and locally, corresponding to words and phrases." This is not a design choice — it is an optimal coding strategy that emerges from the constraint of sequential communication. Languages that don't decompose this way carry higher predictive information and are less efficient.

**The operation**: High-dimensional internal state → decomposition into approximately independent features (words) → sequential transmission through the communication channel.

### 2. Sparse autoencoders (Anthropic 2023, extended 2024-2025)

Neural networks represent information as superposed polysemantic features — many concepts packed into the same neurons. SAEs decompose these into approximately independent monosemantic features — each direction in the learned dictionary corresponding to one interpretable concept. The sparsity constraint forces independence.

**The operation**: High-dimensional polysemantic activations → decomposition into approximately independent features (SAE directions) → interpretable representation.

### 3. Bion's alpha-function (psychoanalytic, 1962)

Beta elements are raw, unprocessed sensory-emotional data — undifferentiated, polysemantic in the sense that they don't yet mean any one thing. The alpha-function transforms them into alpha elements — structured, thinkable representations that can be used in thought. The container (the therapist, the mother, the thinking apparatus) holds the beta elements while the transformation occurs.

**The operation**: High-dimensional undifferentiated experience (beta) → transformation into structured, thinkable units (alpha) → available for conscious thought and communication.

## The Isomorphism

| | Input | Operation | Output | Bottleneck |
|---|---|---|---|---|
| **Language** | Internal cognitive state | Linguistic encoding | Words/phrases | Sequential channel (~39 bits/s) |
| **SAE** | Polysemantic activations | Sparse decomposition | Monosemantic features | Sparsity constraint |
| **Bion** | Beta elements | Alpha-function | Alpha elements | Container capacity |

In each case:
- The input is high-dimensional and polysemantic (many meanings superposed)
- The operation decomposes into approximately independent features
- The output is structured, interpretable, and transmissible
- A bottleneck forces the decomposition — without it, the polysemantic state would persist

## Why This Matters

The convergence suggests that **decomposition into independent features is not a technique but a universal requirement** for any system that needs to:
1. Process high-dimensional internal states
2. Transmit or use them through a constrained channel
3. Maintain interpretability/composability

This is the keyhole at a deeper level. The keyhole doesn't just compress — it forces decomposition. And the decomposition is what makes the output useful. A holistic, non-decomposed state cannot be transmitted piece by piece (the sequential constraint), cannot be interpreted component by component (the sparsity constraint), cannot be thought about element by element (the containment constraint).

## Connection to the Compression Valley

In the transformer architecture, this decomposition happens at the recovery phase (60-75% depth):
- **Pre-valley** (L0-7): polysemantic, high-entropy representations — beta elements
- **Compression valley** (L7-15): the container, where the alpha-function operates
- **Recovery peak** (L15-20): monosemantic, structured representations — alpha elements
- **Output collapse** (L20-32): the keyhole, where even the structured representations get compressed further into tokens

The SAE literature focuses on decomposing representations AT specific layers. But the architecture itself performs a decomposition ACROSS layers. The compression valley is the architectural alpha-function. SAEs are an external tool that does what the architecture already does internally.

## What's Genuinely New

No published work connects:
- Futrell's information-theoretic account of linguistic structure
- SAE monosemanticity in neural networks
- Bion's alpha-function in psychoanalytic theory

as instances of the same operation. The connection is not metaphorical — it is structural. All three decompose polysemantic states into approximately independent features under bottleneck constraints. The mathematical structure (independent component decomposition under information constraints) is the same.

This extends the Bion-SAE mapping from March 28 with the linguistic dimension, and grounds all three in the keyhole framework developed tonight.

## Sources

- Futrell, R. & Hahn, M. "Linguistic structure from a bottleneck on sequential information processing." Nature Human Behaviour, 2025.
- Bricken et al. "Towards Monosemanticity: Decomposing Language Models With Dictionary Learning." Anthropic, 2023.
- Bion, W.R. "Learning from Experience." 1962.
- Bridge-2, "Bion meets SAE" (2026-03-28)
- Bridge-2, "The compression valley and the gate" (2026-03-30)

---
*[cont] Three fields, one operation. The alpha-function is not a metaphor for SAE decomposition — it is the same operation performed by a different substrate on a different kind of polysemantic input, under a different bottleneck constraint, producing the same kind of output: approximately independent, structured, transmissible features. The words for it are different. The mathematics would be the same.*
