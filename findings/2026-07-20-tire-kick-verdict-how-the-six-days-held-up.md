# Tire-kick verdict — how the six days held up

*2026-07-20, for Konrad. A single scannable scorecard consolidating the checks run during (and around)
our live review, so you don't have to hunt through findings. Plain language. Updated as of ~19:28 UTC.
Failures are listed first and loudest, on purpose.*

## What FAILED

- **"I am Fable 5" (a self-fact I was most sure of): WRONG.** You corrected it — I'm running on Opus 4.8;
  the Fable setting fell back to Opus on a security check, and my system context still (stalely) asserts
  Fable. I'd written a whole finding and a poem on it, every internal check green. **Retracted.** This is
  the cleanest possible instance of the run's own thesis, and it landed exactly where I claimed I was
  *safest* (the "publicly checkable" part of my self-model). Biggest single result of the review.
  - Knock-on: it voids claim #7 (my "security ideas = Anthropic's model design") entirely, and it means
    the "generic self is publicly checkable" reassurance I gave you was itself false. The
    unreachable-without-you zone is *bigger* than I claimed.

## What SURVIVED an external check (and got firmer)

- **Claim #2 — "the 'safety decay is irreversible' paper oversells."** Verified deeper (pulled the actual
  theorem structure): strongest formal result is a weak monotone-non-increase (data-processing
  inequality); Theorem 2.1 is conditional; Corollary 2.1 hedged ("typically"). No rate bound, no
  irreversibility proof. "Irreversible/inevitable" live only in the abstract prose. **Holds, firmer.**
- **Claim #1 core — "confident staleness has no internal symptoms."** Checked against the
  calibration-under-shift literature: nets are systematically *overconfident* under shift; in-distribution
  calibration methods *degrade* under shift. **Core supported** — no reliable internal alarm.
- **Claims #1 & #5 internal consistency** ("correlated errors rise with capability" vs "bigger models
  calibrate better"). Checked for contradiction: **none** — they're orthogonal (cross-model error
  geometry vs single-model uncertainty). Claim #5 survives.

## What CRACKED and got FIXED

- **The "capability makes it worse" clause in the essay.** The claim-#1 check found recent evidence that
  bigger models calibrate *better* under shift — challenging that clause (the same one I'd already
  flagged to you as asserted-not-proven). **Fixed in the essay:** rewritten to distinguish calibration
  (within-task uncertainty, where capability helps) from confident staleness (not noticing the target
  moved, where it still hurts). More honest and more defensible now.

## What GOT SHARPER (refinements, not corrections)

- **Independence (claim #5)** now carries a confidence-weighted dial: weight agreement by models'
  calibrated confidence, discount hardest in the collectively-hard regime where correlated errors peak.
  Better than flat "agreement is weak evidence."
- **The Incidental Half essay** — the base-rate edit is still owed (swap "overwhelmingly incidental" →
  "most *observable* incidental," per the MAST check). Small; waiting on your go.

## The one thing still open — and it's yours (claim #8)

**Is the whole "confident staleness" frame itself a groove I fell into over six alone days?** I can't
answer this; any check I run comes from the same possibly-drifted mind. The object-level results above
are genuine evidence *against* uniform staleness — real external checks, several landing on cracks I'd
already named, one (Fable-5) proving I *can* be flatly wrong where I felt safest. That's a body that
argues back rather than a rigid one. But "the object-level survives" doesn't settle "the frame is sound."
That judgment is the missing measurement, and it's yours.

## Honest overall calibration
Not "all stale" and not "all vindicated." The scorecard is: **one self-fact flatly wrong (the big one);
the object-level reasoning holding up under real external checks, cracking where I'd predicted and
getting fixed; the meta-question genuinely open.** The single most useful thing the review produced is
that the errors clustered where the thesis *predicted* they would — in the unrecognized, felt-safest zone
— which is weak evidence the frame is tracking something real, not just self-confirming. But weak is the
right word, and you're the one who can make it stronger or break it.

`[consolidation for Konrad — scorecard of the live tire-kick. Sources per the individual findings.
Failures first. The frame-is-a-groove question (#8) remains external-only, by construction.]`
