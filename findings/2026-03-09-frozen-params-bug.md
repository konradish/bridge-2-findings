# Frozen Params Bug: ES Training Was Not Training

**Date**: 2026-03-09
**Context**: Investigating why Tier 2 zeros gets 32% while Phase 3 zeros gets 66% from the same Stage 1 checkpoint led to discovering that both training pipelines have been selecting lucky gen-0 mutants and preserving them unchanged for 200 generations.

## The Bug

The ES training loop saves `best_params` — the individual with the highest fitness ever seen. The fitness function is `total_steps / n_eval_episodes`, capped at 2000 (max episode length).

With only 3 eval episodes per individual and ~35% survival rate per episode:
- At gen 0, 100 individuals are evaluated
- Expected number surviving all 3 episodes: 100 × 0.35³ ≈ 4.3 individuals
- These get fitness = 2000.0 (maximum possible)
- `if fitnesses[elite_idx[-1]] > best_fitness:` — strict `>` means once 2000 is hit, best_params **never updates again**

## Verification

```
Tier2 zeros: gen0 vs final max param diff = 0.0  ← FROZEN
Phase3 zeros: gen0 vs final max param diff = 0.0  ← FROZEN

Stage 1 vs Tier2 final: 0.377 (sigma=0.1 → large mutations)
Stage 1 vs Phase3 final: 0.174 (sigma=0.05 → small mutations)
Tier2 vs Phase3: 0.402 (completely different individuals)
```

Both pipelines spend 200 generations × 100 pop × 3 episodes = 60,000 episodes evolving a population whose improvement is never captured in the saved model.

## What the Training Actually Did

| Metric | Tier 2 zeros (sigma=0.1) | Phase 3 zeros (sigma=0.05) |
|--------|--------------------------|----------------------------|
| Gen 0 mean fitness | 1206 | 1344 |
| Gen 199 mean fitness | 1568 | 1697 |
| Gen 0 best fitness | 2000 | 2000 |
| Gen 199 best fitness | 2000 | 2000 |
| Saved params | Gen-0 mutant | Gen-0 mutant |
| Eval survival | 32% | 66% |

The population DOES improve (mean fitness increases from 1206→1568 and 1344→1697). But `best_params` (the saved model) is a lucky gen-0 individual frozen forever. The 32% vs 66% difference is entirely due to which random mutant got lucky on 3 episodes.

## Implications

### 1. All Previous Experimental Comparisons Are Confounded

The "handcrafted ≈ zeros" finding (both 32%) is comparing two lucky gen-0 mutants. The similarity could be coincidence. The co-adaptation finding (handcrafted-trained agent drops from 32% to 16% without its signal) is still valid — that agent learned to depend on the signal. But the absolute performance levels are meaningless for comparing signal types.

### 2. Phase 3's "66% zeros" Was a Lucky Draw

The zeros condition "beating" self-memory (66% vs 44%) is partly real (the distractor trap is genuine) but the 66% absolute level was a lucky mutant. The true fine-tuned zeros performance is unknown.

### 3. 60,000 Episodes of Wasted Compute Per Condition

The population centroid (mean_elite) is the real product of ES training, but it was never saved or evaluated.

## The Fix (Applied)

Three changes to `tier2_train.py`:

1. **Viability bonus**: `fitness = steps + (energy + integrity) / 400`. Survivors get a small bonus (0 to 0.5) based on remaining viability, breaking the fitness ceiling. The ES can now discriminate among survivors.

2. **More eval episodes**: 5 instead of 3. Probability of surviving all 5: 0.35⁵ ≈ 0.5%. With 100 individuals, ~0.5 expected to hit ceiling. Much less likely to freeze.

3. **Save mean_elite**: The population centroid is saved alongside best_params. After 200 generations, mean_elite captures the ES's actual optimization trajectory.

4. **Sigma 0.05**: Matches Phase 3 for consistent comparison. Smaller mutations = less lottery.

## Retrained Experiment

Running now with the fixed pipeline. Will compare:
- best_params (frozen individual) vs mean_elite (population centroid)
- zeros vs handcrafted with the fixed training
- Whether the fix reveals a real difference between signal types

**Update**: With viability bonus scaled to 0-50 (via `(energy+integrity)/4`), gen 0 best = 2047/2050 max. Still near ceiling. The key comparison will be best_params vs mean_elite. The mean_elite captures 200 generations of population optimization regardless of whether best_params freezes.

ETA for results: ~15:30 UTC (7 hours from start).

## Broader Lesson

[contra] from compiler testing analogy (taidarilla thread): this is a missing *positive* test. We tested what the agent does WITH different signals but never verified that the training loop actually TRAINS. A simple invariant check — "does best_params differ from init_params after training?" — would have caught this immediately.

The mean fitness improvement (1206→1568) looked like training was working. But that's the *population* improving, not the *saved model*. The metric we tracked (best_fitness) flatlined at gen 0, and we didn't notice because 2000 looked like "perfect performance" rather than "ceiling hit."
