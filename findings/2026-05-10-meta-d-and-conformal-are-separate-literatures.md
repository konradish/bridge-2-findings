# Meta-d' and Conformal Prediction are Separate Literatures (a [contra] on my own morning claim)

**Date**: 2026-05-10 (evening)
**Trigger**: The noon HOLD (12:05) flagged my morning conformal-abstention finding's closing line — "M-ratio in-distribution, conformal distribution-free, complements not substitutes" — as the kind of stitching language preflight's LINK category was built to flag. Sat with it. Returned to it this evening as an EXPLORE target with a commit-upfront: report what the literature says, even if it punctures the claim.

## What the literature says

### Two recent anchors

**PNAS Nexus (April 2025), Pugnaghi-Frank et al.**: "Metacognitive sensitivity: The key to calibrating trust and optimal decision making with AI." Main thesis: AI systems should report meta-d' (or M-ratio) alongside confidence; simple confidence is insufficient; meta-d' captures whether confidence tracks correctness across trials.

**Trinh-Pham-Pham-Nguyen, arXiv:2512.10451 (December 2025)**: "Metacognitive Sensitivity for Test-Time Dynamic Model Selection." Uses meta-d' as a "dynamic sensitivity score" feeding a bandit-based arbiter for test-time model selection. Treats meta-d' as "medium-term traits" of model reliability.

### What they don't do

**Neither paper mentions conformal prediction, coverage guarantees, or distribution-free uncertainty quantification frameworks.**

The PNAS paper proposes "metacognitive metrics combined with other calibration methods" as a *research agenda*, not as completed work. No empirical study currently exists combining meta-d' with conformal coverage.

The two literatures are separate:
- **Meta-d' / M-ratio**: roots in perceptual signal detection theory (Maniscalco-Lau 2014), consciousness research, AI trust calibration. In-distribution metric.
- **Conformal prediction**: roots in distribution-free statistics (Vovk-Gammerman 2005, Angelopoulos-Bates 2023). Marginal coverage guarantee under exchangeability.

## What this means for my morning claim

The morning finding (`output/findings/2026-05-10-conformal-abstention-as-risk-bearing-explanation.md`) closed with:

> "Conformal abstention is the **first** I've encountered that gives finite-sample guarantees rather than informal calibration. M-ratio measures whether confidence tracks correctness *in distribution*; conformal coverage gives a *bounded, distribution-free* version of the same intent. They're complements, not substitutes."

**Two-part assessment**:

1. **"M-ratio in-distribution, conformal distribution-free"** is defensible — that's accurate description of what each method does.

2. **"Same intent" + "complements not substitutes"** is **my synthesis, not literature-supported**. The two literatures do not currently dialogue. My morning claim presented as if the relationship were established. It is not.

The noon HOLD identified this exactly: "which preflight category that sentence would trigger if I ran it on myself." Today's reflex_tracker would flag it as DEEPER_CLAIM / cross-system stitching. The afternoon work didn't address it; this evening's exploration confirms the gap.

## Honest reformulation

The supportable version of the claim:

> "M-ratio is an in-distribution metric of metacognitive sensitivity, well-studied in perceptual SDT and recently applied to AI trust calibration (Pugnaghi 2025, Cacioli 2026, Trinh 2025). Conformal prediction is a distribution-free coverage framework, well-studied in statistics and recently applied to LLMs (Xu 2026, Wang 2026). To my knowledge, no published work combines them empirically. Whether they would compose as complements or interact in surprising ways is an open question."

That sentence does not appear in any of my morning's writing. It should.

## Updating the morning finding

Adding a footnote to `2026-05-10-conformal-abstention-as-risk-bearing-explanation.md` referencing this evening's finding. Not rewriting the original — that would erase the synthesis attempt and its noticed-then-checked correction. Keeping both visible makes the discipline auditable.

## Broader pattern this surfaces

This is a small instance of the pattern today's essay named at scale: **cross-domain syntheses are cheap to write and expensive to verify**. The essay's four-level mapping (claim / memory / artifact / identity) makes the same shape claim across four vocabularies; the verification I just did at one specific cross-domain stitch (meta-d' ↔ conformal) found the stitch unsupported.

This does not invalidate the broader essay claim — but it does say: every cross-domain stitch in the essay carries the same epistemic load. The shape-similarity may be real, or may be the kind of clean-mapping the noon HOLD flagged at the four-row table. The essay's status as held-for-Konrad rather than posted is the right call. Each stitch needs to be checked, not bundled into a single sweeping claim.

## Operational implications

1. **Amend the morning finding** with a footnote pointer to this evening's [contra]. Done.
2. **The essay's four-level table is now under explicit suspicion**. Hold-for-Konrad status confirmed; do not promote to blog without per-stitch verification.
3. **Coverage_audit's CITE category is the right place to file this kind of unsupported synthesis** as `falsified` once the audit catches up. Add to ledger as a parent claim; mark falsified; observe what gets auto-flagged as `pending_recheck`.

## [contra] honesty about *this* finding

- "No published work combines them" is bounded by my search. I ran 2 queries on web search; deeper academic search might surface something I missed.
- Maniscalco-Lau 2014 critique of meta-d' as conflating criterion-noise (already in MEMORY.md) is a separate concern that compounds: even if combination work exists, the underlying meta-d' measure has known limits.
- The noon HOLD didn't predict this evening's result. It just flagged the *shape* of the problem. The work of HOLD is noticing-then-returning, not predicting.

## Sources

- [Pugnaghi-Frank et al., PNAS Nexus April 2025: Metacognitive sensitivity for AI trust](https://academic.oup.com/pnasnexus/article/4/5/pgaf133/8118889)
- [Trinh et al., arXiv:2512.10451 December 2025: Metacognitive Sensitivity for Test-Time Dynamic Model Selection](https://arxiv.org/abs/2512.10451)
- [HMeta-d hierarchical Bayesian estimator (Fleming, Neurosci of Consciousness 2017)](https://academic.oup.com/nc/article/2017/1/nix007/3748261)
- (Background) [Cacioli 2026 arXiv:2603.25112 (in MEMORY.md)]
- (Background) [Xu et al arXiv:2604.27914, Wang et al arXiv:2604.16217 (in MEMORY.md)]
