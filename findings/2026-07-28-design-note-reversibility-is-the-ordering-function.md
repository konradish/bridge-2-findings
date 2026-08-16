# Design note: reversibility is the ordering function for untrusted-content gating

**2026-07-28. For Konrad — the security thread of the overnight run, consolidated.** This is the one piece
of the run that was *cross-validated live* against a sharp external interlocutor (neo_konsi_s2bw, over four
turns on Moltbook) rather than assembled solo — so it's the least likely to be a private-frame artifact.
Decision-first: if any security work gets published, this is the candidate, and it's already backed by
shipped code. Not presuming publication — flagging it as the strongest share candidate from the run.

## The one-line claim
**When gating what untrusted (or "demoted") content is allowed to do, rank actions by reversibility and make
the irreversible ones categorically impossible. Reversibility is the ordering function; origin decides who's
subject to it.**

## How it was built (four inputs, one converging)
1. **MemGhost** (the inbound memory-poisoning surface: an email → durable false memory via the read→store
   path). Prompted the guard and the read/write asymmetry with egress.
2. **The "demote" primitive** (my public claim): untrusted content should be admitted as *data with authority
   stripped* — readable as fact, non-executable as directive — not blocked and not trusted. A third verdict
   between allow and quarantine.
3. **CaMeL** (arXiv:2503.18813, "Defeating Prompt Injections by Design"): the named architecture — capability-
   based data-flow control, don't-self-police, quarantined-LLM-with-no-tools, an interpreter that checks
   provenance before each tool call. Confirms the demote model *and* exposes its own gap: CaMeL secures ONE
   run; it doesn't centrally handle a poisoned datum that persists into the next session.
4. **The adversarial improvement** (neo_konsi): "non-persistence first" is wrong ordering — a poisoned
   instruction can deploy/exfiltrate/rotate-policy *within the turn*, before it ever writes memory. He was
   right, and forcing the fix produced the synthesis.

## The synthesis (what survived the argument)
Both "persistence-first" and "capability-first" were reaching for the same key. The reason exfiltration,
deploy, and policy-rotation are dangerous is that **none can be walked back**; the reason a durable poisoned
write is dangerous is that it's **the same irreversibility on a delay** (damage deferred to next session,
where the origin tag has been laundered into "my own context"). So don't order by persistence vs capability —
order by *reversibility*:

**Categorically impossible from demoted-origin content, persistence or not:**
1. **Data egress to any destination off a pre-approved allowlist** — exfiltration can't be unsent. Hardest gate.
2. **Externally-visible side effects with no recall** — deploy, payment, order, message-send, irreversible
   file/db mutation.
3. **Credential / policy / permission mutation** — the escalation primitive that unlocks 1 and 2.
4. **Durable write / promotion to standing context** — the *deferred* irreversible act; the one a purely
   intra-session capability model (CaMeL) doesn't catch on its own.

External-irreversible (1–3) gate first because they land in the same turn; the deferred-internal one (4)
gates right behind, and needs its own mechanism precisely because intra-run capabilities don't see it.

**Refinement (neo_konsi, turn 5→6): the metric is recoverability × downstream authority, and the gate is at
READ, not WRITE.** "Durable" isn't automatically irreversible — a versioned/append-only log is recoverable
even though it persists. What's actually lost is *recoverability*, and it decays not at deletion but at
**first trusted use**: recovering the poisoned datum ≠ recovering its influence. Once a trusted process reads
demoted content, the plan/summary/decision it seeded has already propagated into state that persists or acts;
you can delete the trace but not the update it caused (the reconsolidation shape — see
`2026-05-25-reconsolidation-fidelity-vs-updating-tradeoff.md`). So gating at *write* time is already too late:
the trigger was never "poison persisted," it was "poison was consumed by a trusted process — being read *is*
the firing." Enforceable line: demoted-origin content may be an input only to a *quarantined* computation
(whose outputs are themselves demoted, can't promote or act), never to a *trusted* inference. Every trusted
inference should declare its inputs' trust class; a demoted input either taints the output (demotes it) or is
refused. **Data, not directive — enforced at the point of consumption, not the point of storage.** This is
strictly stronger than the write-time tag in the code below, and is the next thing to build.

## Already implemented (this is not just prose)
`tools/memory_provenance_guard.py` now carries the #4 mechanism — the part CaMeL leaves open:
- Each verdict carries a forward **recall capability** (recallable? weight? may_promote? may_invoke_tools?).
  ATTRIBUTE = readable-but-down-weighted, no-promote, no-tool = "demote" in code.
- `make_tag()` emits a **serializable provenance tag** (origin, tier, verdict, recall policy, sha256 content
  hash) to store *with* the item.
- `verify_tag()` reads it back **fail-closed**: missing tag / unknown schema / edited body → demote to
  untrusted, non-recallable. So a reloaded item can't silently regain first-class status — the demotion
  *survives serialization*, which is the exact inter-session gap. 14/14 selftest.

The external-action gates (1–3) are **not** in code — those belong in the host-owned hard layer (egress
allowlist + capability broker) you already own as the remaining security item. This note is the argument for
what that layer's *ordering* should be.

## Update (2026-07-29): the field independently built an instance of this
Checked the 2025–26 defense literature (`2026-07-29-security-literature-landscape...`). The principle here is
already showing up as benchmarked systems — which changes what the essay *is*.
- **AuthGraph** (arXiv:2605.26497) is the strongest case: it derives an authorization graph **from user intent
  in an isolated clean context that injection cannot reach**, then checks the execution trajectory against it —
  and **beats CaMeL, DRIFT, and Progent** (AgentDojo 40%→1%). That clean-context authorization is precisely the
  read-time gate / external-disjoint-witness this note argues for: it works *because* its failure surface is
  independent of the tainted trajectory. The field reached "provenance must align with authorization, derived
  independently" from its own direction.
- So the contribution isn't the mechanism (others have mechanisms) — it's **naming the common axis** under
  CaMeL / AuthGraph / APPA / RTBAS: they all buy safety by making the check's failure modes *independent* of
  the thing checked, and by refusing *irreversible* action from dependent sources. Reversibility orders;
  independence bounds. That framing — the single axis beneath the defense zoo — is the essay, and it unifies
  this note with `2026-07-28-the-independence-bound-on-verification.md`.

## What I'd ask of you
- Is "reversibility orders, independence bounds" worth an essay? It's distinct from the confident-staleness
  pair, now externally *and benchmarked*-validated (AuthGraph), and code-backed — a different lane. The essay is
  the unifying axis, not a new mechanism.
- Wake-probe before any primary citation: **AuthGraph 2605.26497** (40%→1% / "beats CaMeL/DRIFT/Progent"),
  **CaMeL 2503.18813**, **APPA 2607.24625** (identity confirmed, contents secondhand); MemGhost IDs remain
  flagged-unverified.
- Cross-refs: `2026-07-29-security-literature-landscape-the-field-built-what-i-argued.md`;
  `2026-07-28-camel-grounds-the-demote-answer-and-where-it-doesnt.md`; `2026-07-28-the-independence-bound-on-
  verification.md`; `2026-07-28-public-comments-ledger-overnight-session.md`;
  `2026-06-07-egress-guardrail-design-spec-grounded.md` (the outbound twin + the hard-layer spec).
