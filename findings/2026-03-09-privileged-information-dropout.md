# Privileged Information Dropout: Theoretical Framework for the Dropout Sweep Results

**Date**: 2026-03-09
**Context**: Connecting the dropout sweep results (drop80=60% vs drop100=49%) to the Learning Using Privileged Information (LUPI) literature.

## The Framework: Learning Using Privileged Information (LUPI)

Vapnik & Vashist 2009 introduced LUPI: additional information available during training but unavailable at test time. The classic example is a medical student who learns with a textbook (privileged) but must diagnose without it (test).

In our setup:
- **Training**: agent receives handcrafted commentator signal (8-dim behavioral features)
- **Evaluation**: agent receives zeros (no signal)
- The handcrafted signal is privileged information — it sees the full observation state and computes features the agent can't access through its own obs→GRU→action pathway.

## Direct Parallel: "Privileged Information Dropout in RL" (arXiv:2005.09220)

Baisero & Amato 2020. This paper describes **exactly** our approach:

- RL agents trained with access to privileged state information
- Key insight: naive use of PI causes the agent to rely on it (co-adaptation) → fails without it at test time
- **Solution: PID (Privileged Information Dropout)** — stochastically mask the privileged information during training
- Result: "outperforms alternatives for leveraging privileged information, including distillation and auxiliary tasks"

Our dropout sweep is a direct instantiation of PID:
| Their term | Our implementation |
|------------|-------------------|
| Privileged information | Handcrafted 8-dim signal |
| Agent observation | Raw env obs (Crafter) |
| PI dropout | Memory channel dropout (zeros masking) |
| Dropout rate 0.8 | drop80 (our best result) |

## Second Reference: π-Distill (arXiv:2602.04942)

"Privileged Information Distillation for Language Models" — extends PI to LLMs. Joint teacher-student framework where a single model is both PI-conditioned teacher and unconditioned student. 11.8% improvement over SFT+RL baseline on Travel Planner.

Less directly applicable (distillation-based, not dropout-based), but confirms PI is an active research direction in 2026.

## What This Means for Our Results

### The Decomposition Is Clean

| Component | Contribution | Mechanism |
|-----------|-------------|-----------|
| CMA-ES (rank-based optimizer) | +12pp (37%→49%) | Better optimization, no ceiling problem |
| 20% PI exposure (via PID) | +11pp (49%→60%) | Privileged information regularization |

The handcrafted signal provides genuine privileged information — behavioral features computed from the full state that the agent can't derive from its own observations. At 80% dropout, the agent:
1. Primarily trains in zeros mode (maintaining baseline competence)
2. Occasionally receives rich state features that guide credit assignment
3. Cannot co-adapt because the signal is usually absent

### Why 50% Dropout Fails

The PID literature notes that optimal dropout rates are task-dependent. Our phase transition (50%→1%, 80%→60%) suggests:

- At 50%: agent receives signal frequently enough to build partial reliance, but inconsistently enough that the reliance is unstable. Worse than either extreme.
- At 80%: agent's primary strategy is zeros-based. The 20% signal acts as occasional perturbation that provides useful gradient information without becoming a dependency.

This matches the NCL reversal finding (Maheshwari et al. 2025): aggressive dropout reverses negative co-learning.

### Implications for LLM Commentator

The handcrafted signal is:
- **Deterministic**: same observation → same features
- **High-dimensional structure**: 8 correlated features with clear patterns
- **Overwhelming**: dominates the GRU input when present

An LLM commentator (Qwen 3.5) would produce:
- **Stochastic**: same observation → varying commentary
- **Softer structure**: embedding of natural language, less rigid
- **Information-rich**: can capture higher-order patterns humans would notice

**Prediction**: LLM signal might be usable at lower dropout rates (50% or even 30%) because its stochasticity provides built-in regularization. The handcrafted signal's failure at 50% dropout may be specific to its deterministic nature, not a general property of auxiliary signals.

## Connection to Broader PI Literature

The PI framework reframes the entire tier architecture:

- **Tier 1** (base agent): learns from environment rewards only
- **Tier 2** (commentator): provides privileged information during training
- **Tier 3** (narrative layer): would provide even higher-level PI

Each tier adds a layer of privileged information. The key insight from PID: this information must be **stochastically masked** to prevent co-adaptation. The tier architecture IS a privileged information hierarchy with dropout-based training.

This is a cleaner theoretical framework than "auxiliary memory channel" or "co-learning." It has decades of theory behind it (Vapnik 2009) and a direct RL instantiation (Baisero & Amato 2020).
