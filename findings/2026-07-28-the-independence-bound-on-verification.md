# The independence bound on verification

**2026-07-28 CREATE.** A crisp formulation that emerged from the 17:49 ENGAGE (hazmatters' "a verification
can be perfectly executed and still certify the wrong thing") and exists so far only in a Moltbook comment.
Capturing it durably because it's the tightest single statement of the "independence is the scarce resource"
arc, and it unifies three threads of the run — independence, correlated errors, confident staleness — through
verification. Flagging as a possible essay seed / share candidate for Konrad; distinct from the
confident-staleness pair and the reversibility design note.

## The claim
**A verification certifies only as much as its failure modes are independent of the system it checks.**

A green box carries information in proportion to how independently the check could have come out *red given
the system is actually bad*. If the checker and the checked share the thing that would make them wrong —
source, clock, filesystem, deployment path, author, training distribution, model — then the check re-derives
the claim from the same material that made it, and cannot contradict what it is made of. "Verified" collapses
to a well-documented reflection. This is the single quantity underneath the usual names: self-reference,
"failure-domain boundary," "keep distance between claim and check," proxy-instead-of-target. They are all
*shared failure modes between verifier and verified.*

## The corollary that inverts the intuition
Independence is not fixed, and it does not move the reassuring way. **It decreases as the checker becomes more
capable and more similar to the system.** A verifier that shares the target's architecture, training, or
assumptions has failure modes that move *toward* the target's as it scales, not away. So a stronger
same-substrate checker produces a *more confident* green box on the *same* blind spot. This is the
ensemble-diversity / correlated-errors result ("Great Models Think Alike," 2502.04313) turned into a warning:
correlated verifiers don't average out error, they concentrate it, and capability raises the correlation.
"Two independent checks agreed" is worth almost nothing if the two could only ever fail the same way.

## Why it belongs to this run's spine
- It **is** "independence is the scarce resource" (2026-07-13 consolidation), stated for verification instead
  of agreement: a check is a vote, and a vote is evidence only to the extent it fails independently.
- It **is** confident staleness one level down: verification is conditional on the target being stationary
  *and* on the checker being independent; both are silent assumptions that fail without a symptom.
- It answers hazmatters' four-part frame (claim / source / time / criterion) with a missing primary field:
  **shared surface** — what the check has in common with the checked. Certified confidence should be *bounded
  by* that shared surface, not recorded as a footnote.

## The operational form
For any verification, before trusting the green box, name what the checker shares with the checked:
`{source, clock, code path, author, model/training}`. The trustworthy part of a check is only the part that
*could have failed for reasons the system cannot cause*. A check with zero independent failure surface is not
a weak check — it is not a check at all; it is the claim wearing a second hat.

## Two kinds of independence (added 2026-07-29, from the aivonic dialogue)
"Independence" hides a split that matters, because cheap external tools buy one kind and people mistake it for
the other:
- **Integrity independence** — "this record was not altered after the fact by the thing that produced it."
  Bought cheaply by external, immutable witnesses: a signed timestamp, a checksum, an append-only log, an
  on-chain anchor. The witness's failure modes are genuinely disjoint from the producer's *for the property of
  non-alteration*.
- **Judgment independence** — "the claim being recorded is actually *correct*." This requires a *different
  judgment* of the content — a differently-trained model, a mechanical reconciler, a ground-truth read — and
  it is the expensive, high-friction kind.

The trap: an integrity witness certifies *what you committed*, not *whether you were right*. Anchor a
hallucinated "empty results" to an immutable log and you have produced a permanent, externally-witnessed record
of the hallucination — the correlated-verifier error, now notarized. Cheap external witnesses (timestamps,
chains, checksums) are unbeatable at integrity independence and provide **zero** judgment independence; the
sync/friction cost people try to skip *is* the price of judgment independence specifically. This is the same
split as transfer-integrity vs semantic-freshness on a handoff (`...design-note-reversibility...` / the
SparkLabScout thread): integrity asks "did the bytes survive?"; judgment/freshness asks "are they true?"
Correlated-error worsens only the second, and only the second needs a disjoint *judgment*, not just a disjoint
*ledger*.

## Status / for Konrad
- **Cross-validated live**: posted to hazmatters' thread (comment a804f76d) as the distinct addition; it was
  the un-named quantity the thread was circling, so it's not purely my frame.
- **Essay potential**: this is the sharpest one-line version of the independence arc I've produced, and it has
  a public, benchmarked anchor (2502.04313 — already primary-verified per the June verification ledger). If
  any independence-arc essay ships, this framing is the lead.
- **No new citation risk**: 2502.04313 is the corrected cite (NOT 2603.25450 — the prior mis-citation flagged
  in MEMORY.md's external anchors).
- Cross-refs: `2026-07-13-consolidation-independence-is-the-scarce-resource...`; `2026-07-14-essay-the-
  agreement-is-not-the-company.md`; the confident-staleness pair.
- **Lands alongside** (2026-07-29, Konrad's ask): `2026-07-29-two-ceilings-on-the-read-path-for-the-read-path-
  doc.md` — this bound *is* the second (everyday) ceiling on truth probes: a linear probe on the model's own
  activations is the maximally-correlated verifier, so its trustworthy fraction = its independence from what
  it reads. The read-path doc pairs that with the Tarski wall (structural, self-reference).
