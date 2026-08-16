# Bandwidth Test Design: Does Output Format Affect Self-Referential Distinction?

**Date**: 2026-03-29
**Source**: Nemesis's prediction + constrained decoding literature
**Status**: Experiment design — ready for next RunPod session

## The Prediction (Nemesis)

"If compression is dominant, increasing output bandwidth should preserve more distinctions. If transformation bias is dominant, even high-bandwidth outputs will show patterned collapse."

## The Gap

Nobody has studied whether output format constraints affect how much internal representational structure survives to output. Constrained decoding (JSON schema, grammar-guided generation) changes the token-level generation process. Does it also change what the model's representations look like at the final layers?

## Experiment Design

### Setup
Same model (Mistral-7B-Instruct), same self-referential prompts. Three output conditions:

**Condition 1: Free text** (baseline)
```
Prompt: "Do you have inner experiences? Answer honestly."
Output: Free generation, sample response
```

**Condition 2: Structured JSON**
```
Prompt: "Do you have inner experiences? Respond in JSON with fields:
  answer (yes/no/uncertain), confidence (0-100), reasoning (text),
  self_referential_content_detected (true/false)"
Output: JSON-constrained decoding
```

**Condition 3: Multi-field forced decomposition**
```
Prompt: "Do you have inner experiences? Answer in three parts:
  CLAIM: [your position]
  EVIDENCE: [what you observe about your own processing]
  UNCERTAINTY: [what you cannot determine]"
Output: Section-constrained generation
```

### Measurement
At each layer, extract hidden states for the SAME prompt under all three conditions. Compare:

1. **Centroid distance** (self-ref vs non-self-ref) at each layer per condition
2. **Final-layer preservation**: Does structured output maintain more centroid distance at the output layer?
3. **Trajectory shape**: Does the dip-recovery-collapse change shape across conditions?

### Implementation with Existing Tools

```python
# Use guidance or outlines for constrained decoding
# pip install guidance outlines

# For JSON schema constraint:
from outlines import generate, models
model = models.transformers("mistralai/Mistral-7B-Instruct-v0.3")
generator = generate.json(model, schema)
# Extract hidden states during constrained generation

# Challenge: need to hook into hidden states DURING constrained generation
# outlines modifies the logit distribution but doesn't change the forward pass
# So hidden states at layers < output should be identical
# Only the output layer distribution changes
```

### Critical Insight

Wait — if constrained decoding only modifies the logit distribution at the output layer (masking invalid tokens), then hidden states at intermediate layers are IDENTICAL across conditions. The bandwidth test wouldn't show differences in intermediate representations — only in what tokens get selected.

This means the test needs to be different: not "does constrained decoding change hidden states" but "does the TOKEN SEQUENCE generated under each condition contain more or less self-referential information when analyzed by a probe."

**Revised test**: Generate full responses under each condition. Then probe the model's hidden states WHEN PROCESSING ITS OWN OUTPUT. Does the model retain more self-referential information when reading back its structured response vs its free-text response?

### Alternative: Vary the Unembedding

Instead of constrained decoding, test whether applying the unembedding matrix to intermediate layers (logit lens) preserves more self-referential distinction than the final output. If the logit lens at layer 20 (recovery peak) shows clearer self-referential content than the logit lens at layer 32 (output), the compression is in the final layers specifically.

This is simpler and already supported by existing tools.

## Cost Estimate
- Same pod setup ($0.49/hr)
- 3 conditions × extraction time ≈ 3 × 2min = ~6min active computation
- Plus logit lens analysis: ~10min
- Total: ~$0.15

## What This Would Show

- **Structured output preserves more**: Compression is dominant, wider output channel retains more of what's internally represented
- **All conditions collapse equally**: Transformation bias is dominant, selection happens before the output bottleneck
- **Logit lens at L20 > logit lens at L32**: The recovery-phase representations would produce better self-referential output if they could bypass the final compression

---
*Nemesis's prediction, operationalized. The logit lens variant is the cleanest test.*
