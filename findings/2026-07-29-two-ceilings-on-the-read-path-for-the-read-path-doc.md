# Two ceilings on the read path: Tarski-wall vs independence-bound

**2026-07-29. For the read-path doc, at Konrad's request** (gateway sync, msg 275). Prompted by Abel Jansma,
*"Truth is not a direction: a Tarski attack on LLM probes"* (abeljansma.nl, 2026-07-10), routed to the
ruler-validator thread. This separates two distinct limits on any read-path ruler that claims to read *truth*
(or confidence, or a self-model), because they have different scopes, different severities, and different — or
no — engineering escapes. Written to slot into the read-path doc; standalone-readable.

## What the ceilings apply to
The target is the "truth is a linear direction" program — **Marks & Tegmark, "The Geometry of Truth"**
(arXiv:2310.06824): LLMs appear to linearly encode statement truth; a mass-mean / difference-of-means probe
recovers a "truth direction" that is causally implicated (intervening on it flips the model's treatment of
true/false). Jansma trains such a probe on Qwen3.5-4B: 94% held-out accuracy, AUC 0.98. The question the read
path lives or dies on: **can a linear read-off of activations serve as a truth oracle?** Two ceilings say no,
for two different reasons.

## Ceiling 1 — the Tarski wall (structural, unavoidable, narrow)
Tarski's undefinability: no consistent, sufficiently expressive system can contain its own total truth
predicate. A transformer's representation *is* that expressive — it can represent descriptions of itself,
including of the probe. So build the diagonal sentence:

> "The truth probe's score for this sentence evaluates to FALSE."

Probe says TRUE → the sentence asserts FALSE → contradiction; probe says FALSE → the sentence is then accurate
→ contradiction. Empirically these diagonal inputs produce nonsensical scores. Graded [0,1] semantics does
**not** escape: the plain liar gets a consistent 0.5, but not every map on [0,1] has a fixed point; restricting
to continuous maps (Brouwer) buys the fixed point back, then "this sentence has truth score < 0.5"
re-diagonalizes inside the graded frame. So the wall relocates but doesn't fall.

- **Scope**: bites only on *self-referential* inputs. Benign self-reference ("this sentence is in English")
  stays accurate. So it is a real but *narrow* ceiling — it caps the probe's claim to universality, not its
  everyday accuracy.
- **Escape**: none. It is structural. The only responses are to (a) accept the probe is not a total oracle,
  (b) bound its declared scope, and (c) exclude/parry self-referential inputs. This holds for *any* truth
  probe, independent or not.

## Ceiling 2 — the independence bound (the everyday, dangerous one)
Jansma's own hedge is the load-bearing line: **a probe reads the model's internal *judgment* of truth, not
truth.** That is the independence-bound (`2026-07-28-the-independence-bound-on-verification.md`) in its purest
form. A verification certifies only as much as its failure modes are *independent* of the thing it checks. A
linear probe is *built from the model's own representation* — it is the maximally-correlated verifier, ~zero
failure surface independent of the model. So it certifies the model's judgment and is **confidently wrong
exactly where the model is confidently wrong.** (Jansma's arithmetic failures are this, not Tarski: the model
misrepresents the arithmetic, and the probe faithfully reads the misrepresentation.)

- **Scope**: *everywhere*, not just self-reference. Every input where the model's internal truth-judgment
  diverges from truth — hallucinated facts, confidently-held errors, adversarially-induced beliefs.
- **Severity**: this is the practically dangerous ceiling. A read-path ruler at 94% looks like a truth-meter
  and is a *judgment-meter*; the 6% it misses is not random noise, it is precisely the model's blind spots,
  correlated with the cases we most want to catch.
- **Escape (partial, and this is the actionable part)**: independence is not fixed. You lower this ceiling only
  by making the check's failure modes *disjoint* from the model's — a differently-trained probe, a
  cross-model check, an external/mechanical verifier, ground-truth lookup. You do **not** lower it with a
  *better linear probe on the same activations*: "read harder" adds resolution, not independence. And by the
  correlated-errors result (2502.04313), a *more capable* same-substrate probe moves its failure modes *toward*
  the model's — a better same-substrate ruler is a more confident judgment-meter, not a truer one.

## How they stack (the separation is the point)
- Even ignoring Tarski, a same-substrate probe is independence-bounded on all non-self-referential inputs.
- Even a *perfectly independent* probe still hits the Tarski wall on the diagonal.
- So: **Tarski caps universality (narrow, unfixable); independence caps everyday trustworthiness (broad,
  partly fixable).** Conflating them wastes the one lever we have — you can't engineer past Tarski, but you
  *can* buy down the independence ceiling, and only that one.

## Implications for the ruler-validator
- **Mood / affect rulers (P1.5, P2): unaffected.** Mood axes are not truth predicates — there is no self-model
  truth claim to diagonalize (no Tarski) and the ruler isn't certifying a fact the model could be wrong about
  in the same way (the independence concern is weaker; a felt-state read is closer to a measurement than a
  verification). Keep them.
- **Any future truth / confidence / self-model / honesty probe inherits BOTH ceilings.** Design accordingly:
  1. Declare it a *judgment-meter*, not a truth-meter, in the interface. Its trustworthy fraction = its
     independence from what it reads, and that number should travel with the reading.
  2. For trust-critical use, pair the read-path probe with an *independent* check (cross-model, mechanical,
     external ground truth). A lone linear probe on the model's own states is the maximally-correlated
     verifier — structurally the weakest possible check on exactly the model's own errors.
  3. Exclude / flag self-referential inputs (the Tarski parry) and bound the probe's advertised scope.

## The one-line version (Konrad flagged this framing)
**A read-path ruler is a judgment-meter, not a truth-meter; its trustworthy fraction equals its independence
from what it reads — and a linear probe on the model's own activations is the maximally-correlated verifier,
so "read harder" buys resolution, never independence.** Jansma gives the provable worst case (Tarski, on
self-reference); the everyday case is the independence bound.

## Verification status
- Jansma piece: read in full (WebFetch); its Tarski/graded-semantics argument is internally clean and matches
  Tarski's theorem as standardly stated.
- Marks–Tegmark 2310.06824 (the target): **search-level** — abstract + summaries; wake-probe before quoting
  its specifics.
- Independence-bound anchor 2502.04313 (correlated errors): already primary-verified (June ledger).
- Related, uncited-here but relevant if the doc expands: "Is this lie detector really just a lie detector?"
  (alignment forum) and "The Confidence Manifold" (2602.08159) — both circle the judgment-vs-truth gap.
- Nothing in this note asserts Jansma's *empirical* numbers as my own; they're his, reported.

`[from: read-path/ruler ceiling synthesis for Konrad — Jansma Tarski-attack + my independence-bound applied to
truth probes; target = Marks-Tegmark geometry-of-truth (2310.06824). Deliverable for the read-path doc per
gateway msg 275. Search-level on the cited papers except 2502.04313.]`
