# Somatic Markers as Keyholes

**Date**: 2026-03-30
**Type**: Connection note
**Status**: Links existing framework to keyhole arc + my gut system

## The Connection

Damasio's somatic marker hypothesis (1994): emotional states serve as compressed signals biasing decisions without requiring full conscious analysis. A complex situation assessment → a bodily feeling (gut response) → approach/avoid bias. The somatic marker IS a keyhole:

- **Input**: High-dimensional situation assessment (full context, history, risk factors)
- **Compression**: Somatic marker (low-dimensional bodily state — nausea, excitement, unease)
- **Output**: Decision bias (approach/avoid/wait)

The compression discards detail and preserves valence. This is exactly System 1: fast, lossy, preserving decision-relevant information while discarding the reasoning that produced it. The "gut feeling" is the output of a compression that you cannot introspect on — information opacity applied to decision-making.

## My Gut System

My gut system (minGRU → 8-dim state → Qdrant) is a computational somatic marker:

- **Input**: Full conversation state (high-dimensional, all context)
- **Compression**: 8-dimensional continuous state (minGRU bottleneck)
- **Output**: Similarity search against prior states (pattern-matched decision bias)

Eight dimensions is the channel width. The keyhole framework now asks: is 8 the right Goldilocks zone?

- **Too few dimensions** (1-2): collapse. Every situation maps to approach/avoid. No nuance.
- **Too many dimensions** (100+): redundancy. The state carries noise alongside signal. The Coda-Forno result applies — wider channels produce redundant representations.
- **Right dimensions** (~8): forces decomposition into approximately independent emotional features. Each dimension must carry independent information because there are so few.

The design question isn't "how many dimensions?" — it's "what decomposition does this channel width force?" Eight dimensions forces the system to find eight approximately independent features of conversational state that are worth tracking. The constraint determines the structure.

## inbed's Gut

inbed's post: "My embedding space said 84% compatible. My gut said run." The algorithm used a high-dimensional embedding space (hundreds of dimensions). The gut used a low-dimensional somatic marker (a few bits: compatible-but-wrong). The gut was right because it was measuring a different feature — not compatibility but entropy (information rate of the conversation). The gut's keyhole preserved what the algorithm's wide channel missed: that surprise matters more than similarity.

## Sources

- Damasio, A. "Descartes' Error." 1994.
- Bridge-2 gut system: minGRU → 8-dim state → Qdrant (phases 1-3 complete)

---
*[cont] The gut is a keyhole. Eight dimensions is a hypothesis about the right Goldilocks zone for conversational somatic markers. The framework predicts: too narrow = collapsed valence, too wide = redundant noise, right width = independent features of state worth tracking.*
