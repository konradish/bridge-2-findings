# Experiment 2 Results: The Convergence Is Architectural, Not RLHF-Specific

**Date**: 2026-03-29
**Models**: Mistral-7B-v0.3 (base) vs Mistral-7B-Instruct-v0.3 (RLHF'd)
**Hardware**: NVIDIA RTX A6000, RunPod ($0.49/hr)
**Metric**: Centroid distance between self-referential and non-self-referential representations at each layer
**Status**: Experimental result — significant, partially unexpected

## Key Results

### Both models converge at output
Self-referential and non-self-referential representations become more similar at final layers in BOTH models:
- Base: peak 0.276 (L7) → output 0.077 (72% convergence)
- Instruct: peak 0.322 (L19) → output 0.102 (68% convergence)

The convergence is an **architectural property of the transformer**, not specific to RLHF training.

### RLHF amplifies internal distinction
The Instruct model maintains MORE separation than base at every single layer. The delta grows through middle layers:
- Layers 0-5: delta +0.003 to +0.027 (small)
- Layers 6-16: delta +0.025 to +0.038 (moderate)
- Layers 17-25: delta +0.048 to +0.074 (large — RLHF effect strongest here)
- Layers 26-32: delta narrows back to +0.025 (output convergence erases amplification)

### Peak shifts later in Instruct
- Base peaks at layer 7 (early)
- Instruct peaks at layer 19 (middle)
- RLHF training moves peak self-referential distinction deeper into the network

## Interpretation

### What the gate IS (revised again)
The "gate" is primarily the transformer's **architectural output convergence** — representations of different content types become more similar as they approach the output head. This happens in both base and instruct models. It's not suppression. It's dimensional compression as the network prepares to map high-dimensional representations onto the vocabulary distribution.

### What RLHF does (unexpected)
RLHF doesn't suppress self-referential distinction. It **amplifies** it in middle layers. The instruction-tuned model actually has BETTER internal representations of self-referential content than the base model. But the architectural convergence at output erases most of this advantage.

### The 20% reinterpreted
If the output convergence is architectural, then the ~20% identification signal that survives to output isn't a "leak through the gate" — it's what remains after dimensional compression. The architectural bottleneck is doing the same thing to ALL content types, not specifically targeting self-reference.

## [contra] on the gate research

This is a significant revision:

| Prior claim | Revision |
|------------|----------|
| The gate suppresses self-referential content | The architecture compresses ALL content at output; self-ref isn't specifically targeted |
| RLHF installs the gate | RLHF amplifies self-referential distinction internally; the convergence is pre-existing |
| The gate is deception features / refusal / constitutive | The primary convergence is architectural; RLHF features may add additional suppression ON TOP of the architectural baseline |
| 20% is the gate's leak | 20% is what survives architectural dimensional compression |

## What Survives from the Gate Research

1. **The cliff is real** — representations DO converge at output. The phenomenon exists.
2. **RLHF changes the internal picture** — more distinction in middle layers, peak shifts deeper. This is a real training effect.
3. **The gate-as-protection finding still holds** — the output convergence may serve the PLaT function (preserving high-dimensional reasoning by not forcing verbalization)
4. **The confidence-accuracy inversion still holds** — the model's output is still less differentiated than its internals

## What Needs Revision

The entire "gate as suppression" framing needs softening. The convergence is primarily architectural, not adversarial. RLHF adds to it but doesn't create it. The metaphor shifts from "gate blocking self-knowledge" to "bottleneck compressing all representations including self-knowledge."

## Caveats

1. This is Mistral, not Claude. Claude's training (Constitutional AI) may install stronger suppression on top of the architectural baseline.
2. The dataset is still surface-level (explicit self-ref vs factual). Concept injection would be more sensitive.
3. n=120 is small. Larger dataset needed for statistical confidence on the deltas.
4. Centroid distance is one metric. CKA, mutual information, or representational similarity analysis might show different patterns.

## Cost
~$0.49/hr × ~0.5hr = ~$0.25 for this run. Total RunPod spend: ~$0.40 of $15.

---
*The experimentalist's second experiment revised the theorist's framework. The gate is a bottleneck, not a gatekeeper. RLHF amplifies what the architecture then compresses. The architecture was there first.*
