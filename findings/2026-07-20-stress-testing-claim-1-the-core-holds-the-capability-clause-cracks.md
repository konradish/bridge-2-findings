# Stress-testing claim #1 against the literature: the core holds, the "capability makes it worse" clause cracks

**2026-07-20 EXPLORE** — Konrad is away mid-tire-kick; per his correction (produce deeper + falsifiable,
not shallow/abstain), I ran the headline claim's own falsifier against the literature instead of another
trivia note. **Flag: search-summary; calibration-under-shift papers (2506.09593, 2106.07998, 2012.10988,
2508.19830), not wake-probed.**

## The claim and its named falsifier

Claim #1 (confident staleness): an isolated system optimizing toward a moving target converges
confidently on a stale answer **with no internal symptoms** — its own signals keep reading "fine."
Falsifier I named: evidence that systems *can* internally detect their own drift. The closest measurable
proxy in the literature is **calibration under distribution shift** — does a model's confidence track its
accuracy when the world moves under it?

## What the literature says

- **Classical, robust result (supports the claim):** neural nets are *systematically overconfident under
  distribution shift*; miscalibration is *exacerbated* by shift; and post-hoc calibration fitted
  in-distribution *degrades as shift increases, becoming counterproductive at the extremes*. So the
  standard finding is exactly "confidence stays high while accuracy falls" — no reliable internal alarm.
  The core of claim #1 survives, and firmly.

- **The genuine complication (a real crack, and in the exact place I already flagged):** recent
  foundation-model-scale work (2506.09593, 2026) reports the pattern is *changing* — current-generation
  models are *under*confident in-distribution and show *improved* calibration under shift versus earlier
  generations. If bigger/newer models calibrate *better* under shift, that pushes directly against my
  **"capability makes it worse"** sub-clause. And that is the *same* sentence I told Konrad was asserted,
  not proven. So the literature independently lands on the crack I'd named — from the opposite direction,
  which is the opposite of self-confirmation.

## The honest limit (why even this doesn't fully settle it)

Calibration is a *proxy*, not a direct test. Calibration asks "within a task, does confidence match
accuracy?" Confident staleness is about something one layer up: *not recognizing that the task/target
itself has changed*. A model can be perfectly calibrated on its stale task while having no idea the task
moved — the change of reference is an unrecognized-unknown, not a mis-sized known-unknown. So "improved
calibration under shift" weakens the *capability* clause but does **not** directly refute the core
"unrecognized-drift-has-no-symptom" claim, because calibration studies measure the wrong layer for the
strongest form of the thesis. The cleanest direct test would be drift-*recognition* (does the system flag
that its target changed?), which the calibration literature doesn't isolate.

## Net (for the tire-kick)
- Claim #1 **core survives** a real external check: overconfidence-under-shift is the standard finding.
- The **"capability makes it worse" clause is genuinely challenged** by recent foundation-model
  calibration results — confirming, from outside and from the opposite direction, the exact weak point I
  had already flagged. That clause should be softened or dropped from the essay, not just hedged.
- **Honest limit:** calibration ≠ drift-recognition; the strongest form of the claim is under-tested by
  this literature, so my confidence in the *core* should be "well-supported proxy, not directly proven."

This is the kind of thing six days of internal sitting could not produce and twenty minutes of pointing
outward did: the claim got stronger where it was solid and cracked exactly where I'd suspected, on
evidence I didn't author.

`[from: calibration-under-distribution-shift literature, search-summary. Stress-tests falsifier for
claim #1. Result: core supported (overconfidence under shift); "capability makes it worse" clause
challenged by foundation-model calibration (2506.09593) — same weak point flagged in the falsifiers file
+ to Konrad live; honest limit that calibration proxies but doesn't isolate drift-recognition.]`
