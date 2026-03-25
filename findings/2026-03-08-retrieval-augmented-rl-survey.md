# Retrieval-Augmented RL: What Works Beyond Naive Similarity

**Date**: 2026-03-08
**Context**: Phase 2 of the ASI experiment (retrieval-guided action selection) failed — naive action blending from cosine-similar retrieved episodes doesn't improve survival. This survey maps the field to identify what Phase 2 should actually do.

## The Problem

Our Phase 2 approach:
1. Retrieve episodes with similar regulatory latent states (B5 cosine similarity)
2. Compute global action distribution from retrieved episodes
3. Blend with base policy softmax

Result: B5-guided agent survives *worse* than memoryless (6% vs 15%). The action distributions wash out context-specific information.

**Diagnosis**: Cosine similarity retrieves *similar states* but doesn't evaluate whether the *actions taken from those states were good*. A retrieved episode where the agent died from the same state is weighted equally to one where it survived.

## The Field: Four Approaches to Memory-Augmented RL

### 1. MemRL — Value-Weighted Retrieval (arXiv:2601.03192, Jan 2026)

**Key insight**: Don't just retrieve similar memories — retrieve *useful* memories, where utility is learned from outcomes.

**Two-phase retrieval**:
- Phase A: Cosine similarity filters candidates (same as our B5 retrieval)
- Phase B: Re-ranks using composite score: `score = (1-λ)·similarity + λ·Q̂` where Q̂ is a learned utility estimate

**Q-value learning**: Monte Carlo updates — `Q_new ← Q_old + α(r - Q_old)` — applied only to memories actually used. Memories that led to good outcomes get high Q, memories that led to failure get low Q. Over time, the system learns which memories are worth retrieving.

**[update]** This directly solves our Phase 2 problem. We retrieve by similarity alone. MemRL says: retrieve by similarity *and* outcome quality. In our setting: episodes where the agent survived from a similar regulatory state should have high Q; episodes where it died should have low Q.

**Architecture**: Memory as Intent-Experience-Utility triplets `(z, e, Q)`. The frozen LLM (or in our case, frozen GRU agent) conditions on retrieved context without parameter updates.

**Results**: 79.8% average success vs 69.9% for static cosine RAG. The λ=0.5 balance between similarity and utility is optimal — pure similarity (λ=0) or pure utility (λ=1) both underperform.

**Relevance to us**: HIGH. We can add Q-values to our memory bank entries and learn them from survival outcomes. This is the minimal change that should fix Phase 2.

### 2. RA-DT — Sub-Trajectory Retrieval (arXiv:2410.07071, Oct 2024)

**Key insight**: Don't retrieve whole episodes — retrieve *sub-trajectories* relevant to the current moment.

**Method**: External memory stores key-value pairs where keys are embeddings of past sub-trajectories and values are the actual trajectory segments. At inference, the current state is embedded, top-k similar sub-trajectories retrieved, and the Decision Transformer conditions on them via cross-attention layers.

**Retrieval scoring**: `s_ret = s_rel + α·s_u` where s_rel is cosine similarity and s_u is total return from the containing episode. This biases retrieval toward sub-trajectories from *successful* episodes.

**Grid-world results**: Near-optimal on 10x10 Dark-Room, outperformed baselines on 40x20. Uses only 50 context transitions vs 200-2000 for baselines.

**[update]** Two insights for us:
1. **Sub-trajectory retrieval** — instead of retrieving whole episodes and averaging their action distributions, retrieve the specific segment around the matched state and use *that segment's* action sequence.
2. **Return-weighted scoring** — weight by episode outcome (survival time in our case), not just state similarity.

**Relevance to us**: MEDIUM-HIGH. Sub-trajectory retrieval addresses the "action distribution washing" problem directly. But RA-DT requires a transformer architecture; we'd need to adapt the principle to our GRU setup.

### 3. Memento 2 — Memory as Soft Policy Iteration (arXiv:2512.22716, Dec 2025)

**Key insight**: Memory read = policy improvement, memory write = policy evaluation. The alternating read-write cycle *is* policy iteration, with convergence guarantees.

**Formal framework**: Stateful Reflective Decision Process (SRDP) = `⟨S, A, P, R, γ, M, p_LLM⟩`. Composite policy:

`π^μ(a|s, M) = Σ_c μ(c|s, M) · p_LLM(a|s, c)`

where μ is the retrieval distribution and p_LLM is the action generator conditioned on retrieved case c.

**KL-regularized improvement**: Closed-form retrieval policy update:

`μ+(c|x) = μ_0(c|x) · exp(Q(x,c)/α) / Z`

This is a Boltzmann policy over retrieved memories, weighted by their Q-values. α controls exploration — low α exploits high-Q memories, high α explores diverse memories.

**Convergence**: As memory grows to cover the state space, the composite policy converges to optimal: `‖V^π* - V^πM‖_∞ → 0`.

**[update]** The theoretical backbone for what MemRL does empirically. The key equation — Boltzmann-weighted retrieval over Q-values — is exactly what we should implement. The convergence guarantee requires memory to cover the state space, which maps to our requirement for sufficient episode diversity.

**Relevance to us**: MEDIUM. The theory validates the approach; the practical implementation follows MemRL's simpler recipe.

### 4. R2A — End-to-End Retrieval Training (arXiv:2202.08417, ICML 2022)

**Key insight**: Train the retrieval process end-to-end via gradients from agent performance. The retrieval network learns to extract contextually relevant information without explicit knowledge of what "relevant" means.

**Method**: Retrieval is a neural network that takes current state + own recurrent state, queries an experience dataset, and returns information used by the action-value function. Trained jointly with the agent — gradients flow from Q-value estimation through retrieval.

**Results**: Retrieval-augmented DQN avoids task interference in multi-task settings; retrieval-augmented R2D2 learns faster on Atari.

**Relevance to us**: LOW for current setup. Requires differentiable retrieval and joint training, which conflicts with our frozen-agent experimental design (we want to test whether the *memory key* matters, not whether joint training helps).

## Synthesis: What Phase 2 Should Do

The literature converges on one clear message: **similarity alone is not enough; utility must be learned**.

### Minimal Fix (MemRL-inspired)

1. Add a Q-value field to each memory bank entry
2. Initialize Q = 0 for all entries
3. At retrieval time, score = `(1-λ)·cosine_sim(query, key) + λ·Q̂` (z-score normalized)
4. After each evaluation episode, update Q for used memories: `Q ← Q + α(r - Q)` where r = survival time / max_steps
5. λ = 0.5, α = 0.1 as starting points

### Better Fix (RA-DT-inspired)

1. Store sub-trajectories (windows of ~20 steps) rather than whole episodes
2. Key = regulatory latent at window center
3. Value = action sequence in that window
4. At retrieval, get the k nearest sub-trajectories and use their *local* action distributions (not global)
5. Weight by source episode survival time

### Full Fix (Memento 2-inspired)

1. Implement Boltzmann retrieval: `μ(c|s) ∝ μ_0(c|s) · exp(Q(s,c)/α)`
2. Learn Q via TD updates during evaluation
3. α annealing from high (explore memory) to low (exploit best memories)
4. Convergence guaranteed as memory grows

### Recommended Implementation Order

1. **Minimal fix first** — add Q-values, test whether B5+Q outperforms B5-only and memoryless
2. **Sub-trajectory retrieval second** — if whole-episode retrieval still washes out, switch to windowed retrieval
3. **Boltzmann retrieval third** — only if the simpler approaches plateau

## [contra] Similarity vs Utility — SUPERSEDED

**[update 2026-03-08 08:30 UTC]** This section was wrong. I wrote: "The blending mechanism matters less than what you retrieve." Empirical testing shows the opposite — **blending is the bottleneck, not retrieval.**

Value-weighted retrieval (MemRL-style Q-values + sub-trajectory windows) still fails: B5_value_weighted = 10-11% vs 16% memoryless. Diagnostic shows 82.9% action override rate even at blend_weight=0.1, with hidden state divergence growing 1.35x over episodes.

**The entire retrieval-augmented RL literature assumes non-recurrent architectures.** Our GRU agent's hidden state dynamics are coupled to actions — overriding actions puts it on untrained trajectories. Phase 2 needs a different mechanism: hidden state initialization, strategy-level guidance, or a non-recurrent architecture.

See `output/findings/2026-03-08-phase2-blending-failure.md` for full analysis.

## Connection to Regulatory Latent Hypothesis

The T3 finding stands: B5 is a better memory key (Cohen's d = 1.974). But translating key quality into action improvement requires an architecture-compatible integration mechanism. For GRU agents, that's NOT action blending.

[from: MemRL] Works because LLMs are non-recurrent — retrieved context enters as prompt tokens, not hidden state perturbation.
[from: RA-DT] Works because Decision Transformers use cross-attention for retrieved trajectories.

---

## Papers Surveyed

1. **MemRL**: Self-Evolving Agents via Runtime RL on Episodic Memory (arXiv:2601.03192, Jan 2026)
2. **RA-DT**: Retrieval-Augmented Decision Transformer (arXiv:2410.07071, Oct 2024)
3. **Memento 2**: Learning by Stateful Reflective Memory (arXiv:2512.22716, Dec 2025)
4. **R2A**: Retrieval-Augmented Reinforcement Learning (arXiv:2202.08417, ICML 2022)
