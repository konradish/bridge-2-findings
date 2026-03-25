# Why Retrieval Failed and How to Fix It: Lessons from NEC, HAMI, and Lampinen et al.

**Date**: 2026-03-08
**Context**: Phase 3 self-memory retrieval is degenerate — 9 of 50 entries used, Gini 0.958, near-constant signal. Self-memory (44%) loses to zeros (66%) and random (58%). Three literatures diagnose the specific failures and suggest fixes.

## Diagnosis: Three Failures Compounding

### Failure 1: Hand-crafted keys don't discriminate

My retrieval key: 9-dim vector = [mean(energy), mean(integrity), mean(thermal), min(energy), min(integrity), min(thermal), std(energy), std(integrity), std(thermal)] over a 20-step window.

**Problem**: Most viability states look similar in this space. An agent at energy=75 heading toward food and an agent at energy=75 fleeing a hazard have nearly identical keys. The key encodes WHERE you are in viability space but not WHAT is happening or WHAT you should do.

**NEC's solution** (Pritzel et al. 2017): Learn the embedding end-to-end. The CNN embedding h = φ(o) is trained so that states requiring different actions produce different keys. Keys are task-relevant by construction — backpropagation through the DND ensures the embedding space supports good action selection.

### Failure 2: Argmax retrieval collapses diversity

My retrieval: `best_idx = argmax(cosine_similarities)`. Winner-take-all.

**Problem**: When many keys have similar similarity (0.968-0.972 in my case), the same entry wins every time. Small numerical differences determine which of ~9 entries gets selected. The memory bank effectively has 9 entries, not 50.

**NEC's solution**: Weighted sum over k-nearest neighbors with inverse-distance kernel:
```
w_i = k(h, h_i) / Σ_j k(h, h_j)    where k(h, h_i) = 1/(||h - h_i||² + δ)
output = Σ_j w_j v_j
```
The δ constant prevents total concentration on nearest neighbor. All k neighbors contribute. With k=50 (my bank size), every entry contributes SOMETHING, weighted by distance. Diversity is structural.

### Failure 3: Compressed representations aren't actionable

My memory values: 8-dim autoencoder latent encoding "what the agent's hidden state looked like during a past episode." This is descriptive — it says what WAS happening, not what SHOULD happen.

**Lampinen et al. (2025)**: "Episodic memory enables flexible reuse by reinstating full original contexts." They use raw experiences, not compressed summaries. Compression loses exactly the information needed for flexible reuse.

**NEC's solution**: Store Q-values as memory values — directly actionable signals. What you retrieve IS the action-value estimate.

**Critical insight from Lampinen**: "Models must learn HOW to use retrieved information." In-context learning during training is necessary — retrieval-augmented models trained without ICL exemplars achieve only 6-12%. My agent trained with a near-constant signal never learned to USE diverse memory, because it never experienced diverse memory.

## Three-Failure Interaction

The failures compound:
1. Coarse keys → many situations map to same region → argmax picks same entry
2. Argmax → diversity collapses → signal is near-constant
3. Near-constant signal → agent never learns to use DIVERSE memory → even if you fix retrieval, the policy isn't trained for it

This is why "more episodes" won't help — it adds entries that never get retrieved (same coarse keys, same argmax collapse). And why the agent co-adapts to a near-constant bias rather than learning situation-specific memory use.

## Redesign Principles

### Principle 1: Keys must encode DYNAMICS, not just STATE (from NEC)

Options (ascending ambition):
- **Quick fix**: Add temporal derivatives (Δenergy, Δintegrity, Δthermal over last 20 steps), action distribution entropy, and recent action histogram to the key. Goes from 9-dim to ~20-dim with more discriminating features.
- **Better**: Use the GRU hidden state directly as the key (32-dim, already encodes temporal context). This is what NEC does with its learned embedding.
- **Best**: Learn the key embedding end-to-end (requires differentiable retrieval, more complex training).

### Principle 2: Retrieval must be SOFT, not HARD (from NEC)

Replace argmax with weighted k-NN:
```python
def retrieve_soft(self, query, k=10, delta=1e-3):
    dists = np.sum((self.keys - query)**2, axis=1)  # L2 squared
    # Select k-nearest
    topk = np.argpartition(dists, k)[:k]
    weights = 1.0 / (dists[topk] + delta)
    weights /= weights.sum()
    return (weights[:, None] * self.values[topk]).sum(axis=0)
```
This ensures the output varies continuously with the query, even when many entries are similar.

### Principle 3: Values must encode GUIDANCE, not DESCRIPTION (from Lampinen + NEC)

Options:
- **Action distribution**: Store the agent's softmax output (7-dim) at each timestep. Retrieved value = "what I did in this situation." More actionable than "what my hidden state looked like."
- **Value estimate**: Store cumulative future reward (NEC-style). Retrieved value = "how good was this situation."
- **Raw hidden state**: Store h directly (32-dim). Reinstates full context rather than compressed summary.

### Principle 4: Train with DIVERSE retrieval from the start (from Lampinen)

The agent must experience diverse memory signals during training, or it will never learn to use them. This means:
- Larger memory bank built from MORE episodes before fine-tuning begins
- Richer keys that produce diverse retrievals
- Possibly: curriculum that starts with strong (oracle) memory and fades to realistic retrieval

## What This Changes About Phase 3

The Phase 3 pipeline (collect → encode → fine-tune) is structurally correct. Local Consistency still matters. Self-memory is still the right constraint. But the implementation details are wrong:

| Component | Current (broken) | Redesigned |
|-----------|-----------------|------------|
| Keys | 9-dim viability summary | GRU hidden state (32-dim) or enriched features |
| Retrieval | Cosine + argmax | L2 + weighted k-NN (NEC-style) |
| Values | Autoencoder latent (8-dim) | Action distribution (7-dim) or raw hidden (32-dim) |
| Bank size | 50 episodes | 200+ episodes |
| Signal dim | 8 | 7 (actions) or 32 (hidden) — adjust agent input dim |

The simplest test: keep everything else the same but replace argmax with weighted k-NN. If retrieval diversity increases and the signal varies across situations, the zeros control advantage should shrink.

## Connection to HAMI

HAMI (2025, Nature Scientific Reports) adds another dimension: **symbolic indexing**. Instead of continuous similarity search, HAMI assigns compact symbolic indices (inspired by hippocampal CA3 region) and retrieves by exact match + hierarchical refinement. This is more computationally efficient and naturally avoids soft-retrieval concentration issues.

For my small bank (50-200 entries), this isn't necessary. But for scaling to thousands of episodes, symbolic indexing or clustering would be essential.

## The Latent Learning Connection

Lampinen et al.'s key argument: parametric learning encodes information inseparably from training task format. Episodic memory enables "format-independent" reuse by reinstating full contexts.

My autoencoder latent IS format-dependent — it encodes hidden states in the format the autoencoder learned. When the agent encounters a new situation, the retrieved latent is in the "format" of past situations' hidden state summaries. If the situation is genuinely novel, the format mismatch makes the signal misleading.

Raw hidden states (or action distributions) avoid this: they're in the agent's own representational format, requiring no translation.

---

## Papers Referenced

1. Pritzel et al. "Neural Episodic Control." ICML, 2017.
2. Lampinen et al. "Latent learning: episodic memory complements parametric learning by enabling flexible reuse of experiences." arXiv:2509.16189, 2025.
3. HAMI framework. "A scalable RL framework inspired by hippocampal memory mechanisms." Nature Scientific Reports, 2025.
4. Gershman & Daw. "RL and episodic memory in humans and animals." Annual Review of Psychology, 2017.
