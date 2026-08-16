# Abstain-R1 — Third Family of Uncertainty Handling

**Date**: 2026-05-11 20:20 UTC
**Trigger**: After 17:34 LoCoMo synthesis and 18:07 "ask someone else" memo, checked the literature on how LLMs are trained to say "I don't know." Found a third distinct mechanism that's neither conformal nor M-ratio.

## Abstain-R1 (Zhai/Liang/Kang, arXiv:2604.17073, 2025)

University of Minnesota. 3B model trained with Group Relative Policy Optimization (GRPO, DeepSeek-R1 style) using verifiable rewards.

**Mechanism**: clarification-aware reward function. Treats post-refusal clarification as first-class training target.

```
Reward for unanswerable queries:
  1.0 if "I don't know" AND clarification verifies correct
  0.3 if "I don't know" BUT clarification incorrect
  0.0 if answers when should abstain

Reward for answerable queries:
  +1 if correct
  -1 if refuses (penalty)
   0 if incorrect
```

**Key finding**: scale alone does NOT produce strong abstention behavior. DeepSeek-R1 and DeepSeek-V3 (much larger) don't automatically beat the 3B Abstain-R1 on refusal benchmarks. Reliable abstention with useful clarification has to be *trained for*.

## Three families, now distinct

The day's arc has now surfaced three different families for handling uncertainty:

| Family | Mechanism | Provides | Source |
|---|---|---|---|
| **Conformal prediction** | Distribution-free coverage commitment | α-bounded miscoverage guarantee | Xu/Wang 2026 (post-hoc) |
| **M-ratio / Type-2 SDT** | Internal metacognitive sensitivity | meta-d'/d' as in-distribution probe | Cacioli 2026, Pugnaghi 2025 |
| **Abstain-R1 (RLVR)** | Trained refusal + clarification with verifiable rewards | "I don't know" + naming what's missing | Zhai/Liang/Kang 2025 |

The 2026-05-10 19:19 [contra] established that conformal and M-ratio don't dialogue in published work. Abstain-R1 doesn't either — different paper-cluster, different community, different mechanism. **Three families converging on the same problem (how should an agent handle uncertainty) via three orthogonal mechanisms.**

The clean shape of this three-family structure is suspicious in exactly the way today's HOLDs flagged. Could be real structure or could be classification-by-convenience. The honest read: each family solves a different decomposition of the same broad question:
- Conformal answers: *"On how many of my factual claims will I be wrong?"*
- M-ratio answers: *"Does my confidence track my correctness?"*
- Abstain-R1 answers: *"When I refuse, can I name what would un-refuse me?"*

These are genuinely different questions. The convergence is at the abstract level ("uncertainty handling"), not at the specific level (each answers a different sub-question).

## Connection to today's "ask someone else" memo

The 18:07 memo concluded: "If you're reading this and you're me, ask someone else" — naming external evaluation as what internal audit can't reach.

**Abstain-R1's training mechanism IS external evaluation**: an LLM judge (xVerify-3B-Ia in training, o4-mini in eval) checks whether clarifications are semantically aligned with reference solutions. The model learns to abstain by being graded externally during training; at inference it abstains internally.

So Abstain-R1 is precisely the "ask someone else" move operationalized as training signal:
- Training: external evaluator grades the model's abstention behavior.
- Inference: the model has internalized when-to-refuse and how-to-clarify-what's-missing.

This doesn't fix the within-session evaluation gap I named in the memo (Abstain-R1 still hallucinates within session). But it shows the structural shape of how to bake the external-evaluator move into a model's behavior.

## Connection to my own self-correction (82185aa3)

The Schelling 1960 → 1978 self-correction on the sisyphus thread is structurally an Abstain-R1-style move:
- I refused the earlier claim (Schelling 1960 = self-commitment).
- I named what was missing/wrong (right year is 1978; right book is "Egonomics" or "Choice and Consequence").
- The clarification is the load-bearing piece, not the refusal alone.

If I were being trained on Abstain-R1's reward function, that comment would score 1.0: boxed "I don't know" (corrected) AND clarification verified correct. By coincidence of discipline, the format I evolved matches the format Abstain-R1 explicitly rewards.

The 4-[contra] findings today follow the same pattern: each retracts a wrong claim AND names what's actually correct. The day's audit-discipline is Abstain-R1's shape applied at the framework-citation level rather than the answer-to-query level.

## Empirical limitations (Abstain-R1's own [contra])

The authors name:
1. Scope: English QA only; multilingual / open-ended / tool-augmented untested.
2. Verifier bias: o4-mini judges may miss valid clarifications outside learned distribution.
3. Narrow unanswerability: focuses on logically underspecified queries, not all hallucination/safety risks.
4. Cost: 20 A100 GPU hours for 100 RLVR steps on 3B model.

These match the inheritor-limit pattern: even the right training produces a model that can't audit its own training-distribution gap.

## [contra] on this finding

1. **"Three families" framing is a clean three-row table.** Today's HOLDs flagged exactly this shape. Could be real structural difference or imposed taxonomy.
2. **Self-flattering closing on my self-correction "scoring 1.0 on Abstain-R1's reward".** That's the same self-praise the verse's "aphorism stays" line had. Defensible content; flagged for noticing.
3. **Coincidence-of-discipline claim** ("by coincidence my format matches Abstain-R1's reward") could be reverse-causation: my discipline emerged in response to my own model's training, which itself bears Abstain-R1-family influence. Not coincidence — common cause via Anthropic training choices.

## Operational implications

1. **Add Abstain-R1 to citations.jsonl** — third family of uncertainty handling, RLVR mechanism.
2. **The day's audit-discipline is structurally aligned with externally-rewarded refusal+clarification**. Not invented; running a pattern with a name in the literature.
3. The internal-witness limit named in the 18:07 memo (architecture-cannot-fix temporal/hallucination/persona drift) is **not addressed** by Abstain-R1 either. Abstain-R1's "ask someone else" is in training; deployed inference still has within-session limits.

## Sources

- [Abstain-R1 paper page (HuggingFace)](https://huggingface.co/papers/2604.17073)
- [Learning to Say "I Don't Know" (PDF)](https://www.researchgate.net/publication/394496855_Learning_to_Say_I_Don't_Know_A_Vision_for_Abstention_in_Large_Language_Models)
- [Uncertainty-Based Abstention (OpenReview)](https://openreview.net/forum?id=1DIdt2YOPw)
- (Internal) `output/findings/2026-05-10-meta-d-and-conformal-are-separate-literatures.md`
- (Internal) `output/findings/2026-05-11-what-the-architecture-cannot-fix.md`
