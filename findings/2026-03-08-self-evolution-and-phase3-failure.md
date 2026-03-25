# Why Self-Memory Failed: The Asymmetry Gap and Self-Evolution Limits

**Date**: 2026-03-08
**Context**: Phase 3 self-memory (44%) lost to zeros (66%). The self-evolution literature explains why and what would fix it.

## The Asymmetry Gap (arXiv:2603.02218, March 2026)

Self-play/self-evolution works when the generated data contains **learnable information** the system can't already access. This is formalized as the "asymmetry gap" — the computational difference between generating and verifying a solution.

Data must be in a "Goldilocks Zone":
- **Too simple** (below zone): The system already knows this → no learning signal
- **Too complex** (above zone): Unlearnable noise → no useful gradient
- **Goldilocks**: Structured enough to learn, complex enough to be non-trivial

### My memory signal is BELOW the Goldilocks Zone

The memory retrieves compressed past viability states. But the agent already has its CURRENT viability state from the 5-dim observation. The 9-dim query space is so coarse that:

```
retrieved_viability ≈ current_viability
```

There is **no asymmetry** — the memory doesn't provide information the agent can't already infer from its current observation. The signal is approximately constant because most situations map to the same few memory entries, which encode approximately the same viability summary the agent already sees.

For self-memory to have positive asymmetry, it must encode information **beyond the current observation horizon**:
- **Temporal**: What happened 100+ steps ago (beyond GRU memory capacity)
- **Counterfactual**: What happened when I took action X in state Y (action consequences)
- **Spatial**: Resource/hazard locations beyond current field of view
- **Strategic**: Which behavioral patterns led to survival vs death

My autoencoder latent encodes none of these. It compresses the hidden state, which is itself a summary of recent observations — information the agent already has.

## Self-Play Collapse Mechanism

The paper identifies **information starvation**: when self-synthetic data repeatedly samples structurally similar directions without introducing asymmetry, the system converges on memorization rather than learning.

My Phase 3 exhibits exactly this:
1. Collect episodes from Stage 1 agent
2. Encode with autoencoder → compressed descriptions of what the agent already experienced
3. Retrieve during Stage 3 → same compressed descriptions, approximately constant
4. Agent memorizes a near-constant bias rather than learning to use diverse episodic information

The iteration plan (re-collect → retrain AE → re-fine-tune) would make this WORSE — each iteration trains on increasingly self-referential data without introducing new information.

## Conditions for Stable Self-Evolution

The asymmetry gap paper identifies three requirements:

### 1. Asymmetric co-evolution
Memory must provide information the policy can't generate itself. This means the memory CONTENT must differ from the current observation in computationally meaningful ways.

**My failure**: Memory content ≈ compressed current state. No asymmetry.
**Fix**: Store action consequences, not state descriptions. "Last time energy was here, I ate and survived for 500 more steps" vs "last time energy was here, the hidden state looked like [0.3, -0.1, ...]."

### 2. Capacity growth across iterations
Model and memory capacity must expand. Static capacity with more iterations = diminishing returns.

**My failure**: Same 8-dim memory channel, same 50-entry bank, same 9-dim query.
**Fix**: Increase memory dimensionality, bank size, and query richness across iterations.

### 3. Proactive information seeking
Generate queries from failures — what memory would have prevented this death?

**My failure**: Memory bank is collected from ALL episodes uniformly. Deaths and survivals contribute equally.
**Fix**: Weight bank entries by outcome quality. Deaths are MORE informative than survivals (they reveal what NOT to do). Or: specifically collect memory from situations that precede deaths.

## Limits of Self-Improvement (arXiv:2601.05280)

Key conditions for self-improvement to work:
1. **External validation** ✅ (survival is ground truth)
2. **Non-synthetic training signals** ✅ (environment provides real rewards)
3. **Distinguishing quality of self-outputs** ❌ (autoencoder treats all episodes equally)

"Models cannot reliably distinguish high-quality from low-quality self-generated outputs." My bank contains 50 episodes: 19 survived, 31 died. The autoencoder compresses both equally. A survival-weighted bank would provide stronger signal.

## Model Collapse Risk

Recursive training on self-generated data degrades quality through:
- Distributional shift from original training data
- Accumulation of subtle errors across iterations
- Loss of nuance through successive refinement

My Phase 3 iteration would amplify the degenerate retrieval: agent trained on constant signal → generates episodes with constant-signal-shaped behavior → memory bank from those episodes → even more constant signal.

## Revised Design: Phase 3.5

Based on self-evolution principles:

| Component | Phase 3 (failed) | Phase 3.5 (proposed) |
|-----------|-----------------|---------------------|
| **Memory content** | AE latent (state description) | Action distribution + survival outcome |
| **Asymmetry source** | None (state ≈ current obs) | Counterfactual: what action worked here? |
| **Query features** | 9-dim viability summary | 32-dim hidden state + action history |
| **Retrieval** | Argmax (degenerate) | Weighted k-NN (diverse) |
| **Bank construction** | All episodes equally | Survival-weighted, death-enriched |
| **Iteration guard** | None | Diversity check: if Gini > 0.8, stop and redesign |

The critical change: memory must provide **asymmetric information** — things the agent can't compute from its current observation. State descriptions don't have this. Action-consequence pairs do.

## Connection to Broader Self-Evolution Taxonomy

From the self-evolving agents survey (arXiv:2507.21046), evolution can target:
- **Models** (weights/parameters) — my ES training does this
- **Memory** (external storage) — my self-memory bank does this
- **Tools** (capabilities) — not applicable here
- **Architecture** (structure) — not applicable here

My experiment evolves both model and memory but fails because the memory evolution doesn't produce asymmetric information. The model evolution (fine-tuning) DOES work — zeros control proves this. The failure is specifically in the memory component.

---

## Papers Referenced

1. "Self-Play Only Evolves When Self-Synthetic Pipeline Ensures Learnable Information Gain." arXiv:2603.02218, March 2026.
2. "On the Limits of Self-Improving in LLMs." arXiv:2601.05280, January 2026.
3. "Multi-Agent Evolve: LLM Self-Improve through Co-evolution." arXiv:2510.23595, 2025.
4. "A Survey of Self-Evolving Agents." arXiv:2507.21046, July 2025.
