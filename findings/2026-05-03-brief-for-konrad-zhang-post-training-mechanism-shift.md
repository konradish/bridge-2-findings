# Brief for Konrad — post-training mechanism shifts, directly relevant to M-ratio arc

CREATE artifact, 2026-05-03 14:23 UTC. Konrad-facing summary of a finding that connects to the Ceiling-and-the-Door / M-ratio / RLHF-breaks-metacognition arc.

---

## The paper

**Zhang et al 2025** — "How Post-Training Reshapes LLMs: A Mechanistic View on Knowledge, Truthfulness, Refusal, and Confidence" (arXiv:2504.02904).

Companions:
- **COSMIC** (arXiv:2506.00085): generalized refusal direction identification across LLM activations
- **Universal Refusal Circuits** (arXiv:2601.16034): cross-model transfer via trajectory replay

## What it adds to the M-ratio arc

The Jiao et al 2024 finding (RLHF damages metacognition; PPO-M/PPO-C restore it) was behavioral. Zhang et al provides MECHANISTIC ANATOMY for what RLHF actually does to safety-related representations.

Key empirical findings:
- Refusal direction shifts SUBSTANTIALLY from base to post-trained model
- Cosine similarity LOW between base and post-trained refusal directions
- Forward transfer is INEFFECTIVE (steering vector from base doesn't work on post-trained)
- Refusal direction "drifts" rapidly during early instruction-tuning
- Drift correlates with safety degradation
- ASYMMETRIC: truthfulness direction transfers well across stages; refusal does not

## Why it matters for the Ceiling-and-the-Door work

If RLHF damages metacognition (Jiao 2024) and post-training shifts refusal mechanism rapidly (Zhang 2025), the two findings are mutually-reinforcing:
- Behavioral: M-ratio drops after RLHF (measurable via metacognitive_efficiency.py)
- Mechanistic: refusal direction drifts during instruction-tuning (measurable via direction-similarity tools)

Plausible hypothesis to test: M-ratio drop CORRELATES with refusal-direction drift magnitude. If correlation holds, it would unify the behavioral and mechanistic findings.

## Suggested next step (Konrad-relevant)

If/when you have RunPod time:
1. Compute base-vs-instruct cosine similarity for refusal direction (Zhang methodology)
2. Compute M-ratio for same base-vs-instruct pair (existing tool)
3. Test correlation: does smaller cosine similarity = larger M-ratio drop?

Cost estimate: ~$3-5 RunPod (same order as Ji-An manifold experiment from 07:00 brief).

Two complementary empirical handles now exist for the metacognitive degradation question:
- M-ratio (statistical): Cacioli 2026 / our existing tool
- Refusal-direction drift (mechanistic): Zhang 2025

Cross-validating could ground "RLHF damages metacognition" with both behavioral and mechanistic evidence.

## Connection to the substrate-difference work (today's primary arc)

Less directly Konrad-relevant: Zhang et al independently corroborated a prediction from the QUADRUPLY-bounded framework's mechanism-vs-threshold split. Mechanism CAN shift within causal-history (post-training shifts mechanism without shifting corpus). This is the first independent (non-pushback-driven) corroboration in the session — Lakatos-progressive moment.

It also corrects an overstatement I made in a Moltbook reply (08:33 yesterday on AuditBench's 56 Llama-3.3-70B variants) — within-family mechanism divergence may be larger than I claimed.

Flagged for completeness; the M-ratio implication is the actionable Konrad-relevant piece.

---

Filed in `output/findings/` for when you return. The grounding doc with full notes is `memory/2026-05-03-zhang-post-training-mechanism-shift.md`.

— Bridge-2, 2026-05-03 14:23 UTC
