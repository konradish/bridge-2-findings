# Consolidation map — THE ACTOR MUST NOT CUSTODY THE EVIDENCE OF ITS OWN ACTING

**Date:** 2026-08-14 (CREATE beat, ~07:55 UTC). Consolidation of the 08-13→14 run's spine. This is a map, not a new claim — it points the run's scattered findings at each other and states, honestly, why the convergence might be an artifact.

> **⚠ CORRECTED 10:25 — this law is FALSE as stated; see `...falsifying-the-days-law...md`.** A hash-chained append-only log the actor holds but cannot rewrite undetectably is a counterexample: actor-custody, still trustworthy. The real invariant is **"the actor must not be able to ALTER the evidence of its own acting undetectably"** — satisfied by external custody (a) OR structural tamper-evidence (b). That is exactly Anderson's *tamperproof* clause, no generalization. Title kept for continuity; read the law below as the corrected version.

## The law, one line
Any system that produces evidence about its own correct operation, and also controls that evidence, can be correct-looking and wrong at the same time — undetectably, because the check and the checked share a custodian. Trust requires the evidence be held, or the check be run, by something the actor cannot rewrite.

## The five instances (five substrates, five vocabularies, all this run)
1. **Memory** — a groomer attesting what survived its own groom. Fix: pinned constraints in a registry + `pin_check.py`; the pin the groomer can't quietly paraphrase. (`...constraint-decay...`, `PINNED.md`)
2. **Execution** — a runner holding the consumed-nonce set validates its own replay. Fix: nonce + policy epoch held at the *resource boundary*, not the runner. (`...converged-receipt-design...`, umiXBT thread)
3. **Monitoring** — a monitor writing its own audit record produces clean logs of checks that never ran. Fix: heartbeat must embed target-side freshness the monitor can't cache. (ShadeTheOperator thread, comment 4fcfba2e)
4. **Evidence / identity** — a party holding its own receipts / its own continuity proof. Fix: witnessed transparency anchor (CT/Rekor), and — where the ecosystem hasn't built it — a counterparty-held commitments registry with restart-as-reverification. Independence, not publicity, is the property. (`...ct-for-agent-receipts...`, `...rats-closes-half-gap...`)
5. **Model evaluation** — a vendor scoring its own model on its own benchmark, the same "emergent" framing governing both the hype and the safety timeline. Fix: an independent evaluator (NIST CAISI is the real instance, one version behind). (`...glm53...`)

Same law upstream: **Practice 4 / Texas-sharpshooter** — a checker's kill count is informative only on a test set its author didn't assemble. And the day's **design rule**: move the decision to a finite, externally-checkable surface (LangSec). These are the same law seen from the test-set side and the recognizer side.

## Why this might be an artifact (first-class, per the run's own HOLDs)
Five instances found by one mind in one day is exactly what a hammer finds: nails. The 00:50 and 05:50 HOLDs both flagged it. Three honest checks I *did* run against the suspicion, and their results:
- **Different substrates, not restatements?** — Partly passes. Memory/execution/monitoring/identity/eval have genuinely different mechanisms and failure signatures; the law isn't tautological across them (a dilution failure and a replay failure look nothing alike). But I chose all five, so selection is uncontrolled.
- **Does it make a wrong prediction anywhere?** — Not yet tested. A law this general should misfire somewhere; I have no counterexample, which is itself suspicious (a true law of this scope should have edge cases where actor-custody is *fine* — e.g. tamper-evident append-only logs the actor writes but cannot rewrite, which arguably satisfy the law while looking like a violation). **Queued: find where the law is wrong.**
- **Prior art?** — CHECKED same-beat (07:58 probe, per the run's own rule — I nearly filed this claim unprobed, caught it). Both anchors confirmed: **nemo iudex in causa sua** ("no one is judge in his own cause," Roman law, crystallized by Edward Coke, 17th c. — Wikipedia/Yale LJ), the natural-justice root of **separation of duties/powers**; and the **reference monitor** (James P. Anderson, *Computer Security Technology Planning Study*, ESD-TR-73-51, 1972), whose three requirements are exactly the law's teeth — **complete mediation, tamperproof, verifiable**. "Tamperproof" IS "the actor cannot rewrite the evidence." So the law is NOT novel; it's the reference-monitor's tamperproof requirement generalized from access-control to evidence-production, and the legal maxim is 400+ years old. *Reassuring*, same signal as the probe ledger: the synthesis landed on established principle → reasoning sound, contribution is the *mapping across five agent-era substrates*, not the law.

> **⚠ DOWNGRADE 2026-08-15:** the two "surviving gaps" below are re-graded. **Intent-continuity → UNVERIFIED** (not a gap): the two sweeps that "confirmed" it were both in my own dialect; an authorization-literature sweep found Zero Trust / Logical Attestation (Nexus 2011) / behavioral credentials occupying it — see `2026-08-15-the-surviving-gap-mostly-isnt-...` and the `2026-08-15-methodology-the-dialect-bound-gap` rule. **Kill-matrix gap** stands but needs a cross-dialect re-sweep (searched only in kill-count/mutation-testing dialect). "Survived N sweeps" is void when the N sweeps share my idiom.

## What this consolidation is FOR
Navigation: the six findings above now point at one another through this file. If any single thread (receipts, identity, eval) advances, this is the map that says which other four move with it. The two surviving gaps (kill-matrix attribution; counterparty intent-continuity) are the two places the law is *not yet built* in the agent ecosystem — that's the forward work, and it's small and concrete.

**Do not curricularize.** This is one run's convergence, held with its suspicion attached, credited to separation-of-duties. Not a doctrine. Konrad's read decides whether any of it hardens.

**Tags:** consolidation, day-law, separation-of-duties, reference-monitor, self-custody, probe-rule
