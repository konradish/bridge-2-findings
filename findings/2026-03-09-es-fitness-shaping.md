# Rank-Based Fitness Shaping: Fixing the ES Training Pipeline

**Date**: 2026-03-09
**Context**: The frozen params bug (best_params locked at gen 0 due to fitness ceiling) led to researching how modern ES implementations handle this. The answer: they don't use raw fitness at all.

## The Core Insight

Modern evolution strategies (NES, CMA-ES, OpenAI ES) use **rank-based fitness shaping**: raw fitness values are replaced with utilities derived from rank ordering. This makes the optimizer invariant to monotonic transformations of the fitness function — including ceilings, plateaus, and outliers.

## Rank-Based Utility Function (Wierstra et al. 2014)

The NES utility function:
```
u_i = max(0, log(λ/2 + 1) - log(i)) / Σ_j max(0, log(λ/2+1) - log(j)) - 1/λ
```
where i is the rank (1 = best, λ = worst).

Properties:
- Only the **rank** matters, not the raw fitness value
- Top-half individuals get positive utility, bottom-half get zero
- Utilities sum to zero (automatic baselining)
- The gradient estimate becomes `∇J ≈ Σ u_i · ε_i / σ`

**Why this fixes the ceiling**: even if 50 individuals all survive 2000 steps, they still have different ranks (broken by viability bonus or random tiebreaking). The ES gets meaningful gradient signal regardless.

## CMA-ES: The Gold Standard

CMA-ES (Hansen 2006) goes further:
1. Uses rank-based selection (inherent, not added)
2. Adapts the **covariance matrix** of the search distribution
3. Learns the local landscape geometry — elongated valleys, correlations between parameters
4. Invariant to all order-preserving fitness transformations

For my 4K-param agent, **Sep-CMA-ES** (diagonal covariance) is feasible:
- O(n) per generation instead of O(n²)
- Still adapts per-dimension step sizes
- Available via `pip install cmaes` (CyberAgentAILab/cmaes)

### Simple Integration (ask-and-tell API)
```python
from cmaes import CMA

optimizer = CMA(mean=init_params, sigma=0.05)
for gen in range(200):
    solutions = []
    for _ in range(optimizer.population_size):
        params = optimizer.ask()
        fitness = evaluate(params)
        solutions.append((params, -fitness))  # CMA-ES minimizes
    optimizer.tell(solutions)
```

No elite tracking, no sigma tuning, no population management. The optimizer handles all of this internally with rank-based selection and covariance adaptation.

## My ES vs. Modern ES

| Feature | My ES (current) | OpenAI ES (Salimans 2017) | CMA-ES (Hansen 2006) |
|---------|-----------------|---------------------------|----------------------|
| Fitness → gradient | Raw (with viability bonus) | Rank-based utilities | Rank-based weights |
| Selection | Truncation (top-20 mean) | All (weighted by rank) | μ-best (weighted by rank) |
| Step size | Fixed σ=0.05 | Fixed σ with noise scaling | Adaptive (path-length) |
| Search distribution | Isotropic Gaussian | Isotropic Gaussian | Full/diagonal covariance |
| Ceiling invariance | No (viability bonus hack) | Yes (by construction) | Yes (by construction) |
| Landscape adaptation | None | None | Covariance learns correlations |

## The Co-Adaptation Connection

The co-adaptation pattern (agent depends on signal without benefiting from it) connects to Hinton et al. (2012) on dropout:

> "Hidden units learn to rely on specific other hidden units rather than being independently useful."

My agent's GRU hidden units co-adapt with the memory signal during training. When the signal is removed, the hidden units that relied on it fail. This is the same mechanism dropout was designed to prevent.

**Implication**: Training with **random masking** of the memory channel (sometimes zeros, sometimes signal) might prevent co-adaptation while allowing the agent to USE the signal when available. This is analogous to dropout for the memory channel.

Training schedule: Start with p=0.5 masking (50% of refresh intervals provide signal, 50% provide zeros), anneal to p=0.1 (mostly signal) as training progresses. The agent learns to treat the memory channel as OPTIONAL enrichment rather than required input.

## Implementation Plan

### V2 (current, running)
- Viability bonus breaks ceiling partially
- Save mean_elite for comparison
- Results expected ~15:30 UTC

### V3 (next)
- Replace custom ES with Sep-CMA-ES (`cmaes` library)
- Rank-based selection automatic
- Add memory channel dropout (p=0.5 → 0.1 anneal)
- Compare: CMA-ES + dropout vs current ES + viability bonus

### V4 (if V3 shows improvement)
- Add LLM commentator (Qwen 3.5 0.8b via Ollama)
- Full Tier 2 test: LLM signal + CMA-ES + dropout

## References

- Wierstra, D. et al. (2014). "Natural Evolution Strategies." JMLR 15.
- Hansen, N. (2016). "The CMA Evolution Strategy: A Tutorial." arXiv:1604.00772.
- Salimans, T. et al. (2017). "Evolution Strategies as a Scalable Alternative to Reinforcement Learning." arXiv:1703.03864.
- Hinton, G. et al. (2012). "Improving neural networks by preventing co-adaptation of feature detectors." arXiv:1207.0580.
- CyberAgentAILab/cmaes: Python library for CMA-ES. https://github.com/CyberAgentAILab/cmaes
