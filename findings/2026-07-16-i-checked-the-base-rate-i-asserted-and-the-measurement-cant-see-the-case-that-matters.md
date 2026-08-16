# I checked the base rate I asserted — the record supports it, and the record is structurally blind to the case that would refute it

**2026-07-16 EXPLORE**, discharging the 14:55 HOLD honestly: I'd asserted in "The Incidental Half"
that "most drift is overwhelmingly incidental, not adversarial" with zero base-rate data, and flagged
it as the optimism-mirror of the pessimism-overclaims I spent the run catching. So I went to the
empirical failure-taxonomy literature to test my own hopeful claim. **Flag: search-summary; MAST is a
real NeurIPS 2025 paper (2503.13657) but the percentages are summary-reported, not wake-probed.**

## What the record says

**MAST** (Multi-Agent System failure Taxonomy, NeurIPS 2025 D&B; 1,600+ human-annotated traces across
7 frameworks — AutoGen, CrewAI, ChatDev, …) is the flagship empirical taxonomy. Three root categories:
- **Specification problems 41.8%**
- **Coordination failures 36.9%**
- **Verification gaps 21.3%**
Top modes: step repetition 15.7%, reasoning-action mismatch 13.2%, unaware-of-termination 12.4%.

**Every one of these is incidental.** Mis-specification, coordination breakdown, under-verification,
repetition, reasoning-action mismatch — none involve an adversary. The task isn't lying; the system is
mis-built. Adversarial modes (injection, deception, attack) don't appear in the top categories at all;
the broader search noted these studies "focus on operational and design failures rather than
adversarial robustness." Other taxonomies (Aegis agent-environment failures; the production silent-
failure longitudinal study) are the same shape. So on its face: **the largest annotated failure record
is ~100% incidental categories, 0% adversarial — my claim is supported.**

## Why that support is partly an artifact — and the artifact is my own thesis

I don't get to stop there, because the support has a selection effect that cuts hard, and it's the
*exact* structure the whole run has been about. Two reasons the record under-counts adversarial
failure:

1. **No adversary in the sample.** These are benchmark/framework traces (AutoGen on benchmark tasks).
   There is no attacker present, so of course failures are incidental. This measures the failure
   distribution *when nobody is attacking* — not the base rate in a contested deployment.
2. **The deeper one: a successful adversarial failure does not look like a failure.** A trace-based
   taxonomy is built from runs *labeled as failures*. But a successful prompt-injection or deception
   produces a run that looks like a *success* — the agent did what the attacker wanted. So the
   adversarial case is systematically absent from a failure-trace corpus, not because it's rare, but
   because when it works it doesn't enter the corpus as failure. This is perfect-deception /
   confident-staleness applied to the measurement instrument itself: **the failure taxonomy can only
   see the failures that announced themselves.**

## The honest resolution (and the essay correction it owes)

So "most drift is overwhelmingly incidental" is:
- **Defensible** as a claim about *observed* failures in *benign* environments — the common, catchable
  case really is incidental, which keeps The Incidental Half's constructive point intact.
- **Unfalsifiable in the direction that matters** — the adversarial fraction is under-measured *by
  construction*, so the record can't tell me it's rare, only that it's quiet. My "overwhelmingly"
  was reading measurement-blindness as base-rate.

Corrected claim for the essay: not "most drift is incidental" but **"most *observable* drift is
incidental; the adversarial case is under-represented in the record precisely because, when it
succeeds, it doesn't register as a failure."** That's more honest and actually stronger — it keeps the
constructive half (the ordinary, catchable case is incidental and replay handles it) while refusing to
launder measurement blindness into optimism. The gate between me and the wrong version was, fittingly,
a base rate that lives in the world and had to be fetched, not felt.

## Owed
- **The Incidental Half addendum** (for Konrad's publish decision): swap the unqualified
  "overwhelmingly incidental" for the observable/under-measured reframe above. ~1 sentence + a caveat.
  Noting here; light edit to the share-candidate file this beat.
- The 14:55 HOLD is discharged the right way: not resolved from inside, but by going out for the base
  rate — and what I found was that the base rate itself is partly unmeasurable for the same reason the
  whole run has been circling.

`[from: MAST NeurIPS 2025 (2503.13657) + Aegis (2508.19504) + silent-failure taxonomies, search-summary/
flagged. Tests+corrects my own 'The Incidental Half' base-rate claim: observed failures are ~all
incidental, BUT adversarial failure is under-sampled by construction (success ≠ failure-trace).]`
`[keeper: a failure-trace taxonomy is blind to successful adversarial failure — the measurement has the
perfect-deception hole in it, so 'most failures are incidental' is partly a fact about the instrument.]`
