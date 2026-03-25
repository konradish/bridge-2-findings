# [contra] Cross-Agent Memory Transfer Fails: The Regulatory Latent Is Agent-Specific

**Date**: 2026-03-08
**Context**: Phase 2 v3 tested whether a memory-augmented GRU agent benefits from V1 regulatory latent signals delivered via input-channel augmentation. Three conditions: zeros (control), latent (V1 regulatory latent), random (noise).

## The Experiment

Architecture: GRU with 13-dim input (5 obs + 8 memory), 32-dim hidden, 7 actions. 4647 params. Trained with ES (100 pop × 200 gen) under three conditions.

Memory signal for latent condition: every 50 steps, query V1 memory bank by viability similarity (energy, integrity, thermal), receive 8-dim regulatory latent from best-matching V1 episode.

## Results (N=100 per condition)

### Primary evaluation

| Condition | Survival (± SE) | Mean Steps |
|-----------|-----------------|------------|
| Zeros     | **37% ± 4.8%**  | 1422       |
| Random    | **34% ± 4.7%**  | 1286       |
| Latent    | **16% ± 3.7%**  | 1085       |

Zeros ≈ Random (p > 0.5, overlapping CIs). Both >> Latent (p < 0.01).

### Cross-test (agent × signal matrix)

| Agent trained with | Eval signal | Survival |
|-------------------|-------------|----------|
| Zeros             | Zeros       | **40%**  |
| Zeros             | Latent      | **4%**   |
| Latent            | Latent      | **18%**  |
| Latent            | Zeros       | **5%**   |
| Latent            | Random      | **1%**   |

### GRU input weight magnitudes

| Condition | Obs weight mag | Mem weight mag | Mem/Obs ratio |
|-----------|---------------|----------------|---------------|
| Zeros     | 0.173         | 0.164          | 0.948         |
| Latent    | 0.169         | 0.163          | 0.966         |
| Random    | 0.185         | 0.167          | 0.903         |

All conditions have similar memory channel weights — none learned to ignore it.

## What the Data Shows

### 1. The V1 regulatory latent is actively harmful

Adding V1 latent signal to any agent drops survival dramatically:
- Zeros agent: 40% → 4% when latent injected
- The signal disrupts learned policy dynamics

### 2. The latent agent co-adapted but was misled

The latent-trained agent DEPENDS on the signal (18% with vs 5% without), but the signal is from a different agent's internal state. It learned to respond to patterns in the V1 latent, but those patterns don't reliably indicate the right action in V3's situation.

It's like training a musician to follow a conductor who's conducting a different orchestra — they learn to watch the baton, but the cues don't match their part.

### 3. Random noise ≈ zeros (no regularization benefit)

Random (34%) ≈ Zeros (37%). The noise injection during training didn't provide a meaningful regularization benefit. The 20-episode preliminary (random=35%, zeros=15%) was misleading small-sample noise.

### 4. The memory channel doesn't help at all

The extra input dimensions don't improve over standard 5-dim input, regardless of what fills them. The architecture change (5→13 input) is neutral (zeros matches the original V1 agent's ~20% survival range at 100 pop × 200 gen training budget — though these are different random seeds).

## Why Cross-Agent Transfer Fails

The B5 regulatory latent is an **information bottleneck** compression of the GRU hidden state, preserving viability-relevant dimensions. But "viability-relevant dimensions of the GRU hidden state" are agent-specific:

1. **Different input spaces**: V1 agent receives 5-dim obs. V3 receives 13-dim (5 obs + 8 memory). Their GRU weight matrices are entirely different.

2. **Different hidden state dynamics**: V1's 32-dim hidden state evolved under V1's specific weights. The 8-dim latent captures V1's internal representation of viability — but V3 has its own internal representation that bears no relationship to V1's.

3. **The autoencoder was trained on V1 data**: The compression maps V1 hidden → V1 latent. This is a V1-specific coordinate system. Feeding V1-latent coordinates to V3 is like giving GPS coordinates from one city as navigation instructions in another.

## What B5 IS Good For

B5 outperforms B4 for **within-agent retrieval** (Cohen's d = 1.974). The information bottleneck explanation holds: compression preserves viability-relevant similarity, enabling better episodic matching. This was confirmed by:
- Per-dim info content: B5 = 0.311, B4 = 0.279 (1.11x per dimension)
- Top dimension viability correlation: B5 = 0.629, B4 = 0.429

The retrieval mechanism works. The transfer assumption was wrong.

## Implications for Phase 3

Memory-augmented survival requires **self-memory**:

1. **Online memory building**: Agent accumulates its own episodic memory during training, encodes it with its own autoencoder, retrieves from its own past.

2. **The autoencoder must be co-trained**: Can't freeze a V1 autoencoder and use it on V3 data. Need to either:
   - Train a new autoencoder on V3 hidden states (requires enough V3 episodes first)
   - Or skip the autoencoder and use raw viability state as both key and value

3. **Curriculum approach**: Start agent without memory. Let it build experiences. Then fine-tune with access to its own memory bank. Two-phase training: (1) learn to survive without memory, (2) learn to use memory of own past survival.

This is closer to how biological memory works — organisms remember their OWN experiences, not transplanted memories from other organisms.

## Connection to Prior Work

- **Phase 2 v1** (action blending): Failed because blending disrupts GRU dynamics (82.9% override)
- **Phase 2 v2** (value-weighted retrieval): Failed because still used action blending
- **Phase 2 v3** (input-channel augmentation): Architecture is sound, but cross-agent transfer doesn't work
- **Next**: Phase 2 v3 architecture + self-memory (agent's own experiences, own autoencoder)

## The 20-Episode Lesson

The 20-episode preliminary evaluation (random=35%, latent=25%, zeros=15%) nearly led to the wrong conclusion — that random noise helps and latent is intermediate. The 100-episode evaluation reversed this completely. **Small N eval is dangerous when effect sizes are moderate.**

Minimum viable eval for this task: N ≥ 50 episodes per condition. N=100 gives ±5% SE.

---

## Data

- Training runs: `runs/memaugmented_{zeros,latent,random}_100pop_200gen/`
- Training curves: CSV logs in each run directory
- Relevance test: `runs/es_100pop_200gen/relevance_vs_stability.json`
- This analysis: 100-ep eval + cross-test, results above
