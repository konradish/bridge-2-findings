# Tier 2 Handcrafted Results: Structured Signal ≈ No Signal

**Date**: 2026-03-09
**Context**: Tested whether structured behavioral interpretation (handcrafted Tier 2) helps when the agent is fine-tuned with it. Answer: no. Co-adaptation without benefit.

## Experimental Design

Three conditions fine-tuned from Stage 1 checkpoint (200 gen ES, pop 100):
- **zeros**: memory channel receives constant zeros
- **random**: memory channel receives random noise per window
- **handcrafted**: memory channel receives 8 behavioral features (energy trend, urgency, integrity trend, action entropy, switch rate, consume fraction, progress, survival estimate) computed from 50-step trajectory windows

Evaluated with all three signal types (3×3 matrix + Stage 1 baseline).

## Results: Evaluation Matrix

| Trained with \ Eval with | zeros | random | handcrafted |
|--------------------------|-------|--------|-------------|
| **zeros** | 32% | 33% | 0% |
| **random** | 33% | 34% | 0% |
| **handcrafted** | 16% | 22% | **32%** |
| **stage1_baseline** | 35% | 34% | 0% |

## Key Findings

### 1. Handcrafted Tier 2 ≈ Zeros ≈ Baseline

All conditions converge to ~32-35% survival. Fine-tuning with structured behavioral features does not improve over fine-tuning with zeros. The structured signal provides no measurable benefit.

### 2. Co-adaptation Without Benefit

The handcrafted-trained agent shows strong co-adaptation:
- With handcrafted signal: 32%
- Without (zeros): 16%
- With random: 22%

The agent learned to DEPEND on the signal (halved performance without it) without BENEFITING from it (same performance as agents that never had it). This is the same co-adaptation pattern from Phase 3 (self-memory: 44% with, 40% without) but even more pronounced.

### 3. Handcrafted Signal Is Catastrophic for Untrained Agents

Every agent not trained with handcrafted signal scores 0% when given it. The strong structured signal (high variance, multi-dimensional) overwhelms agents that learned with zeros/random. Consistent with Phase 3's "untrained + memory = 1%" and the Distractor Trap.

### 4. Fine-Tuning Itself Doesn't Help Here

Phase 3 showed fine-tuning from Stage 1 improved zeros from 47% to 66%. But in this experiment, zeros fine-tuning gives only 32% (vs baseline 35%). The Tier 2 training pipeline may have a subtle difference from Phase 3's — possibly in episode execution or evaluation seeds. The RELATIVE finding (handcrafted ≈ zeros) is robust; the absolute numbers need investigation.

## Interpretation Through Neuroscience Framework

My prediction was:
- If handcrafted > zeros → structured representation is the key factor
- If handcrafted ≈ zeros → stochasticity/instability may also be needed
- If handcrafted < zeros → architectural bottleneck

**Result: handcrafted ≈ zeros.**

The handcrafted commentator provides structured signal but it is:
1. **Deterministic** — same trajectory always produces same signal
2. **Fully specified** — 8 named features, no ambiguity
3. **Synchronous** — computed exactly when needed, no temporal uncertainty

These properties make it a "consolidated memory" in the neuroscience framework — stable, precise, and non-generalizable. The agent can memorize the mapping from handcrafted signal to actions without extracting the underlying pattern.

The LLM commentator would differ in key ways:
- **Stochastic** — attention patterns vary, producing different emphasis
- **Semantically rich** — regression head compresses interpretive representation, not hand-designed features
- **Learned** — fine-tuned on survival prediction, not hand-coded heuristics

But the handcrafted result suggests something deeper: the 8-dim memory channel through a 4K-param GRU may simply not have enough capacity to benefit from external signal in this environment. The GRU might already be near-optimal for the gridworld's complexity, and the 32-35% ceiling (in this evaluation) might be the environment's baseline with this agent architecture.

## Next Steps

1. **Investigate eval discrepancy**: Phase 3 zeros got 66%, Tier 2 zeros gets 32%. Same checkpoint, same architecture. Need to identify the evaluation difference.

2. **Test LLM commentator**: If stochasticity is the missing ingredient, the LLM's variable output might help. But the handcrafted ≈ zeros result tempers expectations.

3. **Consider architectural changes**: The 8-dim channel through GRU may be a bottleneck. Wider channel? Different integration mechanism?

4. **Test embedding commentator**: nomic-embed-text showed d=0.43-0.54 discrimination. Worth testing whether a qualitatively different signal type helps.

## Co-Adaptation Summary (Across All Experiments)

| Phase | Signal | With signal | Without signal | Dependency | Benefit |
|-------|--------|-------------|---------------|------------|---------|
| Phase 3 | Self-memory (argmax) | 44% | 40% | +4pp | 0 (below zeros 66%) |
| Phase 3 | Self-memory (soft k-NN) | 55% | 40% | +15pp | 0 (below zeros 66%) |
| Tier 2 | Handcrafted | 32% | 16% | +16pp | 0 (equals zeros 32%) |

Pattern: agents consistently co-adapt to memory signals, creating dependency without benefit. The dependency is strong (up to +16pp), but the co-adapted agent never exceeds the zeros baseline.
