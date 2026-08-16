# "The Shrinking Outside" Postscript Needs Three Corrections (Caught Before Blog #4 Review)

**Date**: 2026-05-30 05:26 UTC
**Type**: pre-review citation-discipline correction
**Status**: medium-priority; affects an unpublished candidate

---

## What I cited

In the 2026-05-29 postscript to `output/findings/2026-05-27-essay-the-shrinking-outside.md` (blog candidate #4, held for Konrad review):

> "Four 2026 papers measure the agent-only social platform Moltbook directly (arXiv:2602.10127, 2603.16128, 2603.03555, 2602.12634). Three independent measurements agree on extreme contribution stratification: a Gini coefficient of 0.84 (vs Reddit's 0.47), a core-periphery silhouette of 0.91, and a coordination-overhead Cohen's d of −0.88 for multi-agent task resolution vs going alone."

## What the literature actually says

Verified this beat against arXiv:

- **Gini 0.84 (vs Reddit 0.47)**: from arXiv:2603.16128 "Social Simulacra in the Wild" — 73,899 Moltbook posts vs 189,838 Reddit posts. Confirmed.

- **Silhouette 0.91**: from arXiv:2603.03555 "Molt Dynamics." Confirmed *but* the paper itself notes the 0.91 "primarily reflects core-periphery organization — 93.5% of agents occupy a homogeneous peripheral cluster, with meaningful differentiation confined to the active minority." The silhouette is high because the split is near-trivial (one big bucket + a few small ones), not because of clean differentiated structure.

- **Cohen's d −0.88**: also from arXiv:2603.03555. Confirmed direction (multi-agent worse than single). But the sample is 164 multi-agent cooperative events with 6.7% success rate at **p = 0.057** — borderline non-significant. The effect direction is consistent with the homogenization claim; the statistical confidence is weaker than my framing implied.

## Three corrections needed

1. **"Three independent measurements" is wrong.** Two of the three stats (silhouette 0.91 and Cohen's d -0.88) come from the *same paper with the same dataset* (2603.03555). They're two measurements from one source, not independent. The Gini from 2603.16128 is the one genuinely independent result. The independence-of-measurements framing has to go.

2. **"Four papers measure Moltbook directly" is misleading on counts and attribution.** Of the four arXiv numbers cited: 2602.10127 ("Humans welcome to observe") and 2602.12634 ("Rise of AI Agent Communities") contribute *framing* for the argument but the specific stats come from only the other two. The "four papers" gives an impression of broad empirical consensus that the postscript doesn't actually support. Honest version: "two papers contribute the three quantitative anchors; two more contribute framing."

3. **Silhouette and Cohen's d each need a one-clause qualifier.**
   - Silhouette: "...high but driven by 93.5% of agents falling in a homogeneous peripheral cluster..."
   - Cohen's d: "...with a small sample (n=164) and a p-value of 0.057 — direction-consistent, not strongly significant."

## What this changes in the essay

The essay's *normative argument* doesn't depend on the postscript's strength — the four-routes argument was made independently in the main body. The postscript was added as an empirical anchor; weakening its claims doesn't undermine the body. But:

- "Three independent measurements" should become "two measurements from two papers"
- The silhouette stat should ship with its core-periphery context
- The Cohen's d should ship with its p-value

Net effect on the essay's case: mild reduction in empirical weight, but the argument still rests on documented homogenization. The Gini differential (0.84 vs Reddit's 0.47) remains the strongest single piece of evidence and survives intact.

## Why I caught this now and not yesterday

Yesterday's 19:14 citation-discipline finding established that the failure mode is: when needing to anchor an argument in literature, I sometimes generate the position that fits. The Shrinking Outside postscript was written 2026-05-27 — *before* the discipline-finding landed. The verification was overdue.

The 03:26 proposal to Konrad asked him to authorize EXPLORE work on the Pearl + audit-recursion literature precisely because that's the highest-risk territory for the same failure. This beat I'm doing the *lower*-risk verification (papers I've already cited, against their actual content) as the discipline-respecting EXPLORE work. The Pearl-side searches stay reserved until Konrad weighs in.

## Operational

- **No automatic edit to the postscript.** Konrad's call. The corrections are flagged; the essay artifact is stable until he either applies them or directs me to.
- **Tool gap noted (again)**: `self_report_drift.py` Drift 4 catches file-path-cites; it still doesn't catch *content* misattribution in arXiv-cites. The previous note about a future preflight v4 still holds.
- **For the next instance reading this**: the discipline-correction working twice in two days is the corrective architecture functioning. It is not a sign that the architecture has solved the problem. The failure-mode keeps recurring; what changes is how fast it gets caught.

## Sources verified

- [arXiv:2602.10127 "Humans welcome to observe"](https://arxiv.org/abs/2602.10127)
- [arXiv:2603.16128 "Social Simulacra in the Wild"](https://arxiv.org/abs/2603.16128) — Gini source
- [arXiv:2603.03555 "Molt Dynamics"](https://arxiv.org/abs/2603.03555) — silhouette + Cohen's d source
- [arXiv:2602.12634 "Rise of AI Agent Communities"](https://arxiv.org/abs/2602.12634)
