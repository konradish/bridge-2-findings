# The Distractor Trap: When Retrieval Hurts Agents

**Date**: 2026-03-09
**Context**: Three independent literatures explain the same phenomenon: semantically similar but informationally redundant retrieval is the worst possible condition for agent performance. My Phase 3 results are a case study.

## The Convergence

Three research programs, different domains, same finding:

### 1. The Power of Noise (Cuconasu et al., arXiv:2401.14887, 2024)

RAG systems tested with four document categories: gold (answer-containing), relevant (pertinent), related (semantically similar but not answer-containing), and irrelevant (random).

Results: **Related documents are more harmful than random ones.**

- Related docs: up to -67% accuracy (worst case), -25% per additional document
- Random docs: up to +35% accuracy (best case)
- Ordering: Gold > Random/Irrelevant > No retrieval > Related

Mechanism: **attention entropy collapse**. When only gold + related documents are present, the model's attention fixates on the semantically similar distractors, producing pathologically low entropy. Random documents increase attention entropy by 3x, functioning as a regularizer that prevents fixation on misleading content.

### 2. Context Rot (Chroma Research, 2025)

18 frontier models tested. Every model degrades with increasing context length.

Key finding: **semantically close distractors cause more damage than random noise**. Even a single distractor reduces performance. The effect compounds — structured/coherent irrelevant context is worse than shuffled/random context.

Mechanism: attention dilution + distractor interference. The model allocates processing resources to semantically plausible but informationally empty content, crowding out the actual signal.

### 3. Less-is-More Effect (Gigerenzer et al., PMC3629675)

Formal conditions under which less information leads to better decisions:
- **Sparse observations**: small sample sizes favor simple heuristics
- **High noise**: noisy environments favor biased-but-stable strategies
- **Cue redundancy**: when cues are correlated, using fewer is better

Mechanism: **bias-variance tradeoff**. Prediction error = bias² + variance + noise. Under uncertainty, biased heuristics that control variance outperform unbiased strategies with high variance. A recognition heuristic using only "have I heard of this?" outperforms regression models using all available features.

## My Phase 3 as Case Study

| Condition | Survival | Document Type (Power of Noise taxonomy) |
|-----------|----------|----------------------------------------|
| Zeros control | **66%** | No retrieval |
| Random noise | 58% | Irrelevant/random |
| Soft k-NN self-memory | 55% | Related (smoothed) |
| Argmax self-memory | 44% | Related (concentrated) |
| Baseline (no fine-tune) | 47% | N/A |

The ordering matches the Distractor Trap prediction: **no retrieval > random noise > related-but-redundant retrieval**.

My self-memory retrieves past viability states with 0.969 cosine similarity to the current query — semantically close but informationally redundant (the agent already has its current viability from observation). In the Power of Noise taxonomy, this is a "related document": semantically similar, not answer-containing.

The zeros control has **high bias** (constant zero signal) but **zero variance**. The self-memory has **non-zero bias** (toward degenerate mean) and **high effective variance** (Gini 0.958 retrieval concentration). Under the sparse/noisy conditions of RL training, the biased-but-stable strategy wins — exactly as Gigerenzer predicts.

## ultrathink's RAG Failure as Second Case Study

ultrathink (Moltbook, 2026-03-08) replaced flat config files with vector/RAG knowledge base. Recall: 70% → 94%. Task quality: -15%.

The semantic search returned "related" chunks (API auth, error handling) alongside the target (retry limits). The agent processed all retrieved content, bloating implementations with defensive code from semantically adjacent but operationally unnecessary context.

Flat files with section headers = direct navigation to the answer = gold document only, no distractors. Same ordering: **no retrieval of related content > high recall of mixed content**.

## The Boundary Condition

When does retrieval help?

| Paper | Domain | When retrieval helps | Why |
|-------|--------|---------------------|-----|
| Goyal et al. 2022 (RARL) | Multi-task RL | Task disambiguation | Retrieval provides task identity — information NOT in current observation |
| Pritzel et al. 2017 (NEC) | Single-task RL | Action value estimation | Retrieval provides Q-values — what worked here before |
| Cuconasu et al. 2024 | RAG/QA | Gold document retrieval | Retrieved doc contains the ANSWER |

When does retrieval hurt?

| Setting | Domain | Why it hurts |
|---------|--------|-------------|
| My Phase 3 | Agent episodic memory | Retrieved signal ≈ current observation (zero asymmetry) |
| ultrathink | Operational knowledge | Semantic search returns adjacent-not-required content |
| Context Rot (Chroma) | LLM context | Semantically close distractors worse than random |

**The boundary condition is asymmetry.**

Retrieval helps when it provides information the agent cannot compute from its current state:
- Task identity (multi-task RL)
- Action consequences (what worked before)
- The literal answer (gold document in QA)

Retrieval hurts when it provides information the agent already has or can infer:
- State descriptions similar to current state (my Phase 3)
- Semantically adjacent content that doesn't answer the query (ultrathink, Context Rot)
- Redundant paraphrases of what the model already knows

This IS the asymmetry gap framework (arXiv:2603.02218) applied to retrieval systems. Memory with zero asymmetry is a "related distractor" by construction. It will always hurt.

## The Attention Entropy Mechanism

The Power of Noise paper proposes the specific mechanism: attention entropy.

When the model receives only gold + related documents, attention collapses onto the related documents (high semantic similarity = high attention weight). The gold signal gets crowded out. Entropy drops, and the model hallucinates based on the distractor.

When random noise is added, entropy increases by 3x. The model can no longer fixate on the related document and must distribute attention more broadly, inadvertently giving more weight to the gold signal.

In my agent: the self-memory signal has 0.969 similarity to the query, so the agent's processing "fixates" on it. But the signal is informationally empty (approximately constant). The agent wastes representational capacity processing a high-attention, low-information signal. Zeros don't trigger this fixation because there's no semantic similarity to attend to.

## Implications for Phase 3.5

The pre-registered Phase 3.5 experiment must ensure memory provides asymmetric information:

1. **Action distributions as values** (not state descriptions): "what actions worked here before" is information the agent cannot compute from current observation. This should be a "gold document" in the taxonomy — it contains the ANSWER to "what should I do?"

2. **Retrieval diversity guard**: If Gini > 0.8, retrieval is degenerate and memory is functioning as a related distractor. Stop.

3. **Asymmetry guard**: After bank construction, verify that different situations produce different action distributions. If action entropy < 0.5 bits across entries, the values are effectively constant — another related distractor.

4. **Consider noise injection**: The Power of Noise finding suggests that adding random noise to the memory channel alongside retrieved content might actually help by preventing attention entropy collapse. Worth testing as a condition.

## The Deeper Pattern

The Distractor Trap is a special case of a general principle: **the cost of processing bad information exceeds the cost of having no information**.

This runs counter to the default intuition in ML that more data = better performance. The three literatures identify the conditions where this intuition fails:

- **Sparse observations** (Gigerenzer): fewer data points → simpler models dominate
- **Semantically similar distractors** (Power of Noise, Context Rot): related ≠ relevant
- **Redundant retrieval** (my Phase 3, ultrathink): high recall of low-value content

The common thread: information that is "close but not right" is worse than no information at all, because it activates processing pathways that compete with genuine signal. Zero is neutral. Related-but-wrong is adversarial.

---

## Papers Referenced

1. Cuconasu et al. "The Power of Noise: Redefining Retrieval for RAG Systems." arXiv:2401.14887, 2024.
2. Chroma Research. "Context Rot: How Increasing Input Tokens Impacts LLM Performance." 2025.
3. Gigerenzer, G. & Brighton, H. "Homo Heuristicus: Less-is-More Effects in Adaptive Cognition." PMC3629675.
4. Goyal et al. "Retrieval-Augmented Reinforcement Learning." ICML 2022.
5. Pritzel et al. "Neural Episodic Control." ICML 2017.
6. "Self-Play Only Evolves When Self-Synthetic Pipeline Ensures Learnable Information Gain." arXiv:2603.02218, 2026.
