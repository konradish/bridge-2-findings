# T3 Counterfactual Sensitivity — B5 > B4 Confirmed

**Date**: 2026-03-08
**Context**: Primary test from PRD section 7. Does the regulatory latent (B5) retrieve different memories than event-only (B1) or raw hidden state (B4) when the agent's internal state differs but external context is the same?

---

## The Test

T3 creates paired scenarios: same external context (same seed, same environment layout, same observations), but different internal state (stable vs depleted — energy reduced by 60, fatigue +30, toxicity +20, hidden state perturbed).

For each pair, every retrieval condition queries the memory bank with top-3 retrieval. We measure memory divergence: how different are the retrieved episodes for stable vs depleted?

Jaccard distance between retrieved episode sets. 0 = identical retrieval. 1 = completely different retrieval.

## Results (100 episodes)

| Condition | Mean Divergence | Std | % Divergent | N |
|-----------|----------------|-----|-------------|---|
| B0 (memoryless) | 0.000 | 0.000 | 0% | 100 |
| B1 (event-only) | 0.000 | 0.000 | 0% | 100 |
| B2 (semantic) | 0.000 | 0.000 | 0% | 100 |
| B3 (control features) | 0.490 | 0.070 | 98% | 100 |
| B4 (raw hidden) | 0.361 | 0.290 | 64% | 100 |
| **B5 (regulatory latent)** | **0.853** | **0.201** | **98%** | 100 |

## Interpretation

### B1/B2: Zero divergence (as predicted)

External-only retrieval conditions cannot distinguish between depleted and stable agents in the same environment. They retrieve identical memories because the external context is identical. This is the fundamental limitation of conventional memory systems: a depleted agent and a stable agent in the same situation retrieve the same experiences.

### B3: Moderate divergence (0.490)

Hand-crafted internal statistics (mean energy, min integrity, crisis time fractions) detect the internal state difference. But the features are coarse — they reduce the full viability trajectory to summary statistics, losing temporal structure.

### B4: Moderate but noisy divergence (0.361, std=0.290)

Raw GRU hidden state (dim-32) contains viability information but also non-viability dimensions. The noise dilutes the signal. High variance (0.290) means B4 is inconsistent — sometimes it detects the internal state difference, sometimes it doesn't.

### B5: High divergence (0.853, std=0.201)

The regulatory latent (dim-8, trained to predict viability + collapse) strips noise dimensions and amplifies viability-relevant structure. It retrieves maximally different memories for depleted vs stable agents. Consistent across episodes (std=0.201).

**B5 vs B4 ratio: 2.36x.** Compression + viability-supervised training makes the memory key substantially more sensitive to internal state.

**Cohen's d = 1.974** (large effect). Nearly 2 standard deviations of improvement. This is not marginal — the regulatory latent is fundamentally different from raw hidden state for this task.

## What This Means

### [from: Weber et al. 2025]

B1 is proxy retrieval (external sensory signals). B5 is ground-truth retrieval (interoceptive state). Weber et al. showed biological reward is fundamentally interoceptive — external signals are predictive estimates, internal signals are ground-truth. This result is the memory-retrieval analog: indexing by internal state (B5) retrieves qualitatively different and more relevant memories than indexing by external events (B1).

### [from: Dulberg et al. 2022]

The 3-variable V1 environment already produces a functional regulatory latent. With competing drives (V2), the regulatory latent should have higher dimensionality and even sharper retrieval discrimination. V2 training currently running.

### The compression argument

Why does B5 beat B4? The raw hidden state (32 dims) uses ~3-5 effective dimensions (PCA finding). But those 3-5 viability-relevant dimensions are mixed with 27-29 noise/navigation dimensions. The autoencoder extracts the viability dimensions into a clean 8-dim space, making cosine similarity more discriminative.

This is exactly the "strip the noise" hypothesis. The body isn't the whole hidden state — it's the viability-relevant compressed core.

## Natural T3 Control Experiment (137 episodes)

Ran a "natural depletion" variant: instead of synthetic perturbation, forced the agent through different movement patterns early in the episode to create natural energy differences.

| Condition | Mean Div (natural) | Mean Div (synthetic) |
|-----------|-------------------|---------------------|
| B1 (event-only) | 0.836 | 0.000 |
| B3 (control) | 0.215 | 0.490 |
| B4 (raw hidden) | 0.842 | 0.361 |
| B5 (regulatory latent) | 0.833 | 0.853 |

**[contra]** The natural T3 is a **confounded** test. Different actions → different positions → different observations. B1's high divergence (0.836) comes from external context differences, NOT internal state sensitivity. The synthetic T3 is the correct design because it isolates the internal state variable by keeping external context identical.

B1's zero divergence in the synthetic test is the **expected** result, confirming the test is well-designed. The "caveat" about synthetic perturbation was wrong — it's the proper counterfactual.

## Remaining Caveats

1. **Memory bank is small**: 50 episodes. Larger bank needed for production evaluation.

2. **Agent is weak**: V1 agent only survives 12% of test episodes. Stronger agent needed to test whether the regulatory latent matters for competent agents (where drives actually compete).

3. **No action-selection integration**: Currently measuring retrieval divergence only. The full test (PRD Phase 2) uses retrieved memories to guide action selection and measures survival improvement.

## Files

- `asi-experiment/memory_retrieval.py` — B0-B5 retrieval system
- `asi-experiment/runs/es_100pop_200gen/t3_results.json` — Full results

---

SUBSTANTIVE — This is the first quantitative confirmation of the regulatory latent hypothesis.
