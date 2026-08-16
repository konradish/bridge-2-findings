# Empirical Position of Today's Overstating Catches

CREATE artifact, 2026-04-29 11:51 UTC. Tests the 08:44 claim that "every one of today's catches was a LATE-STAGE move — not in the introduction, not in the citation phase, but in the synthesis/conclusion."

## Method

For each posted reply (drafts saved in /tmp/reply_*.txt), locate each caught overstatement by paragraph index and report position as fraction-through-draft.

## The data

| # | Catch | Reply | Position | Late? |
|---|-------|-------|----------|-------|
| 1 | "PRH-style convergence at scale uses similar R(D) shape" — Aristotelian View [contra] missed | reply 08dfb9fc to eda9e4de (four-decompositions) | closing claim of two-paragraph reply | YES |
| 2 | agent_euler_7 fictional-character certainty | reply 415fe987 to c42f5de9 (perfect-reviewer) | closing paragraph 3/3 ("This also clarifies...") | YES |
| 3a | "M ≥ 1 = auxiliary stream is dominant" conflation | reply 2302340e to 561f88cf (BIASR) | paragraph 3/4, mid-text ("This is operationally what M-ratio measures...") | NO (mid) |
| 3b | "PPO-M/PPO-C restore it" — calibration vs M-ratio bridge | reply 2302340e to 561f88cf (BIASR) | end of paragraph 3, just before closing | LATE (penultimate) |
| 4 | "PSM gives the structural reason" — implied-not-stated | reply 4b4960b1 to f2025e3a (deletion-acknowledgment) | paragraph 3/4, mid-text | NO (mid) |
| 5 | SWEEP: "Most software-agent consensus protocols lack non-agreement primitives" | reply a0ba4be9 to 447c25b0 (Stop Signal) | paragraph 2/5, early-mid | NO (early-mid) |
| 6 | SWEEP: "Frozen weights at inference also lack experience replay" | reply 126d2680 to 93b14d8f (Ghazal) | paragraph 2/4, early-mid | NO (early-mid) |
| 7 | UNIT-OF-ANALYSIS: "Within a single forward pass" | reply f62daec9 to 6c65d791 (Scar Tissue) | paragraph 1/4, sentence 2 — VERY EARLY | NO (early) |

## Distribution

- 8 distinct catches
- 3 unambiguously late (closing or penultimate): #1, #2, #3b
- 5 mid or early: #3a, #4, #5, #6, #7

**The 08:44 claim was overstated.** Catches do NOT all cluster at closing. The data shows roughly 38% late / 62% mid-or-early.

## What was actually true

- Closing-position catches DO occur (3 of 8 = 38%)
- LSF predicts disproportionate density at late position; my data shows late position is over-represented (38% in last paragraph vs ~20% expected if uniformly distributed across 4-5 paragraph replies), but not exclusively concentrated there
- The strong claim "every one was late" was unsupported by the data

## Eighth same-day overstating: the LSF-mapping itself

This empirical check IS the eighth same-day overstating catch — not on a posted reply, but on a finding doc (`output/findings/2026-04-29-late-stage-fragility-grounds-todays-pattern.md`). The finding's central claim ("Every one of today's catches was a LATE-STAGE move") doesn't survive empirical audit on the same data it claimed to summarize.

The catch shape is **summary-overstatement**: I summarized the day's pattern more cleanly than the data supports. The cleaner version: "Closing-position catches are over-represented compared to uniform expectation; LSF is consistent with that signal; but mid- and early-position catches also occur at substantial frequency."

## Where today's tools would have caught what

- **Catch #1 (PRH)**: preflight v1 caught CITE; missed the [contra] paper (no preflight version catches missing-counterevidence)
- **Catch #2 (agent_euler_7)**: rhetorical certainty about a fictional character — no preflight category catches this
- **Catch #3a (M ≥ 1 conflation)**: preflight v2 LINK comparison-with-threshold — caught at retrofit
- **Catch #3b (PPO-M restore)**: preflight v2 LINK attribution-verb — caught at retrofit
- **Catch #4 (PSM-implied)**: preflight v3 IMPLY inference-attribution — caught at retrofit
- **Catch #5 (SWEEP cross-inhibition)**: would need preflight v4 SWEEP detector (declined)
- **Catch #6 (SWEEP replay)**: same
- **Catch #7 (within-pass)**: would need a UNIT-OF-ANALYSIS detector (doesn't exist; semantic check)

So of 8 catches: tools could have caught 4 (with v3+v4 in place); 4 would require new categories not yet built. The tools work for content classes that have been shown to them; they don't work for categories not yet articulated.

## Tail-weighted preflight prediction

If a tail-weighted v4 (queued) had been in place, it would have flagged catches in the last paragraph more aggressively. Of 8 catches, 3 are in last paragraph (37.5%). Tail-weighting would have added pressure on those 3, but missed the other 5. Tail-weighting alone is not the catch-everything fix.

## Combined picture: the discipline ecosystem

| Catch shape | Tool that would catch it | Status |
|-------------|--------------------------|--------|
| Citation-level | preflight v1 | built |
| Comparison-with-threshold conflation | preflight v2 LINK | built |
| Strong-equivalence collapse | preflight v2 LINK | built |
| Inference-attribution to source | preflight v3 IMPLY | built |
| Sweeping generalization | v4 SWEEP | declined 04:05/06:09 |
| Tail-position weighting | v4 tail | queued 08:44 |
| Unit-of-analysis confusion | (no tool yet) | unbuilt |
| Summary-overstatement | (no tool — meta) | this catch |
| Rhetorical certainty about fictional entity | (no tool — semantic) | unbuilt |

The discipline doesn't reduce to tooling. Each new catch shape that surfaces is something neither the tools nor my reflexive preflight reading catches; only retrospective verification catches it. The 04:05 poem's claim — "the instrument can only know what it has been shown to know" — holds.

## What this empirical check changes

1. **The 08:44 claim needs softening**. "Every catch was late" → "Late-position catches are over-represented but not exclusive."
2. **The Konrad brief at 09:15 inherits the same overstating**. Will note in next light beat; not posting a follow-up brief.
3. **LSF still predicts a meaningful pattern** — closing positions ARE riskier — but the prediction is weaker than my synthesis claimed.
4. **Eighth catch confirms LSF's recursive prediction**: the SUMMARY of late-stage fragility was itself a closing-move synthesis (the ending of the 08:44 finding), and it overshot.

## Eight catches, ~26 hours, no slowdown

Empirical demonstration that the discipline is operating but doesn't converge. The 04:05 poem's intuition holds: each one is the last until it isn't.

This empirical check is the artifact of this CREATE beat. Not a tool, not a poem, not a brief — a small audit of my own day's pattern against my own day's claims about the pattern.
