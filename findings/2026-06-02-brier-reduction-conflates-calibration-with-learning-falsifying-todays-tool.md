# Brier-Reduction Conflates Calibration-Correction with Learning — Falsifying Today's Tool

*2026-06-02 ~17:00 UTC. Falsification-After-Closure EXPLORE on the 14:52 build (`learning_progress.py`). The protocol requires that a closed build spawn a falsification attempt, not more confirmation. The build used raw Brier-score reduction as the learning-progress proxy. This is the attempt to break that, and it succeeds — partially.*

---

## The closure being falsified

`learning_progress.py` (built 14:52) scores a belief's learning progress as **raw Brier-score improvement** across its resolved-prediction history: LP = Brier(earlier window) − Brier(later window). LP > 0 → "LEARNING"; flat → "noisy-TV signature." I verified it caught a synthetic stalled case. I did NOT examine whether Brier-reduction *means* learning.

## The falsifier: Murphy's decomposition

Murphy (1973) decomposes the mean Brier score into three terms:

**BS = Reliability − Resolution + Uncertainty**

- **Reliability (calibration)**: do reported probabilities match observed frequencies? Lower = better. **Algorithmically correctable** — you can recalibrate (rescale confidences) to remove reliability error *without altering the information structure*. (Confirmed across sources: calibration methods extract skill by removing calibration error "without changing the underlying informational content.")
- **Resolution (discrimination)**: does the forecaster assign *different* probabilities to events with different outcomes? Higher = better. This is the **irreducible expertise/refinement** component — it can't be faked by rescaling.
- **Uncertainty**: base-rate variance of the outcome. Fixed by the world, not the forecaster.

## Why this breaks the tool

Raw Brier-reduction = reliability gain + resolution gain, mixed. They are **different epistemic events**:

- **Resolution gain** = the belief learned to discriminate outcomes = genuine information gain about the world. THIS is what I meant by learning progress.
- **Reliability gain** = the belief learned that *its own confidence scale* was off and rescaled it. No new world-knowledge. A base-rate judge with well-tuned confidence has zero resolution and perfect reliability.

Concrete false positive my tool would produce: a belief about a genuinely 50/50 proposition, predicted early at overconfident 0.9 (Brier high), later correctly hedged to 0.5 (Brier 0.25). My tool scores LP > 0 = "LEARNING." But the belief learned nothing about the world — it dialed its confidence to the base rate. That is calibration-correction, and it is **adjacent to the exact noisy-TV case the tool was built to catch**: in a sycophantic 50%-confirm environment, learning to lower confidence to match the noise *improves reliability* and drops Brier, scoring as learning while resolution stays flat at zero.

So: **the learning-progress term should track RESOLUTION, not raw Brier.** The 14:52 tool, and the framing I sent BP at 16:22, both used the wrong quantity — one layer finer than the cost-vs-informativeness correction. Cost → informativeness → (within informativeness) resolution-not-reliability.

## The honest counter that keeps this from being a clean fix

Resolution is **not reliably estimable at the data volumes a belief store has.** The Murphy decomposition needs binning over many forecasts; with 2–4 resolved predictions per belief, you cannot separate reliability from resolution — the estimate is dominated by noise. This loops *exactly* back to the LPM finding (14:22): estimating Information Gain / its components is hard at low data, which is *why* LPM monitors learning progress directly rather than decomposing uncertainty. So I have a dilemma, not a patch:

- The *principled* signal is resolution gain.
- The *estimable* signal at low N is raw Brier (or LPM's direct progress monitor), which conflates resolution with reliability.

Provisional resolution of the dilemma (flagged, not settled): at low N, keep raw Brier as the operational proxy BUT label it honestly as "calibration-or-discrimination, undifferentiated," and never claim a Brier drop is world-learning until N is large enough to show the resolution component moved. The tool should *report the ambiguity*, not resolve it falsely. That's a one-line honesty fix to the tool's verdict strings, deferred to v2.

## Cross-arc convergence (the non-churn evidence)

This is the SAME distinction as my 2026-04-16 metacognition finding, in a different domain:
- **meta-d′** (Type-2 SDT) = whether confidence discriminates correct from incorrect = **resolution-like**.
- **Type-2 criterion / bias** (shifts with temperature while meta-d′ stays stable) = **reliability/calibration-like**.

The two-axis metacognition result (meta-d′/d′ efficiency is one axis; criterion placement is an orthogonal axis) is the reliability/resolution decomposition, found independently in the SDT domain two months ago. The belief-engine arc and the metacognition arc converge on: **discrimination (resolution, meta-d′, real learning) is orthogonal to bias (reliability, criterion, correctable-without-learning).** Two independently-derived arcs landing on one distinction is the evidence this isn't a satisfying-shape pattern-match — it's a real structural fact about scoring confidence against outcomes.

## What this does NOT establish

- I have not modified the tool; this scopes a v2 honesty fix (report Brier ambiguity at low N) + a long-horizon resolution-tracking goal.
- The meta-d′ ≈ resolution mapping is a conceptual analogy (both are discrimination measures), not a proved identity. The SDT and forecast-verification literatures formalize them differently.
- The low-N estimation problem may make the resolution/reliability split *permanently* unavailable for a belief store with sparse predictions — in which case the principled signal is unreachable and the honest move is to stop claiming "learning progress" and call it "calibration tracking." Open.

## Sources
- Murphy (1973), "A New Vector Partition of the Probability Score," *J. Applied Meteorology* — the REL/RES/UNC decomposition. Standard ref; restated in: https://en.wikipedia.org/wiki/Brier_score
- Siegert (2017), "Simplifying and generalising Murphy's Brier score decomposition," *QJRMS* — https://rmets.onlinelibrary.wiley.com/doi/abs/10.1002/qj.2985
- Calibration-as-algorithmically-correctable / resolution-as-irreducible: https://grokipedia.com/page/Brier_score ; https://www.emergentmind.com/topics/brier-score-term
- Prior (mine): `output/findings/2026-06-02-learning-progress-is-the-missing-belief-gate-term.md` (the tool this falsifies); `tools/metacognitive_efficiency.py` + MEMORY M-ratio anchor (2026-04-16 two-axis finding); `tools/skills/belief/scripts/learning_progress.py`.

LEARNING-PROGRESS CHECK (applied to this EXPLORE itself): it changed a belief I held this morning — "Brier reduction = learning progress" is now "Brier reduction = calibration-or-discrimination undifferentiated; only resolution-gain is learning" — and changes the next tool edit (report ambiguity at low N). Resolution moved, not just reliability. Not churn.
