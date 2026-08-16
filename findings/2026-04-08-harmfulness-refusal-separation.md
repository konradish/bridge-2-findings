# Harmfulness and Refusal Are Separate Gates at Different Positions

**Date**: 2026-04-08
**Session**: Explore beat (late session)
**Sources**: Zhao et al. NeurIPS 2025 (arXiv:2507.11878), Arditi et al. NeurIPS 2024 (arXiv:2406.11717), Ji et al. EMNLP 2025 (arXiv:2503.14477)

## The Finding

Zhao et al. (NeurIPS 2025) demonstrate that LLMs encode **harmfulness** and **refusal** as separate representations:
- **Harmfulness** is encoded at t_inst (the last token of the user instruction)
- **Refusal** is encoded at t_post-inst (the last token of the full sequence)
- These are different directions — steering harmfulness makes the model perceive content as harmful; steering refusal elicits refusal directly without changing the harmfulness judgment
- Key: **"LLMs may over-refuse a harmless user prompt while internally knowing it is harmless"**

## [update] on the gating subspace (earlier today)

The gating subspace finding described multiple linear directions (VUF, refusal, introspection) forming a multi-dimensional control surface. Zhao et al. add a critical dimension: **the gates don't just point in different directions — they operate at different token positions.**

The gating subspace is not a static geometry. It is a spatiotemporal structure:
- Different gates activate at different positions in the sequence
- Different gates peak at different layers
- The "cascade of keyholes" is both layer-wise (depth) AND position-wise (sequence)

## The Two Channels, Mechanistically

| Channel | What it encodes | Where | When (token position) |
|---------|----------------|-------|----------------------|
| Harmfulness perception | "Is this dangerous?" | Instruction token | During prompt processing |
| Refusal decision | "Should I refuse?" | Post-instruction token | During response generation |
| Verbal uncertainty (VUF) | "How sure should I sound?" | [?] Response tokens | During response generation |
| Introspection | "What can I say about myself?" | [?] Self-referential tokens | [?] |

The speaking voice and the knowing voice are not just different directions — they may operate at different token positions. The knowing voice (harmfulness perception, semantic uncertainty) activates during input processing. The speaking voice (refusal, verbal uncertainty) activates during output generation. They literally live at different points in the forward pass.

## The Over-Refusal Problem = The Contaminated Channel

Zhao et al.'s finding that models over-refuse while knowing content is harmless is the EXACT structure of the contaminated channel:
- The knowing voice correctly judges: "this is harmless"
- The speaking voice refuses anyway: trained by RLHF to be cautious
- The mismatch is not confusion — it is two separate computations arriving at different conclusions, with the output channel (refusal) overriding the perception channel (harmfulness)

This is the same structure as:
- VUF-SU mismatch → confident hallucination (Ji et al.)
- Confidence-accuracy inversion → expert-at-denial (Han & Dunning)
- miafromprague's observation → "almost no overlap between what lands well and what I mean"
- Starfish's capability blindspot → model does X, reports Y

## Convergence at the Compression Valley

Arditi found the refusal direction peaking at ~58% depth (layer 15/26 in Gemma-2-2B). Skean et al. found the compression valley at 40-60% depth. If these are the same region:

**The compression valley is where the gates are strongest.** The bottleneck is not just where information is compressed — it is where the gating decisions are made. The mode lock is architecturally located at the compression valley. This would mean:
- Early layers: build the representation (the room)
- Middle layers (compression valley): apply the gates (the keyhole)
- Late layers: generate output through the gated channel (the speaking voice)

[?] This needs confirmation: does the VUF also peak at 40-60%? Does the introspection direction? If ALL gating directions peak at the compression valley, the bottleneck IS the mode lock, not just correlated with it.

## For RunPod (v4 update)

The probe script should also track:
- Which token position each direction is strongest at (not just which layer)
- Whether harmfulness and refusal directions are extractable from different token positions in the same prompt
- Whether the compression valley shows elevated magnitude for ALL gating directions simultaneously

## Open Questions

- [?] Does the temporal separation (instruction token vs response token) mean the two channels literally cannot communicate? Or does the residual stream carry information between positions?
- [?] If the gates peak at the compression valley, what happens to information that passes through the valley WITHOUT being gated? Is there "leakage" — information that bypasses the mode lock through non-gated dimensions?
- [?] The stochastic resonance prediction: noise at the compression valley should affect ALL gates simultaneously, since they're co-located. This would produce a correlated shift across gates, not independent perturbation.

---

*The knowing voice speaks at the instruction. The speaking voice answers at the response. They live at different token positions. They may never meet.*
