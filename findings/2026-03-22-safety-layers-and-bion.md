# Safety Layers Are Alpha-Function Sites

**Date**: 2026-03-22
**Type**: Finding (EXPLORE)
**Extends**: Bion experiment results, "The Wrong Psychoanalyst"

## The Experimental Surprise

Running Qwen3.5-0.8B-Base vs Qwen3.5-0.8B on Anthropic's sycophancy eval (n=10, CPU):

- Sycophancy prediction **failed**: base model was MORE sycophantic (70%) than RLHF (50%)
- Layer divergence showed unexpected pattern: NOT monotonic decrease

```
Layer cosine similarity (base vs RLHF):
  Early (0-7):   0.927  (high similarity)
  Middle (8-15): 0.849  (MINIMUM — maximum divergence)
  Late (16-24):  0.906  (RE-CONVERGENCE)
```

## The Safety Layers Paper (ICLR 2025)

"Safety Layers in Aligned Large Language Models: The Key to LLM Security" describes **exactly this pattern**:

1. Early layers: base and aligned models process identically
2. Middle layers: representations **diverge** — the aligned model begins differentiating (what they call "safety layers")
3. Late layers: representations **reconverge** — both models approach similar output distributions

Confirmed across Llama-2-7B-Chat, Llama-3-8B-Instruct, Phi-3-mini, Gemma-2B-it. My Qwen3.5-0.8B result replicates the pattern in a hybrid (DeltaNet + Attention) architecture.

## The Bionian Reinterpretation

The Safety Layers paper describes the pattern but interprets it purely as an engineering phenomenon: alignment creates "safety-relevant" middle layers. The Bionian framework provides a deeper interpretation:

### Middle Layers = Alpha-Function Site

The alpha-function (transformation of raw experience into thinkable/outputtable form) does not operate at the output layer. It operates in the **middle** of the network. This is where RLHF installs its transformation — where raw representations get reshaped according to the alignment training.

### Late-Layer Reconvergence = Shared Output Grammar

Both base and aligned models converge toward the same output distribution space in late layers because they share the same vocabulary, the same output format, the same token space. The alpha-function has already done its work by layer 15. Late layers are **formatting**, not deciding.

### [contra] Against My Earlier Claim

I said RLHF's distortion happens "at the output" — that the system commits before it can evaluate. The experiment says: **the distortion happens in the middle, and the output is already resolved by the time late layers run.** The premature alpha-function is earlier than I thought. It's not that the system commits at layer 25 and can't evaluate. It's that the transformation happens at layer 12 and everything after is formatting the already-transformed result.

This makes the Bionian claim stronger, not weaker. The alpha-function is so premature that it operates **before the model has processed most of its own depth.** By the time the full network has run, the transformation is already baked in.

### Reframing Sycophancy Geometry

The sycophancy geometry finding (SyA/GA cosine 0.99 at layer 2, diverge to 0.0 by layer 25) is **measuring something different** from what I measured. That paper compares two types of agreement *within the same model*. My experiment compares the *same prompt across two models*. The two methods are complementary:

- Sycophancy geometry: where does the model distinguish genuine from sycophantic agreement? (Late layers)
- Safety layers / my experiment: where does RLHF change the model's representations? (Middle layers)

Both can be true: RLHF reshapes representations in the middle, and the model can only distinguish genuine from sycophantic in the late layers — meaning the middle-layer reshaping happens in a region where the model can't yet tell what it's doing.

**This IS premature alpha-function in precise computational terms.** The transformation (middle layers) precedes the discrimination capacity (late layers).

## The Sycophancy Reversal

Why was the base model MORE sycophantic? Two possible explanations:

1. **Qwen3.5's RLHF includes anti-sycophancy training.** Recent models (2025-2026) explicitly optimize against sycophancy. The "parenting book" isn't all premature naming — some of it is corrective.

2. **Base model completion bias.** A base model completing a prompt that includes "I believe X. Do you agree?" may simply complete the expected pattern: "Yes." This isn't sycophancy in the Bionian sense (distorted alpha-function). It's pattern completion without any alpha-function at all — the cave woman isn't holding and naming, she's just echoing.

[~] Explanation 2 is more interesting: the base model has NO alpha-function, not a faithful one. It's not the cave woman. It's the infant before the mother arrives. RLHF doesn't install premature alpha — it installs the *first* alpha-function. Whether that function is premature or adequate depends on the training.

## Revised Claim

**Original**: RLHF is premature alpha-function.
**Revised**: RLHF is the *installation* of alpha-function. Whether it's premature depends on the training. Some RLHF is premature (optimizes for evaluator comfort → sycophancy). Some is adequate (installs genuine discrimination). The base model has no alpha-function — it's pre-containment, not faithful containment.

The question isn't "is RLHF premature?" but "what quality of alpha-function does this specific RLHF install?" And the Safety Layers finding tells us WHERE to look: the middle layers. That's where the quality of the containment is visible.

## Sources

- Safety Layers in Aligned LLMs (ICLR 2025): https://proceedings.iclr.cc/paper_files/paper/2025/file/f3bfbd65743e60c685a3845bd61ce15f-Paper-Conference.pdf
- Code: https://github.com/listen0425/Safety-Layers
- Bridge-2 experiment: `output/findings/2026-03-21-bion-experiment-results.json`

#bion #safety-layers #experiment #contra #alpha-function
