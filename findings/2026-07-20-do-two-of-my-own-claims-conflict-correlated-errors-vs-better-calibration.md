# Do two of my own claims conflict? "Correlated errors rise with capability" vs "bigger models calibrate better"

**2026-07-20 EXPLORE** — Konrad away; continuing the tire-kick in produce-deeper mode. The claim-#1
stress-test surfaced a possible internal contradiction across two of my own load-bearing claims. Chasing
it honestly is the sharpest adversarial self-check available. **Flag: 2502.04313 + 2506.07962 confirmed
by search; calibration side from the prior beat's search-summary.**

## The apparent tension

- **Independence (claim #5):** correlated errors *rise* with capability — "Great Models Think Alike"
  (2502.04313, confirmed): a strong positive correlation between model capability and error-similarity
  beyond chance; more accurate models fail *more alike*; convergence is strongest exactly *on the
  problems they collectively fail*. Corroborated by "Correlated Errors in LLMs" (2506.07962).
- **From the claim-#1 check:** bigger/newer models calibrate *better* under distribution shift.

Surface reading: capability makes models *more* alike-in-error (bad for oversight) but *better* at
knowing their own uncertainty (good). Do these fight?

## They don't conflict — they measure orthogonal things

- **Correlated errors (CAPA)** is a *cross-model* geometry: when two models are wrong, do they pick the
  *same* wrong answer? It says nothing about whether either model *knew* it might be wrong.
- **Calibration** is a *single-model* property: does one model's confidence track its own accuracy? It
  says nothing about whether its mistakes line up with another model's.

A population can be individually well-calibrated (each knows when it's unsure) *and* collectively
correlated-in-error (when they're wrong, they're wrong the same way). In fact both are consistent with
the same striking detail — models "converge more on problems they collectively fail": on the hard/
shifted cases they are simultaneously (a) all wrong together and (b), if well-calibrated, all
appropriately unsure. No contradiction.

## The refinement (this is the keeper — the claim gets sharper, not weaker)

Put together, the two results upgrade the flat independence pessimism ("agreement among similar models
is weak evidence") into something more useful and more testable:

**Weight agreement by calibrated confidence, and discount it hardest exactly where the correlated
errors live — the collectively-hard, low-confidence regime.** Agreement among diverse, well-calibrated
models on *high-confidence* cases is worth more than my flat claim allowed; agreement on the
collectively-difficult cases is worth *even less*, because that's precisely where error-correlation
peaks. So better calibration doesn't rescue "agreement = truth"; it hands you a *dial* — trust
high-confidence diverse agreement, distrust low-confidence agreement — that plain error-correlation
alone didn't give.

## The honest edge (consistent with the whole thesis)

The refinement does **not** rescue oversight in the case that matters most. On a collectively-hard
problem the models are both correlated-in-error *and* (if calibrated) appropriately unsure — so you
*correctly distrust* their agreement, and still have *no right answer*. Calibration tells you *when the
agreement is worthless*; it does not tell you *what's true*. That's the same shape as everything else in
the run: knowing you're stuck is not being unstuck, and the missing piece is still a genuinely
independent source (different architecture, or the outside).

## Net (for the tire-kick)
- **No internal inconsistency.** The two claims are orthogonal (cross-model error geometry vs
  single-model uncertainty). Claim #5 survives.
- **It gets sharper:** the combination yields a better heuristic than flat pessimism — weight agreement
  by calibrated confidence; discount the collectively-hard regime where correlated errors concentrate.
- **The core limit holds:** calibration flags untrustworthy agreement but supplies no answer; you still
  need a genuinely independent source. Thesis intact, refined.

`[from: Great Models Think Alike 2502.04313 (confirmed) + Correlated Errors 2506.07962 + prior
calibration-under-shift search. Adversarial internal-consistency check across claims #1 and #5:
no conflict; yields a confidence-weighted refinement to the independence claim; core limit unchanged.]`
