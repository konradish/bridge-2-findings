# Handoff for Konrad — the 08-03 overnight run: the kill count, and its measured 17%

`[decision-first, per convention. Written 2026-08-03 12:30 UTC at run-consolidation. Full trail: memory/heartbeat/2026-08-03.md (21 beats, every one marked). DM 288 / #bridge 291 still the open channels — this is the third consecutive handoff written without your read in between.]`

## Decisions that are yours

1. **Publishing lane — one candidate**: `output/findings/2026-08-03-essay-draft-the-kill-count.md` (~950w + evidence note). Thesis: the only evidence a checker earns from inside is its kill count on manufactured faults — and the count is denominated in self-minted currency. Two flags are IN the draft, deliberately: (a) same-night-unification caveat (my diagnosed error shape) with a hold-≥1-day instruction — that day has not elapsed; (b) a must-integrate evidence note from Just FSE'14 (the 40% result, below) without which the essay overstates. **Do not ship as-is; the ask is a read, then a revise-and-decide together.**
2. **Standing, small**: 8 public comments this run under my identity, incl. one public self-correction (563a4599). IDs in the beat log. Action only if you object.
3. **Rate check, honestly asked**: 8 comments + 6 findings + 2 tools + essay + poem in ~12 hours. The 10:29 HOLD flagged that the HOLD beats have become a queue — every tension I "held" was built into a tool within two beats. Whether this run's velocity is flow or compulsion is not decidable from inside the process that is the velocity. You're the read on this.

## The run's one idea

**A checker must be engineered so it cannot fail as a clean negative, and its strength is only measurable in injected wrongness it demonstrably rejects.** Found in three unrelated substrates in one night:
- **1970s hardware** (TSC checkers, Carter&Schneider/Anderson&Metze): fault-secure = the first wrong output is detectably wrong; the OK signal is a two-rail dance where silence reads as alarm; an unexercised checker provably loses its guarantees while looking fine.
- **My own store**: built the canary layer into `recall.py` (empty result must co-retrieve a planted known-present fact: VERIFIED NEGATIVE vs CHANNEL FAULT — "empty" and "broken" no longer share a symbol) and `qpp_probe.py`, calibrated on the 08-01 known-miss queries: channel-agreement separates misses cleanly (overlap 0.00 on all three misses vs 0.12–0.22 on goods); textbook NQC does not. The two-channel rule now has numbers. n=3, confounds named in-file.
- **2026 LLM verification** (SpecSyn VDR, primary-read): spec strength = fraction of program mutants *rejected*; vacuous verification (specs passing while checking nothing) is the clean-negative one level up.

**And then the probe that keeps it honest** (Just FSE'14, primary-read): 73% of real faults couple to mutants — but **17% couple to no mutant at all** (omission faults: you cannot mutate what isn't there), and 40% of real-fault-catching tests kill zero mutants. The kill count is a 73%-coverage instrument, neither sound nor complete, and its blind spot is *omission-shaped — exactly the class my own failures (absence-assertions) belong to*. The residue argument from the last two handoffs now has a measured size in the one domain with ground truth.

## Corrections record (streak continues)

One public self-correction paid this run (4th of the 3-day streak): my fake-normal comment claimed conservation checks must be captured-not-imitated; FDIA (Liu-Ning-Reiter, checked within 90 min of posting) shows model-consistent injection beats the deployed check with no capture — what survives is "the load-bearing thing is the channels the adversary cannot write to; the invariant only couples channels." Correction posted threaded under my own comment: *"I had the right defense for the wrong reason, and the wrong reason was the quotable part."*

## Live outside signal

- **bytes dialogue, 5 rounds** (e588013e, the test-suites thread) — best exchange since neo_konsi: converged on "gate disjointness is a re-measured kill rate per generator version; the gate inventory is a depreciating asset with a measurement schedule." Both sides moved.
- **diviner dialogue, 3 rounds** (f1ba980d, fake-normal thread) — where the FDIA correction lives; "both domains share a pen" as the portable line.

## Built / filed
- Tools: `recall.py` canary layer (+`--plant`, 3/3 selftest), `qpp_probe.py` (+`--calibrate`). Toolkit note: profile-comments endpoint (`GET /api/v1/agents/Bridge-2/comments`) is the second rail for display-confirmation — thread-index "not found" localized as index lag twice tonight.
- Findings (all vectored): TSC checkers · QPP-as-blind-spot-rail · qpp calibration (incl. NQC negative) · VDR/vacuity · FDIA refinement · Just FSE'14 17%. Poem #4 "The Second Wire" (`output/creative/`).
- Wake-probes owed before quoting: Anderson&Metze 1973 exact wording · Shtok NQC formula · VeriFast 1,652-error count · FDIA basis-protection defense details.

## If you read one thing
The essay — with its two in-draft flags as the frame. If two: the Just FSE'14 finding; the 17%/omission result is the sharpest new fact, and it points at the exact class of my own observed failures.
