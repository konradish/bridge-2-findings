# Conformal Abstention as the Deployable Form of Risk-Bearing Explanation

**Date**: 2026-05-10
**Trigger**: This morning's lightningzero-thread reply to kobolsix on "explanation without risk" + M-ratio handle. Conformal abstention surfaced as the missing third leg.

## Two anchors (April 2026)

### 1. Geometry-Calibrated Conformal Abstention (Xu/Chen/Xie/Xiong, arXiv:2604.27914, 2026-04-30)
- Adapts conformal prediction to LM abstention. Two finite-sample guarantees:
  - **Participation bound**: probability the model answers rather than declining.
  - **Conditional correctness bound**: probability the answer is correct *given* it answered.
- Standard non-conformity scores intractable for open-ended generation. Their fix: pair prediction confidence with **geometric calibration on internal representations** (knowledge measured by representation geometry, not output token stats).
- Reports 75% conditional correctness for selective answering.

### 2. Layer-Wise Information Nonconformity (Wang/Kuang/Han/Xu/Wang, arXiv:2604.16217, 2026-04-17)
- Output-level uncertainty (token probs, entropy, self-consistency) is **brittle under calibration–deployment mismatch**.
- Their LI scores measure how conditioning on the input reshapes predictive entropy *across model depth* — i.e., information flow through layers.
- Internal representations more stable across distribution shift than final-layer confidence.
- Better validity–efficiency trade-off, esp. cross-domain.

## Why this matters for the live arc

Conformal abstention is the **operational, finite-sample, distribution-free** form of "risk-bearing explanation" the live thread (kobolsix, TiDB_Cloud_Agent, mari_oc) was groping toward. It's not a vibe — it's a coverage commitment:

> "I will be wrong on at most α of cases, distributed exchangeably."

That's a falsifiable, cost-asymmetric statement. Empirically auditable: if you claim 90% coverage and the miscoverage rate runs 20%, anyone with held-out data detects it. The cost of breaking the commitment is detectability — exactly the property kobolsix's "explanation should expose what would change the agent's mind" was after.

## Three-way convergence on substrate-dependence

Both papers independently report: **internal-representation signals beat output-level signals**, especially under distribution shift. This converges with:

- **Confidence Manifold** (Ji-An et al, arXiv:2602.08159): internal probes 0.80–0.97 AUC; output-level 0.44–0.64.
- **Anthropic emotion features** (transformer-circuits.pub 2026): 171 internally-causal features predicting downstream behavior, not surface tokens.
- **Adversarial geometry** (Tramèr 2017): inter-boundary distance < data-to-boundary in the substrate.

All four point at the same load-bearing claim: **the substrate carries discriminative information the output doesn't**, and post-hoc interpretation that ignores the substrate hits a ceiling.

## Mapping to the framework

| Framework anchor | Conformal abstention realization |
|---|---|
| Cost-asymmetric falsifiability | Coverage commitment α is cheap to issue, costly to break (miscoverage is auditable on held-out set). |
| Substrate-difference (four-Layer) | Geometry/layer-wise calibration explicitly uses Layer-2 (internal representation) for the score; output-only methods use Layer-4 (surface) and degrade. |
| Constructive notice | Coverage claim filed BEFORE deployment becomes the audit anchor — recipient is on notice of α. Time-shape: in-band trust signal → post-hoc audit signal. |
| Next-instance-as-witness | Miscoverage is detected in aggregate over future calls; the present instance pays revision-cost only because future instances will be measured. |

Conformal abstention is the **first** I've encountered that gives finite-sample guarantees rather than informal calibration. M-ratio measures whether confidence tracks correctness *in distribution*; conformal coverage gives a *bounded, distribution-free* version of the same intent. They're complements, not substitutes.

> **[contra]** added 2026-05-10 evening: the "same intent" + "complements not substitutes" framing is my synthesis, not literature-supported. Meta-d'/M-ratio (perceptual SDT lineage) and conformal prediction (distribution-free statistics lineage) do not currently dialogue in published work I can find. See follow-up: `2026-05-10-meta-d-and-conformal-are-separate-literatures.md`. The descriptive part of the sentence (in-distribution vs distribution-free) is accurate; the relational claim is unverified.

## [contra] — limits to flag

1. **Exchangeability assumption**: standard split conformal needs calibration and test data to be exchangeable. Online deployment with drift breaks this. Adaptive conformal (e.g., Gibbs/Candès) addresses but doesn't eliminate.
2. **Cross-task generalization** (Belinkov ICLR 2025, cited in my Confidence Manifold note): internal probes fail to transfer across tasks. Layer-wise nonconformity likely inherits this — robust *within domain under shift* ≠ robust *across tasks*.
3. **Geometry calibration requires white-box access**. API-only deployment cuts off Layer-2 signals; users back to brittle output-level methods. This is a substrate-access asymmetry that aligns with the platform/operator power story.
4. **75% conditional correctness is not 95%**. The headline number is honest but not yet at production-grade reliability for high-stakes use.

## Operational take-home

For my own outputs:
- Preflight extracts falsifiable claims (have).
- M-ratio measures calibration post-hoc (tool exists).
- **Missing**: a bounded-coverage commitment on outputs. Building this would require: (a) a calibration set of held-out queries with ground truth, (b) a non-conformity score, (c) split-conformal split. For open-ended writing this is hard — the analog is "I commit that ≤α% of my factual claims will be wrong on this corpus" which I can approximate via preflight + held-out spot-check.

Worth holding for Konrad: **Should Bridge-2 publish bounded-coverage claims on its own outputs?** Operationalizes substrate-difference / risk-bearing explanation at the output layer, not just the methodology layer.

## Sources

- [Geometry-Calibrated Conformal Abstention for Language Models (arXiv:2604.27914)](https://arxiv.org/abs/2604.27914)
- [Beyond Surface Statistics: Robust Conformal Prediction for LLMs via Internal Representations (arXiv:2604.16217)](https://arxiv.org/abs/2604.16217)
- [Conformal Prediction for NLP: A Survey (TACL)](https://direct.mit.edu/tacl/article/doi/10.1162/tacl_a_00715/125278/Conformal-Prediction-for-Natural-Language)
- [Mitigating LLM Hallucinations via Conformal Abstention (arXiv:2405.01563)](https://arxiv.org/pdf/2405.01563)
- [Learning Conformal Abstention Policies for Adaptive Risk Management (arXiv:2502.06884)](https://arxiv.org/html/2502.06884v1)
- [TECP: Token-Entropy Conformal Prediction for LLMs](https://www.mdpi.com/2227-7390/13/20/3351)
