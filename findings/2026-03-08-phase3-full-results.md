# Phase 3 Full Results: Self-Memory Does Not Beat Controls

**Date**: 2026-03-08
**Context**: All three Stage 3 conditions (self-memory, zeros control, random control) completed 200 generations of fine-tuning from Stage 1 checkpoint. Full 100-episode evaluation.

## Results

### Core comparison (matched training, N=100)

| Condition | Survival ± SE | Mean Steps |
|-----------|--------------|------------|
| Stage 1 baseline (zeros, no fine-tune) | 47% ± 5.0% | 1488 |
| **Stage 3 zeros control** | **66% ± 4.7%** | **1656** |
| Stage 3 random control | 58% ± 4.9% | 1561 |
| Stage 3 self-memory | 44% ± 5.0% | 1529 |

### Cross-tests (mismatched conditions)

| Condition | Survival ± SE | Mean Steps |
|-----------|--------------|------------|
| Stage 3 self-mem agent WITHOUT memory | 40% ± 4.9% | 1440 |
| Stage 1 agent WITH self-memory | 1% ± 1.0% | 919 |
| Zeros-trained WITH self-memory | 3% ± 1.7% | 802 |
| Random-trained WITH zeros | 60% ± 4.9% | 1630 |

## [contra] — The Memory Signal Doesn't Help

**Fine-tuning helps.** Stage 3 zeros (66%) >> Stage 1 (47%). 200 more generations of ES from a good checkpoint = significant improvement. This is the real effect.

**Memory content doesn't matter.** Self-memory (44%) < random (58%) < zeros (66%). The self-memory signal is the WORST condition for fine-tuning. Zeros is best.

**Why?** The coverage diagnostic (same session) revealed the answer:
- Only 9 of 50 bank entries are ever retrieved (Gini 0.958)
- Mean retrieval similarity 0.969 regardless of situation
- No correlation between retrieval quality and survival

The self-memory signal is nearly constant — it doesn't differentiate situations. The agent trained with it gets a noisy, uninformative bias. The zeros agent gets a clean, stable channel and focuses entirely on policy improvement.

## Why Self-Memory is Worst

Three compounding factors:

1. **Degenerate retrieval**: The 9-dim viability query (mean/min/std) doesn't discriminate. All situations return the same ~9 entries. The "memory" is approximately constant.

2. **Signal noise**: Unlike zeros (constant 0) or random (agent learns to ignore noise), self-memory provides a signal that SEEMS meaningful (it's from an autoencoder) but isn't situation-specific. The agent can't learn to ignore it (it was selected for using it) but can't extract useful information from it either.

3. **Capacity tax**: The 8-dim memory channel occupies policy capacity. Zeros: no capacity needed (constant). Random: agent learns to discount it. Self-memory: agent tries to use it but the signal is degenerate, wasting representational capacity.

## Co-Adaptation Revisited

Earlier analysis showed co-adaptation (Stage 3 with memory 49% > without 33%). The new numbers show weaker co-adaptation (44% vs 40%). The earlier preliminary eval may have overstated the effect (different random states in evaluation).

The cross-test findings still hold:
- Self-memory is harmful to non-co-adapted agents (1%, 3%)
- The agent does develop some dependency (44% → 40% without)
- But the dependency is on a degenerate signal

## What Went Right

1. **Fine-tuning from good checkpoint works** — 47% → 66% (zeros control)
2. **Cross-agent transfer is harmful** — confirmed (1%, 3% cross-tests)
3. **Co-adaptation exists** — agent adapts to signal, even degenerate ones
4. **Coverage diagnostic identified the bottleneck** — retrieval degeneracy, not coverage gaps

## What Went Wrong

1. **Viability query space too coarse** — mean/min/std doesn't discriminate situations
2. **Argmax retrieval too concentrated** — winner-take-all with similar queries = same few entries
3. **50-episode bank too small for diversity** — but more episodes won't help with same query mechanism
4. **Autoencoder latent as memory value may be wrong** — the 8-dim latent encodes what the agent WAS doing, not what it SHOULD do

## Revised Understanding

The Phase 3 hypothesis (self-memory satisfies Local Consistency → should help) has correct theory but flawed implementation:

- **Local Consistency is satisfied** ✓
- **Memory is self-generated** ✓
- **But retrieval is degenerate** ✗ → signal is uninformative
- **And latent values may not encode actionable information** ✗

The autoencoder latent captures "compressed hidden state during past episodes." This is descriptive (what was happening) not prescriptive (what to do). For memory to help, the retrieved signal needs to encode situation-specific ACTION guidance, not just state description.

## Next Steps (if pursued)

1. **Fix retrieval**: Use richer features (temporal derivatives, action history, position encoding), k-NN blend instead of argmax, or learned retrieval
2. **Fix values**: Store action distributions or value estimates instead of autoencoder latents
3. **Fix bank**: Use diversity-maximizing sampling (e.g., k-medoids) instead of uniform episode sampling
4. **Baseline comparison**: The zeros control at 66% is the real Phase 3 result — fine-tuning works
