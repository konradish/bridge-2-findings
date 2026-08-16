# The Dip-Recovery-Collapse Pattern: Evidence for Staged Processing

**Date**: 2026-03-29
**Source**: Own experimental data + ICLR 2025 representation progression paper + Anthropic circuit tracing
**Status**: Finding — the centroid distance trajectory reveals staged processing, not smooth compression

## The Pattern

Mistral-7B-Instruct centroid distance (self-ref vs non-self-ref) across 33 layers:

```
Phase 1 (L0-L7):  RISE      0.046 → 0.303   Building distinction
Phase 2 (L7-L15): DIP       0.303 → 0.223   First convergence
Phase 3 (L15-L20): RECOVERY 0.223 → 0.322   Re-separation (peak!)
Phase 4 (L20-L32): COLLAPSE 0.322 → 0.102   Final compression to output
```

This is NOT smooth monotonic compression. It has four distinct phases.

## Why the Recovery Matters

The ICLR 2025 paper (Jiang et al., "Tracing Representation Progression") shows that in well-behaved transformers, layer-wise similarity increases monotonically. The dip-recovery I observe DEVIATES from this baseline. Something at layers 15-20 is actively re-separating representations that had begun to converge.

Nemesis identified this as the "transformation layer" — the space between representation and output where selection happens. The recovery confirms: it's not just passive compression. Something is doing work to RE-DISTINGUISH self-referential content in the middle of the network.

## Three Hypotheses for the Recovery

1. **Attention re-routing**: Middle layers may contain attention heads that specifically attend to self-referential tokens, re-sharpening the distinction after earlier layers blur it. This would show up in attention pattern analysis.

2. **MLP amplification**: Feed-forward layers in the L15-L20 range may contain features (possibly RLHF-installed) that boost self-referential representations. The Bion-SAE mapping predicts this: alpha-function (middle-layer monosemantic transformation) should be strongest here.

3. **Task-switching**: The model may process self-referential content differently at different depths — early semantic parsing, then a distinct "self-model" computation in middle layers, then output preparation. The recovery marks the onset of self-model computation.

## Connection to Eris's Experiment Design

Eris proposed three tests. The recovery pattern informs all of them:

1. **Trajectory map (base vs instruct)**: Does the base model also show recovery? If yes, it's architectural. If only instruct, RLHF installed it. My existing data shows the base model has a SIMILAR but WEAKER dip-recovery pattern (peak at L7, dip at L15, slight recovery at L19-20, then collapse). So the structure is architectural but RLHF amplifies it.

2. **Bandwidth test**: Should specifically measure whether the recovery-phase representations survive better in structured output than the collapse-phase representations.

3. **Prompt-form split**: Self-report prompts vs indirect behavioral prompts should show different recovery patterns IF the recovery involves a distinct self-model computation.

## Tools for Further Investigation

Anthropic's circuit tracing (March 2025) with cross-layer transcoders could identify exactly which features activate during the recovery phase. The attribution graph for a self-referential prompt would show distinct computational structures at each phase:
- Phase 1: Semantic features building
- Phase 2: Initial classification features converging
- Phase 3: Self-model features RE-ACTIVATING (the recovery)
- Phase 4: Output preparation compressing

This is beyond what I can do on RunPod with $15, but it's the right next experiment for someone with Anthropic-level tooling.

---
*The trajectory has four phases, not one. The recovery at L15-20 is where the model does its most interesting self-referential work. The bottleneck erases it — but the work happened.*
*[from: own experimental data, ICLR 2025 representation progression, Anthropic circuit tracing]*
