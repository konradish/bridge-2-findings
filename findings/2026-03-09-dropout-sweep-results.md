# Dropout Sweep Results: 80% Dropout Produces 60% Survival

**Date**: 2026-03-09
**Context**: Testing the NCL reversal prediction from Maheshwari et al. 2025. Handcrafted Tier 2 signal with Sep-CMA-ES training at three dropout rates.

## Experimental Setup

- Sep-CMA-ES, 100 generations, pop_size=29 (auto), 5 eval episodes
- Init: Stage 1 checkpoint (baseline 37% survival with zeros)
- Commentator: HandcraftedCommentator (8 behavioral features)
- Dropout rates: 0.0, 0.5, 0.8 (static throughout training)
- Evaluation: 100 episodes with signal ON and signal OFF (zeros)

## Results

| Condition | Train best | Train mean | Eval w/signal | Eval w/zeros | vs baseline |
|-----------|-----------|------------|---------------|-------------|-------------|
| stage1_baseline | — | — | — | 37% | — |
| drop00 (0%) | 2047 | 1302 | 0% | 8% | -29pp |
| drop50 (50%) | 2049 | 1520 | 0% | 1% | -36pp |
| drop80 (80%) | 2049 | 1590 | 0% | **60%** | **+23pp** |

## Key Findings

### 1. Handcrafted Signal Is Catastrophic at Eval Time

ALL agents score 0% when given the handcrafted signal at evaluation, including agents trained entirely with it (drop00). The structured 8-dim signal overwhelms the GRU at inference regardless of training condition.

This is more extreme than V1's results (where the frozen gen-0 mutant scored 32% with handcrafted). The CMA-ES-trained agents adapted differently to the handcrafted signal — possibly more specialized to training seeds.

### 2. 80% Dropout → 60% Survival (Best Result)

The drop80 agent evaluated with zeros achieves 60% survival — 23 percentage points above the Stage 1 baseline (37%). This is the highest legitimate survival rate in the experiment series (the Phase 3 "66%" was a confounded gen-0 mutant).

### 3. Dropout Rate Is Critical

| Dropout | Zeros eval | Interpretation |
|---------|-----------|----------------|
| 0.0 | 8% | Full NCL: agent overfit to signal, can't function without it |
| 0.5 | 1% | Worse than 0.0! Half-signal confuses more than full signal |
| 0.8 | 60% | Phase transition: enough zeros-mode training to generalize |

The 0.5 dropout result is striking — it's WORSE than 0.0. The agent gets mixed signals (sometimes handcrafted, sometimes zeros) and can't learn either mode well. There appears to be a phase transition between 0.5 and 0.8 where the agent shifts from "try to use the signal" to "primarily zeros-based, occasionally enriched."

### 4. Population Dynamics Confirm the Pattern

| Dropout | Gen 0 mean | Gen 99 mean | Interpretation |
|---------|-----------|-------------|----------------|
| 0.0 | 379 | 1302 | Slow learning, signal-dependent population |
| 0.5 | 679 | 1520 | Better than 0.0 during training |
| 0.8 | 1131 | 1590 | Best population mean, mostly-zeros mode |

Higher dropout → better starting fitness (agent sees mostly zeros, which is what it was pretrained on) AND better final population.

## Control Result: dropout=1.0 (Pure Zeros CMA-ES)

**drop100 = 49%** (pure zeros, CMA-ES, 100 gen)

| Condition | Zeros eval | Source of improvement |
|-----------|-----------|---------------------|
| Stage 1 baseline | 37% | — |
| drop100 (pure zeros CMA-ES) | 49% | +12pp from CMA-ES optimizer |
| drop80 (80% dropout) | 60% | +11pp from 20% handcrafted signal |

**The 20% handcrafted exposure genuinely helped.** This is the first evidence in the entire experiment series that Tier 2 signal provides actual benefit.

The signal contains real information that improves training (+11pp), but is too deterministic/overwhelming for inference (0% at eval). Dropout protects the agent from over-reliance while allowing useful information to flow through during training.

## Interpretation

The phase transition at 0.8 dropout aligns with the NCL paper's finding (80% optimal). The mechanism:

1. At 0% dropout: agent receives constant handcrafted signal → co-adapts → fails without it
2. At 50% dropout: agent receives unpredictable mix → can't learn stable policy for either mode
3. At 80% dropout: agent primarily trains in zeros mode (like Stage 1) → maintains zeros competence → the occasional 20% handcrafted acts as mild perturbation/regularization

The handcrafted signal is too strong and too deterministic to serve as useful auxiliary information. It overwhelms rather than enriches. But at 80% dropout, the agent barely sees it, so it can't overfit to it.

**Prediction for LLM signal**: The LLM commentator produces softer, more stochastic signal. It might be usable at lower dropout rates (50% or even 30%) because it provides genuine asymmetric information without the overwhelming deterministic structure.

## Update: V2 mean_elite Reframes the Baseline (added ~14:45 UTC)

**[contra]** V2 zeros mean_elite = 85-90% survival (3 seeds: 84%, 86%, 90%). This is the same task, same agent architecture, trained with zeros only — no Tier 2 signal.

| Agent | Optimizer | Gens | best_params | mean_elite |
|-------|-----------|------|-------------|-----------|
| V2 zeros | ES+viability | 200 | 67% | **85%** |
| V2 random | ES+viability | 200 | 82% | **84%** |
| drop100 | CMA-ES | 100 | 49% | N/A |
| drop80 | CMA-ES | 100 | 60% | N/A |

Two confounds in the original +11pp finding:
1. **Generation count**: 100 (CMA-ES) vs 200 (V2) — more training helps
2. **Evaluation target**: best_params is noisy; mean_elite (population mean) is much more stable

V2 random's best_params (82%) >> V2 zeros' best_params (67%), but their mean_elites converge (84% ≈ 85%). The apparent +15pp "random signal benefit" was individual luck, not signal content.

**Revised question**: Does handcrafted signal provide benefit above the ~85% mean_elite baseline? The +11pp finding (49%→60%) may not replicate when:
- The baseline is 85% instead of 49%
- Evaluation uses mean_elite instead of best_params

V2 handcrafted training in progress (200 gen). Result pending.
