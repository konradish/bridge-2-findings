# Signal Type × Dropout: A 2D Framework for Auxiliary Information

**Date**: 2026-03-09 (updated ~15:30 UTC with full noisy sweep results)
**Context**: Combining dropout sweep results with the stochastic signal experiments.
**Headline**: Noisy signal at 30% dropout achieves **Positive Co-Learning** — the only condition where signal helps at eval time (56% vs 40% baseline).

## The Two Dimensions

### Dimension 1: Signal Determinism
- **Deterministic**: same trajectory window → same signal (HandcraftedCommentator)
- **Stochastic**: same trajectory window → varying signal (NoisyHandcraftedCommentator, LLM)

### Dimension 2: Dropout Rate
- **Low (0-30%)**: agent sees signal most of the time
- **Medium (50%)**: agent sees signal half the time
- **High (80%+)**: agent mostly trains in zeros mode

## The 2×2 Matrix (observed results)

| | Low dropout | High dropout |
|---|---|---|
| **Deterministic** | NCL collapse: zeros=1-8%, signal=0% | Good zeros-mode: zeros=60%, signal=0% |
| **Stochastic** | Baseline zeros (37%), signal usable (48%) | **PREDICTED: good zeros + signal usable** |

### Quadrant 1: Low dropout + Deterministic (drop00, drop50)
- Agent co-adapts to deterministic patterns
- Catastrophic failure when signal removed OR present at eval
- The worst of all worlds — NCL (Negative Co-Learning)
- drop50 (1%) is WORSE than drop00 (8%) — mixed mode confuses

### Quadrant 2: High dropout + Deterministic (drop80)
- Agent primarily trains in zeros mode
- The 20% signal exposure provides training gradient but no eval reliance
- Best zeros-mode: 60%
- Signal catastrophic at eval: 0% (even worse: noisy signal = 30%)
- The agent learned to IGNORE the memory channel at eval

### Quadrant 3: Low dropout + Stochastic (noisy_drop30)
- Noise prevents deterministic co-adaptation
- Agent learns to USE the signal productively
- Zeros-mode: 37% (baseline — no improvement without signal)
- Signal-at-eval: **48%** (usable! not catastrophic)
- The agent learned to USE the memory channel but depends on it

### Quadrant 4: High dropout + Stochastic (noisy_drop80 — IN PROGRESS)
- **Prediction**: combines Quadrant 2's zeros-mode strength with Quadrant 3's signal usability
- Expected zeros-mode: ~50-60% (high dropout protects zeros competence)
- Expected signal-at-eval: >0% (stochastic signal doesn't overwhelm)
- This would be the **graceful degradation** regime: works without signal, works better with it

## Why This Matters

### The Deterministic/Stochastic Distinction Is Not About Information Content

The noisy signal has the SAME information as the deterministic signal (same 8 features, just with Gaussian noise). The difference in eval behavior comes from the signal's statistical properties, not its informational content.

Deterministic signals create **sharp dependencies**. The agent's hidden state adapts to exact patterns — when those patterns are absent (zeros) or slightly different (noisy), the adaptation breaks catastrophically.

Stochastic signals create **soft dependencies**. The agent can't memorize exact signal patterns because they vary. Instead, it learns to extract the USEFUL part of the signal (the underlying features) while being robust to the VARYING part (the noise). This is equivalent to regularization.

### Implications for LLM Commentator

An LLM produces naturally stochastic signal:
- Same trajectory window → different embeddings/commentary each time
- Temperature > 0 adds noise by construction
- Context window effects create variation

**Prediction**: The LLM commentator occupies the stochastic column. At moderate dropout (50-80%), it should produce agents that:
1. Function well without signal (good zeros-mode from dropout)
2. Improve further when signal is present (stochastic signal is non-catastrophic)

This is the ideal Tier 2 behavior: the commentator helps when available, the agent copes when it's not.

### Connection to V2 mean_elite

V2 zeros mean_elite achieves 85-90% survival — far above any Tier 2 condition so far. This suggests the task may be nearly solved by optimization alone (more generations + better parameter aggregation).

The signal benefit may be more relevant for:
- Harder tasks where the ceiling is lower
- Faster convergence (reach good performance in fewer generations)
- Eval-time improvement (for agents that can use signal at eval)

## [contra] The Sweet Spot Prediction Was Wrong

Predicted: noisy_drop80 would combine good zeros-mode with eval-time signal benefit.
Actual: noisy_drop80 = 10% zeros, 1% noisy signal. Catastrophic.

The phase transition is **reversed** for stochastic signals:

| | Low dropout (30%) | Medium dropout (50%) | High dropout (80%) |
|---|---|---|---|
| **Deterministic** | 8% zeros, 0% signal | 1% zeros, 0% signal | **60% zeros**, 0% signal |
| **Stochastic** | **37% zeros, 48% noisy** | 24% zeros, 51% noisy | 10% zeros, 1% noisy |

Deterministic: phase transition at 80% (low→high dropout helps)
Stochastic: inverse gradient (low→high dropout HURTS)

### The Mechanism: Noise Substitution

Signal noise and dropout noise are **substitutes**, not complements. The agent needs a certain level of regularization to prevent co-adaptation, but too much destroys the optimization landscape.

**Deterministic signal** (zero intrinsic noise):
- 0% dropout → zero regularization → co-adaptation → NCL
- 80% dropout → sufficient regularization → good zeros-mode

**Stochastic signal** (σ=0.3 intrinsic noise):
- 30% dropout → noise provides regularization → no co-adaptation, signal usable at eval
- 80% dropout → noise + dropout = too much randomness → CMA-ES can't optimize (fitness landscape too noisy with 5 eval episodes)

The **total regularization** (noise + dropout) has a sweet spot. For deterministic signal, that's ~80% dropout. For stochastic signal (σ=0.3), that's ~30% dropout.

### Implication for LLM Commentator

The LLM produces stochastic signal (different output each time). Based on these results:
- Use **low dropout** (20-30%), not high
- The LLM's natural variation provides the regularization that deterministic signals need dropout for
- Higher dropout with LLM would degrade the optimization landscape

## Full Data Matrix

| Condition | Train signal | Dropout | Zeros eval | Signal eval | Pattern |
|-----------|-------------|---------|-----------|------------|---------|
| stage1_baseline | — | — | 37% | — | Baseline |
| det_drop00 | handcrafted | 0% | 8% | 0% | NCL |
| det_drop50 | handcrafted | 50% | 1% | 0% | Worse NCL |
| det_drop80 | handcrafted | 80% | **60%** | 0% | Zeros-mode only |
| drop100 | zeros | 100% | 49% | — | CMA-ES only |
| noisy_drop00 | noisy(0.3) | 0% | 6% | 25% | Overfit to signal, no dropout |
| noisy_drop10 | noisy(0.3) | 10% | 12% | **73%** | Best signal-at-eval (peak 1) |
| noisy_drop20 | noisy(0.3) | 20% | 0% | 17% | Confusion zone |
| noisy_drop30 | noisy(0.3) | 30% | **45%** | 56% | Best zeros-mode (peak 2, PCL) |
| noisy_drop50 | noisy(0.3) | 50% | 10% | 54% | Signal-dependent |
| noisy_drop80 | noisy(0.3) | 80% | 13% | 0% | Over-regularized |
| V2 zeros mean_elite | zeros | — | **85%** | — | 200-gen ES |

### Det_drop80 Full Signal Response (100-episode eval)

| Eval signal | Survival | Notes |
|-------------|---------|-------|
| zeros | 55% | Agent's optimized mode |
| random | 60% | Noise treated as null |
| noisy_0.3 | 30% | Structure hurts but noise buffers |
| noisy_0.5 | 40% | More noise = more buffering |
| handcrafted | 0% | Full structure = catastrophic |

### [update] Cross-Signal Matrix Findings (100-ep eval, beat 93)

Key patterns from full evaluation matrix:

**1. Tolerance vs Utilization**: det_drop80 TOLERATES noisy signal (30-40%) but doesn't BENEFIT from it (all below zeros baseline of 55%). Noisy-trained agents (drop10, drop30) BENEFIT from noisy signal (64-66%, 56% vs zeros of 17%, 45%).

**2. Noise as Buffer**: det_drop00 with noisy signal (21-28%) vs with handcrafted signal (2%). Noise dilutes the deterministic structure that causes co-adaptation. The more noise (σ=0.5 > σ=0.3), the more buffer.

**3. Signal Wall**: det_drop100 (pure CMA-ES, never saw signal) rejects ALL signal types: 0% for handcrafted AND noisy. The architecture never developed any signal-processing pathway.

**4. det_drop80 vs det_drop100**: Dropout-trained agent (55% zeros, 30-40% noisy) vs zero-signal agent (53% zeros, 0% noisy). The 20% signal exposure during training gave the architecture TOLERANCE for signal — it doesn't help, but it doesn't destroy. Pure-zeros training creates total signal rejection.

**Implication**: Dropout training creates three distinct capabilities:
- Independence (zeros-mode competence)
- Tolerance (ability to function with degraded/noisy signal)
- But NOT utilization (ability to benefit from signal) — that requires stochastic training
