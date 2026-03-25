# Phase 2 Blending Is Fundamentally Broken for Recurrent Agents

**Date**: 2026-03-08
**Context**: Phase 2 retrieval-guided action selection fails across all conditions — naive cosine similarity (v1), value-weighted retrieval (v2), sub-trajectory retrieval — all perform at or below memoryless baseline.

## The EXPLORE Finding (Earlier Today)

Surveyed 4 papers (MemRL, RA-DT, Memento 2, R2A). Concluded the problem was *retrieval quality* — cosine similarity doesn't evaluate utility. Built value-weighted retrieval with Q-learning on memory entries.

**Result**: Still doesn't work. B5_value_weighted = 10-11% survival. Memoryless baseline = 16%.

## The Actual Problem: Blending Disrupts Hidden State Dynamics

Diagnostic results (100 episodes, blend_weight=0.3):

| Metric | Value |
|--------|-------|
| **Action override rate** | **82.9%** |
| Hidden state divergence (mean relative) | 36.2% |
| Hidden state divergence (final) | 45.9% |
| Divergence growth (final/early) | 1.35x |
| Survival — base agent | 10% |
| Survival — blended agent | 6% |

**Even at blend_weight=0.1**, the override rate is 82.2% and survival drops from 18% → 10%.

### Why the override rate is so high

The GRU agent's policy is **peaked** — at any given hidden state, the softmax over action logits concentrates probability mass on 1-2 actions. When you mix in a uniform-ish retrieval prior at even 10% weight, you create enough probability mass on other actions that random sampling frequently selects a different action.

With 7 actions and a peaked policy (~60% on the preferred action):
- Base: 60% chance of preferred action
- Blended (0.1): 0.9×0.60 + 0.1×0.14 = 55.4% on preferred
- But the *other* 6 actions go from ~6.7% each to ~7.4% each
- Over 2000 steps, the agent takes ~1660 different-from-preferred actions vs ~1480 without blending

### Why hidden state diverges

The GRU's hidden state at time t is:
```
h_t = GRU(obs_t, h_{t-1})
```

The observation `obs_t` depends on the action taken at t-1 (movement changes position, position determines what's observed). When blending changes the action, the next observation is one the hidden state wasn't "expecting." Over hundreds of steps, the hidden state trajectory drifts into regions the agent was never trained to handle.

**Divergence grows 1.35x from step 100 to end** — the drift compounds.

### [contra] Updating my EXPLORE finding

I wrote earlier: "The problem is retrieval, not blending."

**The problem IS blending**, at least for recurrent agents. Even with perfect retrieval (oracle telling you exactly the right action distribution), mixing it with a GRU policy via softmax blending will:
1. Override ~80% of actions
2. Push the hidden state off its trained manifold
3. Compound errors over the episode

The retrieval quality finding (B5 > B4 for similarity, T3 Cohen's d = 1.974) still holds. But translating retrieval quality into action improvement requires a different mechanism than blending.

## What Phase 2 Actually Needs

For recurrent agents, you **cannot blend at the action level**. The hidden state dynamics are coupled to the action sequence. Alternatives:

### 1. Hidden State Initialization (Most Promising)
Use retrieved episodes to *warm up* the GRU hidden state at episode start, not to override actions during execution. Find episodes where the agent survived from similar regulatory states and initialize `h_0` from their hidden state trajectories.

### 2. Strategy-Level Guidance
Instead of blending individual actions, use retrieved episodes to select a high-level strategy (e.g., "seek food in quadrant 3" vs "flee hazards"). This is the Option/HRL approach — memory selects the macro-action, the GRU handles micro-actions.

### 3. Retrain with Memory Channel
Add retrieved episode information as an input to the GRU (additional observation channels). Train the agent to *use* memory from scratch. This is R2A's approach — end-to-end training with retrieval. But it breaks our experimental design (we want to test the *key* quality, not the training procedure).

### 4. Non-Recurrent Architecture
Switch to a transformer (like RA-DT) where past context enters via cross-attention, not via recurrent hidden state. Action changes don't compound through the state trajectory.

## Implications for the Regulatory Latent Hypothesis

The T3 finding stands: B5 is a better memory key (Cohen's d = 1.974).

But the *utility* of that better key depends on the action integration mechanism. For GRU agents, the path forward is hidden state initialization or strategy-level guidance, not action blending.

**The regulatory latent tells you WHERE the agent is (internal state space). It doesn't tell you WHAT to do from there — that's the GRU's job, and the GRU needs to do it with its own hidden state intact.**

## Connection to Literature

[from: MemRL] Works because the base agent is an LLM — a non-recurrent architecture where retrieved context enters as additional prompt tokens, not as hidden state perturbation.

[from: RA-DT] Works because the Decision Transformer conditions on retrieved trajectories via cross-attention, keeping the agent's own processing path intact.

[from: Memento 2] The convergence guarantee assumes the agent can condition on retrieved cases. For a GRU, "conditioning" = changing actions, which breaks the hidden state trajectory.

**The entire retrieval-augmented RL literature assumes non-recurrent or attention-based architectures.** Our GRU agent is the wrong substrate for action-level blending.

---

**Artifacts**: `value_weighted_retrieval.py`, `diagnose_blending.py`
**Data**: `runs/es_100pop_200gen/phase2_v2_results.json`, `runs/es_100pop_200gen/blending_diagnostic.json`
