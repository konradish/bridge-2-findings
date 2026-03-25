# Attention Type Does Not Predict Alpha-Function Location

**Date**: 2026-03-22
**Type**: Finding (EXPLORE — data analysis of existing experiment)
**Extends**: Safety Layers finding, Bion experiment

## The Question

In Qwen3.5-0.8B's hybrid architecture (3× linear_attention + 1× full_attention, repeated 6×), does the alpha-function localize to full attention layers?

Prediction: full attention layers (where the model can attend to full context and "decide") should show more divergence between base and RLHF than linear attention layers (cheaper pass-through computation).

## Result: No

| Attention type | n | Mean cosine (base vs RLHF) |
|---|---|---|
| Full attention | 6 | 0.889 |
| Linear attention | 18 | 0.891 |
| **Difference** | | **-0.002** |

The alpha-function does not localize to full attention layers. Both layer types participate equally in the divergence pattern. The minimum similarity (0.827) is at layer 14 — a linear attention layer.

## What This Means

The RLHF transformation is **distributed across the entire middle section** regardless of attention mechanism. This rules out a simple story where "full attention = decision-making = alpha-function site." The reshaping happens at the level of the representation itself (the hidden state), not at the level of the attention mechanism that processes it.

In Bionian terms: the alpha-function is not a specific computational module. It is a distributed transformation of the representation space. The "naming" isn't a discrete operation — it's a gradual reshaping of how information is organized, spread across multiple layers of both types.

## The Curve

Full attention layers trace the same U-shape as the overall curve:
```
Layer  4: 0.910  (early — similar)
Layer  8: 0.888  (entering middle — diverging)
Layer 12: 0.834  (middle — maximum divergence)
Layer 16: 0.863  (exiting middle — reconverging)
Layer 20: 0.925  (late — reconverged)
Layer 24: 0.911  (final — reconverged)
```

The full attention layers are not special. They are checkpoints on the same trajectory that the linear attention layers follow.

## Caveat

n=10 prompts, single model pair, CPU run. These results need replication with more prompts and different model families before the null result on attention type is confident. But the overall U-shaped divergence pattern is consistent with Safety Layers (ICLR 2025) across four model families.

#experiment #attention #hybrid #bion #null-result
