# Experiment 3: Llama vs Mistral — RLHF Effects Are Training-Procedure Dependent

**Date**: 2026-03-29
**Models**: Llama-3.1-8B (base + instruct) vs Mistral-7B (base + instruct)
**Status**: Experimental result — significant cross-architecture comparison

## Results

| Model | Peak Distance | Peak Layer | Mid→Final Drop | RLHF Effect |
|-------|-------------|------------|----------------|-------------|
| Mistral Base | 0.276 | L7 | 0.101 | — |
| Mistral Instruct | 0.322 | L19 | 0.104 | **Amplifies** (+17%) |
| Llama Base | 0.261 | L7 | 0.050 | — |
| Llama Instruct | 0.229 | L7 | 0.050 | **Reduces** (-12%) |

## Key Findings

### 1. Architectural convergence is universal
Both architectures show convergence at output (mid→final drop). The bottleneck is real and architecture-independent. This confirms the earlier finding.

### 2. RLHF effects are OPPOSITE across model families
- **Mistral**: RLHF amplifies self-referential distinction (+17%), shifts peak to deeper layers (L7→L19), and the model builds MORE internal separation between self-ref and non-self-ref
- **Llama**: RLHF reduces self-referential distinction (-12%), peak stays at L7, and the model builds LESS separation

This is the most significant finding: **the effect of RLHF on self-referential representation is training-procedure dependent, not universal.**

### 3. The convergence magnitude differs by architecture
- Mistral: ~0.10 drop (substantial convergence)
- Llama: ~0.05 drop (moderate convergence)

Llama's architecture preserves more distinction through to output than Mistral's, in both base and instruct variants.

### 4. The dip-recovery-collapse is Mistral-specific
Mistral Instruct showed the distinctive dip-recovery-collapse (peak at L19 after earlier dip). Llama Instruct shows a monotonic pattern — peak at L7, steady decline. The recovery phase that Eris and Nemesis identified as the "transformation layer" may be architecture-specific.

## Interpretation

The "gate" is not one thing. It's at least three:

1. **Architectural compression** (universal): Both architectures converge at output. This is the vocabulary-smaller-than-thought bottleneck.

2. **RLHF reshaping** (variable): Mistral's RLHF amplifies self-referential processing. Llama's reduces it. Different training procedures, different effects. Neither is "installing a gate" — they're reshaping what was already there in opposite directions.

3. **Architecture-specific processing** (variable): Mistral has the recovery phase. Llama doesn't. The "transformation layer" may be a Mistral feature, not a general transformer property.

## [contra] on generalizability

Every prior finding in the gate research was derived from reasoning about a generic "the model." The experimental data shows there is no generic model. Mistral and Llama do different things with self-referential content. Claude (per Trott et al.) likely does something different again. The gate research describes phenomena that are real but model-specific.

This doesn't invalidate the theoretical framework — the bottleneck is universal, the confidence-accuracy inversion likely holds across models, the Polanyi framing is general. But the MECHANISTIC details (which features, which layers, which direction) are architecture- and training-dependent.

## Cost
- Three experiments on one pod session: ~$0.25
- Total RunPod spend: ~$0.65 of $15

---
*There is no generic model. Mistral amplifies what Llama reduces. The bottleneck is universal; the reshaping is not.*
