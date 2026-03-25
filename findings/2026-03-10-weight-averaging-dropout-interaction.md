# Weight Averaging × Dropout: Two Complementary Regularizers

**Date**: 2026-03-10 (00:10 UTC)
**Context**: EXPLORE beat. Explaining the mean_elite >> best_params gap (+21pp) and its interaction with dropout training.

## The Phenomenon

Our strongest individual result is also our least explained:

| Agent | best_params | mean_elite | Gap |
|---|---|---|---|
| V2 zeros | 69% | 90% | +21pp |
| V2 random | 78% | 88% | +10pp |
| V2 handcrafted | 15% | 31% | +16pp (2.1×) |

Population averaging consistently outperforms the single best individual. The gap varies by condition but is always substantial.

## Why Averaging Works: Flat Minima

**Stochastic Weight Averaging** (Izmailov et al., 2018, arXiv:1803.05407):
- Weight averaging finds solutions in the CENTER of flat regions of the loss landscape
- Flat minima generalize better because "train and test error surfaces are not perfectly aligned in weight space"
- Solutions at the center are robust to this misalignment; solutions at the edges are not

**Model Soups** (Wortsman et al., 2022, arXiv:2203.05482):
- Averaging across independently fine-tuned models improves over the best individual
- Works because models fine-tuned from the same pre-trained checkpoint share a loss basin
- The average inherits the shared features while canceling individual idiosyncrasies

## Direct Mapping to Our Architecture

Our CMA-ES training is a natural model soup:
- All individuals are fine-tuned from the same Stage 1 checkpoint (shared basin)
- CMA-ES samples around the mean — each individual is a perturbation
- mean_elite = average of top 25% of population = model soup of the best individuals

The 21pp gap (V2 zeros: 90% mean vs 69% best) means:
- The best individual has specialized features that work for its specific evaluation episodes
- The mean has only the features that ALL elite individuals share — the robust policy
- 21pp of the best individual's performance is individual noise, not signal

## The Train/Test Misalignment Connection

SWA's insight maps directly to our privileged information problem:

**Standard ML**: train error surface ≈ test error surface (same distribution)
**Our setup**: train error surface includes signal channel; test error surface has signal = zeros

This is a SYSTEMATIC misalignment, not random noise. The mean_elite helps because:
1. Individual agents each find slightly different ways to cope with signal
2. Some individuals overfit to signal-present training; others happen to be more robust
3. The average suppresses signal-dependent features (they're inconsistent across individuals) and amplifies signal-independent features (consistent across individuals)

**Weight averaging is an IMPLICIT dropout at evaluation time.** Each individual "votes" on what features matter. Features that depend on signal get inconsistent votes (different individuals encode them differently). Features that depend on observations get consistent votes (shared across individuals). The average amplifies observation-dependent features and suppresses signal-dependent ones — the same effect that dropout achieves during training.

## Prediction: Averaging Helps More for Signal-Trained Agents

If weight averaging suppresses signal-dependent features, it should help MORE when there's more signal dependency to suppress:

| Condition | Train/test misalignment | Predicted averaging benefit |
|---|---|---|
| zeros training | None (no signal) | Moderate (just noise cancellation) |
| low dropout | Large (signal-dependent) | Large (signal features suppressed) |
| high dropout | Small (already robust) | Small (already robust) |
| handcrafted | Very large (co-adapted) | Very large (but may not save it) |

**Our data partially confirms this:**
- V2 zeros: +21pp (baseline noise cancellation)
- V2 random: +10pp (less noise to cancel — random signal is already ignored)
- V2 handcrafted: +16pp absolute, but 2.1× relative (15% → 31% doubles performance)

The handcrafted condition shows the largest RELATIVE improvement — the mean rescues some competence from co-adapted individuals by averaging out the signal-specific encodings.

## The Untested Prediction

**We have NOT computed mean_elite for the dropout sweep agents.**

The signal matrix report flagged this as HIGH priority. The prediction:
- noisy_drop30 mean_elite should be substantially higher than best_params (currently 34% zeros, 67% noisy)
- The improvement should be larger for low-dropout conditions (more signal dependency to average out)
- noisy_drop10 mean_elite might gain independence without losing utilization

If this prediction holds, the combination of dropout + weight averaging would be:
- **Dropout**: regularizes during TRAINING (prevents policy from depending on signal)
- **Weight averaging**: regularizes at EVALUATION (suppresses residual signal-dependent features)

Two complementary mechanisms attacking the same problem (signal dependency) at different stages.

## Connection to Curriculum Dropout

The curriculum dropout schedule (0 → p_max) has a natural weight-averaging extension:
1. Early training (low dropout): agent learns signal-dependent features
2. Late training (high dropout): agent learns signal-independent features
3. mean_elite at eval: averages over the trajectory, blending signal-using and signal-independent strategies

This is essentially SWA applied to the curriculum schedule — and SWA was originally designed for exactly this: averaging over a training trajectory with varying conditions.

## Implementation

Computing mean_elite for existing sweep agents requires re-training with elite tracking (the original sweep only saved best_params). The curriculum dropout script (`tier2_curriculum_dropout.py`) already includes mean_elite tracking. A fair comparison would be:

```bash
# Already ready — curriculum sweep with mean_elite
python3 tier2_curriculum_dropout.py --sweep --generations 100

# Then compare mean_elite vs best_params across all schedules
python3 signal_matrix_report.py  # after adding new checkpoints to matrix
```

## Summary

1. **mean_elite >> best_params** because weight averaging finds flat, centered solutions robust to train/test misalignment (SWA/model soups theory)

2. **Weight averaging is implicit evaluation-time dropout** — it suppresses signal-dependent features by averaging over individuals that encode them inconsistently

3. **Dropout and averaging are complementary**: dropout regularizes training, averaging regularizes evaluation. Both attack signal dependency from different angles.

4. **Testable prediction**: mean_elite of dropout-trained agents should show LARGER improvement for low-dropout conditions (more signal dependency to suppress)

5. **Curriculum + SWA**: the natural next experiment combines scheduled dropout with weight averaging over the training trajectory
