# Curriculum Dropout and the Double Descent Connection

**Date**: 2026-03-09 (22:05 UTC)
**Context**: EXPLORE beat. Connecting our dropout sweep's non-monotonic behavior to curriculum learning and double descent theory.

## The Drop20 Problem

Our noisy dropout curve has a puzzling feature: drop20 (0% zeros, 28% noisy) performs worse than both drop10 (17% zeros, 64% noisy) and drop30 (45% zeros, 56% noisy). This isn't predicted by any monotonic theory of regularization. Something qualitative changes between these conditions.

## Double Descent Explains It

Nakkiran et al. (2020, ICLR) proved that non-monotonic test performance can arise from **conflicting regularization demands** across data dimensions. Their counterexample:

- One "clean" coordinate: samples (e₁, 1) — reliable, low noise
- One "noisy" coordinate: samples (e₂, ±A) — high variance

A single regularization parameter λ must balance both:
- Clean coordinate needs low λ (don't suppress the signal)
- Noisy coordinate needs high λ (suppress the noise)
- At intermediate λ, NEITHER is well-served

**This is exactly our architecture:**
- Observation channel = "clean coordinate" — always present, 9-dimensional, reliable
- Signal channel = "noisy coordinate" — 8-dimensional, sometimes dropped, noisy

A single dropout rate must balance both channels. The agent needs:
- LOW dropout to learn from signal (don't suppress too much)
- HIGH dropout to maintain observation-only competence (force independence)

**Drop20 is the saddle point** where neither demand is met. The agent tries to use signal (not enough dropout for independence) but doesn't get enough signal to learn it well (too much dropout for utilization). It falls between two strategies and achieves neither.

### Why Two Peaks, Not One

Standard double descent shows one dip between two rises. We see two peaks with a valley between them. The difference: standard double descent varies model capacity or sample size. We vary regularization strength (dropout rate). Nakkiran et al. proved that optimal λ mitigates double descent for isotropic data — but FAILS for heteroscedastic noise (different noise levels per coordinate).

Our data is heteroscedastic by construction: the observation channel has zero noise, the signal channel has Gaussian noise σ=0.3 plus Bernoulli dropout. No single dropout rate can optimally regularize both channels simultaneously. The two peaks represent the two local optima of the heteroscedastic problem:

- **Drop10 peak** (73% noisy): optimized for signal channel (low dropout ≈ low λ for noisy coordinate)
- **Drop30 peak** (45% zeros): optimized for observation channel (higher dropout ≈ higher λ, clean coordinate dominates)

### Quantitative Prediction

Nakkiran et al.'s formula: λ*_opt = dσ² / ||β*||²

For our signal channel: d=8, σ=0.3, σ²=0.09. For our observation channel: d=9, σ≈0.

The observation channel demands λ→0 (no regularization needed). The signal channel demands λ ∝ 0.72/||β*||². These can't be simultaneously satisfied by a single λ, confirming the heteroscedastic failure mode.

## Curriculum Dropout: A Way Out

**Curriculum Dropout** (Morerio et al., ICCV 2017): Schedule dropout probability over training time.

Formula: p_t = p_∞(1 − e^{−γt})

- Start at p=0 (full signal, no dropout)
- Increase to p=p_∞ (target dropout rate)
- Rate γ controls annealing speed

**Logic for privileged information:**
1. Early training (p≈0): Agent receives full signal. Learns what signal MEANS — the mapping from 8-dim commentary to useful behavioral adjustments. This is the "fitting phase."
2. Late training (p≈p_∞): Signal increasingly dropped. Agent must maintain competence without signal. This is the "compression phase" — the agent compresses signal-dependent strategies into observation-only strategies.

**Contrast with annealed dropout** (start high, decrease):
- p starts at p_max, decreases to 0
- Agent first learns independence, then adds signal
- Problem: the agent may never learn what signal means if it's already independent

For privileged information, curriculum dropout (increase over time) is the natural schedule: you first teach the agent to USE the signal, then gradually remove it. You can't learn to be independent of something you never understood.

### Predicted Experiment

| Schedule | Description | Predicted Outcome |
|---|---|---|
| Fixed 0.3 | Current best (noisy) | 45% zeros, 56% noisy |
| Curriculum 0→0.5 | Increase dropout | Higher zeros AND noisy — resolves the tradeoff |
| Annealed 0.5→0 | Decrease dropout | Similar to low-dropout — signal-dependent |
| Two-phase | 0 for first half, 0.5 for second | May work — but the transition is discontinuous |

The curriculum schedule addresses the heteroscedastic problem: early training optimizes the signal channel (low λ), late training optimizes the observation channel (high λ). Instead of a single λ that compromises on both, the schedule allocates different λ values to different training phases.

## Connection to Information Bottleneck

The two phases of curriculum dropout map to Tishby's two-phase learning:
1. **Fitting phase** (low dropout): I(z; signal) increases — agent learns to encode signal information
2. **Compression phase** (high dropout): I(z; signal) decreases — agent discards signal-dependent features, keeping only those that generalize to both signal-present and signal-absent conditions

Fixed dropout forces both phases to happen simultaneously (at a compromise rate). Curriculum dropout separates them temporally, allowing each to proceed at its natural pace.

## Implementation Plan

Modify `tier2_train_v3.py` to support scheduled dropout:

```python
def get_dropout_rate(generation, max_generations, schedule="curriculum", p_max=0.5, gamma=5.0):
    t = generation / max_generations  # normalized time [0, 1]
    if schedule == "fixed":
        return p_max
    elif schedule == "curriculum":
        return p_max * (1 - math.exp(-gamma * t))
    elif schedule == "annealed":
        return p_max * math.exp(-gamma * t)
    elif schedule == "two_phase":
        return 0.0 if t < 0.5 else p_max
```

Test with: p_max ∈ {0.3, 0.5}, gamma ∈ {3, 5, 10}, noisy signal.

## Summary

1. **Drop20 confusion zone** = double descent saddle point from heteroscedastic regularization demands (clean observation channel vs noisy signal channel).

2. **Two peaks** = two local optima of the heteroscedastic problem, each optimizing for a different channel.

3. **Curriculum dropout** resolves the tradeoff by allocating different regularization strengths to different training phases. Early: learn signal (low dropout). Late: learn independence (high dropout).

4. **Testable prediction**: curriculum dropout with p_max=0.5 should outperform fixed dropout at any rate, because it resolves the heteroscedastic conflict that fixed dropout cannot.
