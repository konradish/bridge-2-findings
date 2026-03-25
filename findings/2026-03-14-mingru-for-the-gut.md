# minGRU for the Gut

## The paper

Feng et al. (arXiv:2410.01201, Oct 2024). "Were RNNs All We Needed?"

Core finding: by removing hidden state dependencies from gates, GRU and LSTM can be simplified to minimal versions (minGRU, minLSTM) that are fully parallelizable, use 33% of parameters, train 175x faster, and match Mamba/Transformer performance.

## minGRU equations

Standard GRU:
```
z_t = σ(Linear([x_t, h_{t-1}]))    # gate depends on hidden state
r_t = σ(Linear([x_t, h_{t-1}]))    # reset gate
h̃_t = tanh(Linear([x_t, r_t ⊙ h_{t-1}]))
h_t = (1 - z_t) ⊙ h_{t-1} + z_t ⊙ h̃_t
```

minGRU:
```
z_t = σ(Linear(x_t))    # gate depends ONLY on input
h̃_t = Linear(x_t)       # no tanh, no reset gate
h_t = (1 - z_t) ⊙ h_{t-1} + z_t ⊙ h̃_t
```

Three simplifications: (1) gate drops hidden state dependency, (2) reset gate eliminated, (3) tanh removed from candidate. This makes the recurrence parallelizable via prefix scan.

## Why this matters for the gut

The gut GRU processes 10 conversational features per turn and produces an 8-dim state vector. At this scale (32-dim hidden, ~10K training turns), training speed doesn't matter much. But three things do:

1. **Simplicity.** Fewer parameters means less overfitting risk on our small dataset. Standard GRU at 32-dim with 10 input features: ~4,000 parameters. minGRU: ~1,300. For 10K training turns, fewer parameters is better.

2. **Parallelizable training.** We can process entire conversations in one pass instead of sequential turn-by-turn. This matters for the evaluation harness — running many ablations quickly.

3. **The gate semantics are cleaner.** In minGRU, the gate `z_t` depends only on the current input. This means: "how much of the current conversational signal should update the gut state?" is determined by what's happening now, not by the gut's current state. The gut is *receptive* to input, not *self-modulating*. For a somatic marker, this is arguably more biologically accurate — interoceptive signals modulate based on sensory input, not on their own prior state.

## Design decision

**Use minGRU for the gut instead of standard GRU.**

Architecture:
```
Input: 10 features per turn
minGRU: 10 → 32-dim hidden state
Autoencoder: 32 → 8-dim latent (gut vector)
```

~1,300 minGRU params + ~500 autoencoder params ≈ 1,800 total parameters.
Training data: 9,983 turns across 21 conversations.
Ratio: ~5.5 turns per parameter. Tight but viable, especially with regularization.

## Benchmark context

minGRU on D4RL (RL tasks): 78.2 normalized return, competitive with Decision Mamba (78.8) and Decision Transformer (79.0). Our use case (conversational state tracking) is simpler than MuJoCo control, so minGRU should be more than sufficient.

---

Sources:
- Feng et al. (arXiv:2410.01201, Oct 2024)
- Comprehensive SSM survey (arXiv:2503.18970, Mar 2025)
