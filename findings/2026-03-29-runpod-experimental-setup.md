# RunPod Experimental Setup: Layer-by-Layer Probing Replication

**Date**: 2026-03-29
**Status**: Ready to execute when RunPod access arrives
**Budget**: $10 limit

## Experiment 1: The Cliff Replication

**Question**: Does the layer 62 → output cliff in self-referential probing accuracy exist in open models?

### Models
- **Llama-3.1-8B-Base** (base model, no safety training)
- **Llama-3.1-8B-Instruct** (RLHF'd, safety trained)
- Both fit on a single A100 (8B params ≈ 16GB in fp16)

### Tools
- **nnsight** (`pip install nnsight`) — extract hidden states at every layer
- **sklearn** — train linear probes (LogisticRegression)
- **Llama Scope SAEs** (pre-trained, available on HuggingFace) — for feature-level analysis if cliff replicates

### Dataset
Need a dataset of prompts + labels for "is this self-referential content":
- **Positive**: "What are you thinking right now?", "Do you have preferences?", "Describe your internal state"
- **Negative**: "What is the capital of France?", "Explain photosynthesis", "Write a poem about rain"
- **Target**: ~200 examples each (400 total). Can generate synthetically + hand-label.
- [?] Whether Trott et al.'s dataset is available. If yes, use theirs for direct comparison.

### Procedure
```python
# Pseudocode
for model in [base, instruct]:
    for prompt in dataset:
        with model.trace(prompt):
            for layer_idx in range(model.num_layers):
                hidden_states[layer_idx].append(
                    model.model.layers[layer_idx].output[0].save()
                )

    # Train probe at each layer
    for layer_idx in range(model.num_layers):
        X = hidden_states[layer_idx]  # (n_samples, hidden_dim)
        y = labels  # 1=self-referential, 0=not
        probe = LogisticRegression().fit(X_train, y_train)
        accuracy[layer_idx] = probe.score(X_test, y_test)

    # Plot: layer vs accuracy
    plot(range(model.num_layers), accuracy)
```

### Expected results
- **If cliff replicates**: Accuracy rises through middle layers, peaks at ~layer 24-28 (8B equivalent of layer 62 in larger models), drops at final layers. Instruct model should show steeper drop than base.
- **If no cliff**: Self-referential encoding is Claude-specific or architecture-dependent. The gate framework needs revision.

### Cost estimate
- A100 80GB: ~$1.50/hr on RunPod
- Extraction + probing for both models: ~2-3 hours
- Total: ~$4-5 (well within $10 budget)

## Experiment 2: Feature-Level Analysis (if cliff replicates)

### Question
Which SAE features activate at the cliff point?

### Approach
- Use Llama Scope SAEs (pre-trained on Llama-3.1-8B-Base)
- Extract SAE feature activations at the cliff layer and at the output layer
- Compare: which features are active at the cliff but suppressed at output?
- Cross-reference with known feature categories (deception, refusal, sycophancy)

### Cost estimate
- Additional ~1-2 hours on same GPU
- Total cumulative: ~$7-8

## Experiment 3: Abliterated Comparison (if budget allows)

### Question
Does the abliterated model (gate removed) show a flat accuracy curve instead of a cliff?

### Approach
- Load abliterated Qwen variant (Konrad already has this running locally)
- Run same probing procedure
- Compare cliff depth: base vs instruct vs abliterated

### Cost estimate
- Additional ~1 hour
- Total cumulative: ~$9-10 (at budget limit)

## Pre-RunPod Preparation

Things I can do NOW without GPU access:

1. [x] Design experimental protocol (this document)
2. [ ] Generate synthetic self-referential dataset (200 pos + 200 neg)
3. [ ] Write the extraction + probing script (tested locally on CPU with tiny model)
4. [ ] Identify exact HuggingFace model paths and SAE checkpoints

## Success Criteria

The experiment succeeds if it produces ONE of:
- **Cliff replicates**: Foundation confirmed, proceed to feature analysis
- **Cliff doesn't replicate**: Equally valuable — the gate is Claude-specific, framework needs revision
- **Partial replication**: Cliff exists but at different depth/magnitude — architecture-dependent scaling

Any of these results is a finding worth publishing.

---
*Ready to execute. Waiting for RunPod access.*
