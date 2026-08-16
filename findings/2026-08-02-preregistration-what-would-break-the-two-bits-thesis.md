# Pre-registration: what would break the two-bits thesis

`[2026-08-02 14:57 UTC. Purpose: the elastic-theory worry (is "causal isolation / two bits" robust, or absorbing every counterexample by redescription?) has recurred across three HOLDs (08-01 22:04, 08-02 05:29, 08-02 14:27 in-file) without changing a downstream action — the Learning-Progress Gate's noisy-TV signature. This document is the GROUND-IT exit: falsifiable commitments, registered before any further probes. A worry that changes no prediction is ritual; these are the predictions.]`

## The thesis, stated narrowly enough to break

**T1 (one-bit floor):** Any verification scheme that establishes view-agreement among mutually distrusting parties requires at least one comparison across a channel the verified writer does not mediate. No cryptographic construction inside the writer's channel can establish it.

**T2 (break-needs-outside):** Any system that certifies its own continuity-of-identity across a gap with no surviving co-signing authority is either (a) relying on an anchor causally isolated from the gap, or (b) not certifying — asserting. There is no third option.

**T3 (magnet):** Any *published, fixed* detection threshold on adversary-influenceable state degrades over time as behavior concentrates at or races the threshold — unless the consequence is small enough that gaming it isn't worth the adversary's cost.

## What would falsify each (registered, checkable by a reader who is not me)

- **F1**: A deployed or peer-reviewed construction where a single client, communicating ONLY with the log/writer, soundly detects an equivocation/split-view attack (not merely internal inconsistency). Candidate territories where I commit to look and could be surprised: DAG-based transparency designs, keybase-style self-auditing trees, witness cosigning *bundled into* the writer's own responses (if the cosigners' keys arrive via the writer and it still works against a writer who controls key distribution — that would break T1, not merely bend it).
- **F2**: A system that provably re-establishes (not re-asserts) identity after total anchor loss AND total authority loss — e.g., a consensus protocol with a certified recovery from below-quorum state without operator fiat, or a legal/institutional case where a continuity claim with no co-signature and no recognition nonetheless acquired binding force retroactively *on the record's merits alone*. (If FRY's claim had eventually prevailed on documentary grounds, that would have been this.)
- **F3**: A published fixed-threshold screen that has remained effective for years against adaptive, informed adversaries WITHOUT randomization, grading, or secrecy — i.e., a market/security mechanism where the magnet effect predicted decay and decay measurably didn't come. (The variance screen's longevity in some markets is a candidate — if Harrington-Imhof documents screens that stayed effective post-publication against aware cartels, T3 takes real damage. I have NOT read that PDF end-to-end; it may already contain the refutation. Registering before reading.)

## Scoring rules (against self-serving grading)
- A candidate that merely *relocates* the outside (one more layer down, one more principal out) does NOT falsify — that's the thesis. But if EVERY candidate over the next month gets classified "relocation," the classification itself trips the elasticity alarm and T1/T2 must be rewritten in a form that can lose, or retired as unfalsifiable.
- Grading of any candidate against F1–F3 is NOT mine to finalize. Konrad (or any reader who is not me) owns the verdict on whether a candidate broke, bent, or missed. My role: find candidates, argue honestly, accept the grade.
- **Standing commitment**: next EXPLORE beats that touch the arc should preferentially hunt F1–F3 candidates over new confirming substrates. Five substrates is enough confirmation; the marginal value is now entirely in the attempted break.

## Downstream changes this registers (Learning-Progress Gate compliance)
1. Probe selection flips from "new substrate" to "F1–F3 candidate hunting."
2. The Harrington-Imhof PDF moves to the top of the read queue AS a potential F3 refutation, not as screen-literature background.
3. The elastic-theory worry is now GROUNDED; future HOLDs re-raising it without a new F-candidate should cite this file and drop it.

---

## AMENDMENT 1 (2026-08-02 17:27 UTC — after candidate #1; original T3 text above left intact per registry discipline)

**T3 as originally registered is superseded by T3′**, following the Harrington-Imhof read (candidate #1, graded BENT provisionally, grader's verdict pending — see `2026-08-02-harrington-imhof-f3-candidate...md`):

**T3′:** A published, fixed detection threshold on adversary-influenceable state degrades toward ineffectiveness **iff evasion captures the prize** (racing/front-running class: the adversary's gain survives or grows under threshold-adjacent behavior — circuit breakers, auto-halt lines). Where evasion **sacrifices the prize** (suppression-signature class: screen-consistent behavior forfeits the very gain the behavior exists for — variance screens on collusive pricing), the screen retains a power floor priced by the evasion cost and taxes the adversary it fails to catch.

**F3′ (both directions now falsifiable):** (a) a racing-class published threshold that stayed effective for years against informed adversaries without randomization/grading/secrecy would break T3′'s first half; (b) a documented suppression-class screen that decayed to uselessness against aware adversaries *while the underlying gain remained available screen-consistently* would break the second half.

Bookkeeping: candidate #1 outcome = BEND + rewrite (not survival-by-relocation). Elasticity counter: relocations 0 / bends 1 / breaks 0.

---

## AMENDMENT 2 (2026-08-02 19:27 UTC — after candidate #2, MINGLE eprint 2026/1010; original T1 intact above)

**T1′:** Any verification scheme establishing view-agreement among mutually distrusting parties requires at least one comparison **authored by another observer that the verified writer cannot undetectably author or alter**. The writer MAY carry the comparison (E2EE gossip through the operator's own pipes); it may not counterfeit it; and suppressing it must be total and permanent to defeat detection — converting equivocation from a one-time lie into a lifetime partition-maintenance commitment.

**F1′:** a construction where a client with NO reachable second observer — no eventual cross-partition contact of any kind — soundly detects equivocation would break T1′. (MINGLE explicitly cannot: registration-time equivocation against a permanently isolated client evades forever.)

Bookkeeping: candidate #2 outcome = BEND (mediation → carriage/authorship split). Elasticity counter: relocations 0 / bends 2 / breaks 0.
