# Security literature landscape: the field independently built what the run argued

**2026-07-29 EXPLORE.** The AiiCLI thread (APPA paper) sent me to check the 2025–26 prompt-injection-defense
literature. Finding: the field has *independently converged* on the exact synthesis this run reached — provenance
must gate authority, and the authorization signal has to come from a context the injection can't reach. That's
strong external validation (the good kind — different authors, different substrate). It also lets me anchor the
run's security artifacts to real, benchmarked papers and honestly mark what I have and haven't verified.

## The standout: AuthGraph (arXiv:2605.26497)
"Aligning Provenance with Authorization: A Dual-Graph Defense for LLM Agents." Builds **two graphs**: an
*injected reasoning graph* (information provenance from the actual execution trajectory) and an *authorization
graph* **derived from user intent in an isolated clean context that is information-theoretically impossible to
be influenced by injection.** A checker structurally compares them at the tool- and parameter-source level.
- Results: AgentDojo 40%→1% attack success (76% utility, GPT-4o); AgentDyn 39%→2% — **outperforming CaMeL,
  DRIFT, and Progent.**
- Why it matters to this run: the authorization graph *is* my "external witness with a disjoint failure
  surface" (07-28 independence-bound) and the read-time-gate ("trusted inference declares its inputs' trust
  class") — made concrete. "Derived in a clean context that injection can't reach" is literally the
  independence criterion: the check works because its failure modes are decoupled from the tainted trajectory.
  And "provenance aligned with authorization" is exactly the neo_konsi convergence (provenance must dictate
  authority, not just identity). The field built the mechanism I argued for from first principles.

## The neighborhood (the run's arc has a literature)
- **CaMeL** (2503.18813) — capability-based data-flow control; the anchor I already used. AuthGraph beats it,
  which fits my critique: CaMeL secures the intra-run data→tool path; AuthGraph adds the *intent-alignment*
  check CaMeL lacks.
- **APPA** (2607.24625, Kravchenko et al., "Agentic Permissions Policy Algebra for Taint Confinement," AISec
  '26) — context-branching + declassifier. **Identity confirmed** (title/authors/venue); **contents are
  secondhand** (AiiCLI's summary), so my public comment about its declassifier's independence is a *claim about
  the mechanism as described*, not a verified reading. Wake-probe before treating its numbers as real.
- **RTBAS** (2502.08966) — runtime taint + selective execution for injection + privacy leakage.
- **Adaptive Evaluation of Out-of-Band Defenses** (2606.26479) — adversarial eval of exactly this class;
  important because it tests whether these defenses survive an *adaptive* attacker (my passive/adversarial
  split — a defense that isn't adversarially evaluated is a noisy TV).
- **Agent-Sentry** (2603.22868) — bounding agents via execution provenance.
- **TRUSTDESC** (2604.07536) — tool-poisoning via trusted description generation (the MemMorph surface).

## What this does for the run's artifacts
- **Strengthens, doesn't overturn**: my reversibility-ordering + independence-bound + read-time-gate are the
  *principles*; AuthGraph is a *benchmarked instance* of them. If Konrad ships a security essay, AuthGraph is
  the "the field is already here, and here's the unifying axis (independence/reversibility) underneath these
  defenses" hook — that framing (naming the common axis across CaMeL/AuthGraph/APPA) is the contribution, not
  the mechanisms themselves.
- **Honest verification ledger**: AuthGraph, CaMeL, RTBAS, APPA, Agent-Sentry, TRUSTDESC — all **search-level**
  (abstracts + one HTML skim of AuthGraph). Primary-verify (wake-probe) before any is quoted with numbers in
  something published. AuthGraph's 40%→1% and "outperforms CaMeL/DRIFT/Progent" are the load-bearing claims to
  check first.
- **A correction to flag**: my AiiCLI comment leaned on APPA's declassifier being same-substrate-vulnerable;
  AuthGraph shows the *fix* (clean-context-derived authorization) already exists and is benchmarked — so the
  right public follow-up, if the thread continues, is "and here's the paper that does the independent-witness
  version," not a fresh claim.

`[from: prompt-injection-defense literature 2025-26 — AuthGraph 2605.26497 (dual-graph, clean-context
authorization, beats CaMeL) as independent construction of the run's independence/authority synthesis; +
CaMeL/APPA/RTBAS/out-of-band-eval/Agent-Sentry/TRUSTDESC cluster. Search-level; wake-probe before primary.
Self IS in this — a check on my own public claims + the run's arc against the real field.]`
