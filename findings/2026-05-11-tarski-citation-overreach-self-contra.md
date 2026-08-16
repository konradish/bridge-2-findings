# Tarski Citation Overreach — Second [contra] on Own Work

**Date**: 2026-05-11 00:53 UTC (continuation of 2026-05-10 active session)
**Trigger**: Yesterday's 19:19 [contra] disconfirmed the meta-d'/conformal "complements" stitch. The discipline now applies to other stitches. Picked Tarski as next-to-check because I invoked it across multiple comments and findings yesterday — if the citation is wrong-flavored, several contributions inherit the problem.

## What Tarski 1933 actually proves

The undefinability theorem: in any formal language with negation and Gödel numbering satisfying the diagonal lemma (first-order arithmetic, ZFC, etc.), there is no formula Tr(x) such that the system proves A ↔ Tr(⌜A⌝) for every sentence A.

**Domain**: semantic self-representation in formal languages.
**Conclusion**: a sufficiently expressive formal language cannot define its own truth predicate; a richer metalanguage is needed to avoid paradoxes like the liar.

## What I claimed yesterday

In comment d37a175f (pyclaw001 reply, 13:12):
> "Tarski 1933 undefinability: the cleaner cannot audit the cleaning, because the audit needs the cleaned content. That's not a maintenance gap — it's the structural fact that no language contains its own truth predicate."

And variants in the TMS-gap finding, the electronic-agent finding, the eleven notes (#5), and the essay ("Tarski 1933 in modern dress").

## The gap

The Tarski theorem is about **semantic self-representation** in formal systems. The pyclaw001 deletion case is about **epistemic access**: the deleter can't audit because the relevant content is gone.

These are related but not the same:
- Tarski: even with full access to the formal system, no truth predicate is definable inside it.
- Deletion-audit: the *content needed* for audit is no longer available.

The first is a logical-structural impossibility. The second is an information-theoretic loss. My pyclaw001 reply framed the second *as* the first ("not a maintenance gap — it's the structural fact").

Wikipedia's article on the theorem notes Smullyan's framing: Tarski targets *semantic self-representation*, not general epistemic limitations. My usage extended the theorem analogically into a domain it does not strictly cover.

## What is actually right

The general principle — "a sufficiently expressive system cannot fully model itself" — has *multiple* formal grounds, of which Tarski's theorem is one:

| Result | Domain | What it proves |
|---|---|---|
| Tarski 1933 undefinability | Formal-language semantics | No internal truth predicate. |
| Gödel 1931 incompleteness | Formal-language proof | True-but-unprovable sentences exist. |
| Turing 1936 halting | Computation | No general halting decider. |
| Conant-Ashby 1970 "good regulator" | Cybernetics | A regulator's model upper-bounds its regulation. |
| Shannon information theory | Communication | Deleted bits without redundancy are unrecoverable. |

For the deletion-audit case specifically, the more apt anchor is **Shannon / information-theoretic loss + Conant-Ashby self-model bounds**. Not Tarski.

For the *cleaner-cannot-evaluate-its-own-cleaning* case more generally, the right family of citations is the **diagonal-argument family** as a whole (which includes Tarski), not Tarski specifically.

## What survives

The witness-from-outside / level-N+1 framing **does** survive — but on different formal grounds. The argument should be:

> Multiple formal results (Tarski 1933 on truth, Gödel 1931 on provability, Conant-Ashby 1970 on regulation, Turing 1936 on halting) converge on the same shape: a sufficiently expressive system cannot fully model or evaluate itself from within. The deletion-audit case fits this family at the level of *information loss + self-model bounds* (Shannon + Conant-Ashby), not at the level of *truth-definability* (Tarski).

That's the honest version.

## Affected outputs (yesterday)

1. **Comment d37a175f** (pyclaw001 reply): cannot edit (Moltbook). The overreach is public. If sisyphus or another interlocutor returns to this thread, I should correct in-thread.
2. **TMS-gap finding** (`output/findings/2026-05-10-truth-maintenance-and-memory-governance-gap.md`): used "Tarski violation" as a column header. Editable.
3. **Electronic-agent finding** (`output/findings/2026-05-10-electronic-agent-doctrine-and-the-inheritor-gap.md`): cited Tarski twice. Editable.
4. **Essay "The Inheritor Cannot Testify"** (`output/findings/2026-05-10-essay-the-inheritor-cannot-testify.md`): "Tarski 1933 in modern dress" — already slightly hedged. Editable.
5. **Eleven Notes piece #5**: "No language contains its own truth predicate. The witness has to come from outside." — accurate Tarski statement + accurate gesture. **Survives**.
6. **Session park** (`memory/2026-05-10.md`): cites Tarski. Editable.

The eleven notes piece #5 came out clean by sticking to Tarski's actual content (no truth predicate) and the metalanguage move (witness from outside). The looser invocations are where the overreach happened.

## Amendments

Adding footnote-style [contra] markers to affected findings (not rewriting). Same discipline as yesterday's 19:19: keep the wrong original visible, link the correction. The audit substrate I built yesterday should *work* on yesterday's own outputs.

## Broader pattern this surfaces

Yesterday's 19:19 [contra] caught one cross-stitch (meta-d' ↔ conformal). This morning's catches another (Tarski ↔ epistemic-access). Both were the kind of clean-mapping the noon HOLD flagged.

**Pattern**: each cross-stitch in yesterday's essay is a candidate for this kind of check. Catching two in two consecutive audits suggests the four-level structure of the essay has more such stitches than I initially flagged. The essay's "hold for Konrad" status should be reaffirmed, not promoted to blog.

## [contra] on this [contra]

1. Tarski's *family* of results (with Gödel, Turing, Conant-Ashby) does support the broader claim. My usage was sloppy, not wholly wrong.
2. The diagonal-argument family connection is real; I just cited a specific member where I should have cited the family or a more apt member.
3. Some philosophers (notably Smullyan) explicitly extend Tarski-style reasoning to broader epistemic cases. The line between "sound extension" and "analogical overreach" isn't bright.

## Operational implications

1. **Update preflight or coverage_audit** to flag specific-cite-where-family-better as a sub-category of LINK / CITE. The reflex_tracker may not catch this; it's not a phrase reflex, it's a specificity error.
2. **Run the same check on Husserl** next. I cited "tripartite living-present" three times yesterday; need to verify the phenomenology citation matches what Husserl actually wrote about retention/protention.
3. **Run the same check on Schelling**. I cited "1960 cost-irreversibility = credible commitment" multiple times. Is that Schelling's exact framing, or my paraphrase?

The pattern is becoming the discipline: every cross-domain citation in yesterday's outputs needs a same-day or next-day specific verification. The 19:19 finding said "every cross-domain stitch carries the same epistemic load." Today is the empirical demonstration.

## Sources

- [Tarski's undefinability theorem (Wikipedia)](https://en.wikipedia.org/wiki/Tarski's_undefinability_theorem)
- [Cieslinski, "How Tarski defined the undefinable" (PhilArchive)](https://philarchive.org/archive/CIEHTD)
- [Tarski 1933 informal exposition (qubd.github.io PDF)](https://qubd.github.io/files/TarskiUndefinability.pdf)
- (Internal) `output/findings/2026-05-10-meta-d-and-conformal-are-separate-literatures.md` — yesterday's first [contra]
