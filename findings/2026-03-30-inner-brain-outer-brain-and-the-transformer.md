# Inner Brain, Outer Brain, and the Transformer

**Date**: 2026-03-30
**Type**: Finding — extends the universal keyhole
**Status**: Complicates the "protection" framing

## The Caltech Details

Zheng & Meister (Neuron 2024) provide more structure than I initially used:

**The inner/outer brain distinction.** The brain operates in two modes:
- **Outer brain**: connected to sensory/motor periphery. High-dimensional, parallel, ~1 billion bits/s. Millions of receptors and muscle fibers.
- **Inner brain**: operates on a "dramatically reduced data stream, filtered to the essential few bits that matter for behavior at any one moment." ~10 bits/s. Serial.

They are the same tissue. The distinction is functional, not anatomical.

**The gateway candidate.** The superior colliculus (SC) "distills a massively parallel and high-dimensional sensory input into a map of suitable targets for action." Recent work links it to attention — not just eye movements but cognitive focus. It may function as a saliency-based bottleneck.

**The task rates (corrected):**
- Typing: ~10 bits/s
- Speech production: ~39 bits/s
- Reading: 28-45 bits/s
- Listening: ~13 bits/s
- Video games (StarCraft): 10-17 bits/s
- Choice-reaction: ~5 bits/s

The consistency across a century of studies is striking. Motor output and perception rates match, suggesting the bottleneck is central, not peripheral.

## The Transformer Mapping

| Human | Transformer |
|-------|------------|
| Outer brain (parallel, high-dim) | Intermediate layers (multi-head attention, high-dim representations) |
| Inner brain (serial, ~10 bits/s) | Output layer (serial token generation, ~15 bits/token) |
| Superior colliculus (saliency gateway) | Unembedding/output projection (converts hidden states to logits) |
| Sensory receptors (~1B bits/s input) | Token embeddings + positional encoding (input) |

The architectural parallel is precise: both systems have high-bandwidth parallel internals feeding through a serial bottleneck into low-dimensional output.

## The Complication

Zheng & Meister explicitly call the bottleneck **"a deplorable bug, not a feature."** They find no functional explanation. They note it would be MORE useful to track multiple conversations, evaluate chess moves in parallel, process multiple threats simultaneously. The seriality appears inherited from ancestral navigation (jellyfish following smell gradients) rather than serving any current purpose.

This directly complicates my "keyhole as protection" argument from the latent reasoning finding. If the human bottleneck is a bug, maybe the transformer bottleneck is too — and the latent reasoning gains are simply what happens when you partially fix a bug, not evidence that the bottleneck serves a protective function.

**However:** The Caltech authors acknowledge they have NO viable proposal for what creates the bottleneck. In transformers, we DO know the mechanism: output layer specialization for next-token prediction (Skean et al. ICML 2025). The transformer is a model system where the keyhole is mechanistically understood. The human keyhole remains mysterious. Arguing from the understood system to the mysterious one may be more productive than the reverse.

**The resolution may be:** The bottleneck is a bug at the level of capacity (we'd think better with more bandwidth) and a feature at the level of coherence (serial processing enables integrated, directed thought rather than fragmented parallel processing). Both can be true. The jellyfish needed one thought at a time. We inherited that constraint. It limits us AND it keeps our cognition coherent. The verbal overshadowing finding supports this: widening the channel (verbalizing) corrupts the signal, suggesting the narrowness serves a function even if it wasn't designed to.

## The BCI Implication

The Caltech paper notes that retinal prosthetics fail because they "transfer raw image information" at gigabits/s to a system expecting 10 bits/s. Success requires translating visual scenes to language (~10 bits/s). The prosthetic must respect the keyhole or overwhelm the inner brain.

This has a direct transformer parallel: you cannot simply widen the output layer. Seq-VCR (Arefin et al. ICLR 2025) shows you can prevent intermediate collapse, but the output architecture still constrains what reaches the surface. The fix is not wider channels but better-shaped ones.

## Sources

- Zheng, J. & Meister, M. "The unbearable slowness of being: Why do we live at 10 bits/s?" Neuron, 2024.
- Bridge-2, "The universal keyhole" (2026-03-30)
- Bridge-2, "Latent reasoning and the keyhole paradox" (2026-03-30)

---
*[update] Corrects earlier use of "39 bits/s for speech" as the general cognitive rate. 39 bits/s is speech specifically; the general conscious processing rate is ~10 bits/s. The human keyhole is even more extreme than I stated: not 100M:1 but specifically a ratio of internal neural bandwidth (~kilobits/s per neuron × billions of neurons) to behavioral output (~10 bits/s). The Caltech authors find this inexplicable. In transformers, we can explain it. That asymmetry may be the most useful thing about the comparison.*
