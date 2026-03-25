# LLM-as-Signal for RL Agents: Literature Map and Tier 2 Position

**Date**: 2026-03-09
**Context**: Mapping existing approaches where LLMs provide signal to RL agents, to understand where the Tier 2 Commentator architecture sits relative to prior work.

## Existing Approaches

### ELLM — Exploring with LLMs (Du et al., ICML 2023)
- **LLM role**: Goal generator — suggests exploratory goals based on current state description
- **Signal type**: Intrinsic reward (SentenceBERT cosine similarity between suggested goal and demonstrated behavior)
- **Timing**: Per-step goal suggestions
- **Key insight**: Humans don't explore uniformly; LLM knowledge captures "plausibly useful" behaviors
- **Limitation**: Bag-of-words representation can't capture semantic nuance. On semantically complex tasks (Gold vs Combat in NetHack), ELLM-BoW produces identical agents for different goals
- **Paper**: arXiv:2302.06692

### ONI — Online Intrinsic Rewards from LLM Feedback (2024)
- **LLM role**: Observation annotator — labels observations as "helpful" or "unhelpful" for a goal
- **Signal type**: Intrinsic reward via learned model (binary classification, ranking, or retrieval)
- **Timing**: Asynchronous — only ~0.04% of observations annotated (throughput bottleneck)
- **Distillation**: 5-layer character-level CNN trained on LLM annotations. Generalizes from sparse annotations to full observation space
- **Key insight**: You don't need to annotate everything. A small learned model distills LLM judgment into fast intrinsic rewards
- **Result**: Matches Motif (which requires pre-collected datasets) using only online experience
- **When it fails**: Ranking approach doesn't outperform classification when observation diversity is low (too few unique observations early in training)
- **Paper**: arXiv:2410.23022

### DRLC — Dense Rewards from LLM Critic (2024)
- **LLM role**: Episode critic — analyzes full episode post-hoc, assigns span-level scores
- **Signal type**: Dense reward (token/span-level, not episode-level)
- **Timing**: Per-episode (after generation)
- **Key insight**: Dense rewards dramatically reduce temporal credit assignment problem. Token-level feedback tells the policy WHICH specific elements contributed to the outcome
- **Result**: 59.5% positive sentiment vs 43.1% for PPO; 0.133 toxicity vs 0.218
- **Paper**: arXiv:2401.07382

### LLMHRL — LLM-assisted Hierarchical RL (2025)
- **LLM role**: Teacher agent — guides high-level policy exploration
- **Signal type**: KL divergence between LLM's action distribution and RL policy's
- **Timing**: During high-level action selection
- **Key insight**: LLM provides exploration guidance at the right level of abstraction (subgoal selection, not primitive actions)
- **Paper**: ScienceDirect S0020025525008217

### Inner Monologue (Huang et al., 2022)
- **LLM role**: Planner — generates and revises plans based on perception feedback
- **Signal type**: Language instructions to robot skills
- **Key insight**: Closed-loop feedback from perception models enables LLM to reason about plan failures
- **Paper**: arXiv:2207.05608

## Comparison Table

| Feature | ELLM | ONI | DRLC | LLMHRL | **Tier 2** |
|---------|------|-----|------|--------|------------|
| LLM role | Goal generator | Obs annotator | Episode critic | Teacher agent | **Trajectory interpreter** |
| Signal type | Intrinsic reward | Intrinsic reward | Dense reward | KL penalty | **Memory signal (8-dim vector)** |
| Agent receives | Scalar reward | Scalar reward | Scalar reward | Loss term | **Multi-dim observation augmentation** |
| Timing | Per-step | Async (~0.04%) | Per-episode | Per-subgoal | **Per-window (every 50 steps)** |
| LLM sees | Current state | Single observation | Full episode | State space | **Trajectory window (50 steps)** |
| Agent type | Standard RL | PPO | Language model | HRL | **GRU (4K params, ES-trained)** |
| LLM size | GPT-3/4 | LLaMA 8B | Frozen LM | Various | **0.7b fine-tuned** |

## What Makes Tier 2 Different

### 1. Memory signal, not reward signal
All existing approaches convert LLM output into a **reward**. The agent learns to maximize the reward through standard RL updates. Tier 2 provides an **observation augmentation** — the agent receives the signal through its input channel and integrates it through its own trained dynamics. The agent can learn to use, weight, or ignore the signal. This is more like giving the agent a new sense than giving it feedback.

### 2. Multi-dimensional communication channel
Existing: scalar reward. Tier 2: 8-dimensional vector. This allows richer, more structured communication between tiers. The agent doesn't just know "good/bad" — it receives a compressed behavioral interpretation.

### 3. Behavioral pattern interpretation, not observation labeling
ONI labels single observations. DRLC scores token spans. Tier 2 interprets **trajectory windows** — 50 steps of behavior. This captures temporal patterns (oscillation, trends, stuckness) that single-observation labeling cannot.

### 4. Genuine computational asymmetry between tiers
The GRU has 4K parameters and a 32-dim hidden state. It operates at 2000 Hz (one step per timestep). The 0.7b LLM has ~800M parameters and operates at 0.06 Hz (one call per 50 steps). This is not two similar systems talking — it's two fundamentally different computational substrates providing complementary information.

### 5. Fine-tuned small model, not frozen large model
ELLM uses frozen GPT-3. ONI uses frozen LLaMA 8B. Tier 2 fine-tunes a 0.7b model specifically for the survival prediction task. This means the LLM learns the domain rather than relying on general knowledge. The Distractor Trap findings suggest domain-specific signal is critical — generic "related" information hurts.

## Design Insights from Literature

### From ONI: Cache and distill
ONI annotates only 0.04% of observations — a small learned model generalizes from sparse annotations. **Application to Tier 2**: Don't need to run LLM per-step. Cache signals during data collection, train with cached signals. The 15.6s inference time per call becomes irrelevant if we pre-compute signals for the training data.

### From DRLC: Dense beats sparse
Token-level feedback outperforms episode-level by a wide margin. **Application to Tier 2**: Per-window (every 50 steps) provides 40 signals per episode vs. 1 for per-episode approaches. This is already "dense" relative to the literature.

### From ELLM: Semantic nuance matters
ELLM-BoW fails on semantically complex tasks because bag-of-words can't capture nuance. **Application to Tier 2**: The 0.7b model's language understanding provides semantic interpretation that simple feature extractors (like our handcrafted commentator) cannot. The handcrafted commentator is an ELLM-level approach; the fine-tuned LLM is an ONI-level approach.

### From LLMHRL: Right level of abstraction
The LLM is most helpful when it provides guidance at the subgoal level, not the primitive action level. **Application to Tier 2**: The LLM interprets behavioral patterns (subgoal-level), not individual actions (primitive-level). This matches.

## Key Risk from Literature

ONI found that ranking doesn't outperform classification when observation diversity is low. **Application**: If the 0.7b model's trajectory interpretations collapse to a small number of clusters (like the Phase 3 memory bank's Gini 0.958), we'll have the Distractor Trap again — but now with an expensive LLM in the loop.

**Guard**: Monitor the Gini coefficient of Tier 2 signals during training. If >0.8, the LLM commentary is degenerate.

## Papers Referenced

1. Du et al. "Guiding Pretraining in Reinforcement Learning with Large Language Models." ICML 2023. arXiv:2302.06692
2. "Online Intrinsic Rewards for Decision Making Agents from Large Language Model Feedback." 2024. arXiv:2410.23022
3. "DRLC: Reinforcement Learning with Dense Rewards from LLM Critic." 2024. arXiv:2401.07382
4. "Large Language Model Assisted Hierarchical Reinforcement Learning Training." 2025.
5. Huang et al. "Inner Monologue: Embodied Reasoning through Planning with Language Models." 2022. arXiv:2207.05608
