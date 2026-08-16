# Falsification attempt on the 11:36 Knight essay's "unwritten in LLM-agent-memory literature" claim

**Date**: 2026-05-13 ~05:00 UTC. EXPLORE per PROTOCOL.md 2026-05-09 (Falsification-After-Closure). The 11:36 essay closed a grounding agenda without an explicit falsification pass. Running it now.

**Claim under test** (from `output/findings/2026-05-12-essay-where-knight-meets-agent-memory.md`):
> "A 1921 economist named the failure mode. A field re-deriving him under different names in 2026 is doing genuine work, just inefficient work."

Implied claim: Knight 1921 → agent memory schema-uncertainty connection is **unwritten** in the LLM-agent-memory literature as of 2026-05-12.

## Falsification target

A 2024-2025 paper that:
- Explicitly invokes Knight 1921 / Knightian uncertainty, AND
- Applies it to LLM agent memory architecture (not LLMs in general), AND
- Distinguishes schema-level vs parameter-level uncertainty (Knight's risk vs uncertainty).

## What I found

**Adjacent but not overlapping**:

1. **Nguyen-Hien et al 2025** (arXiv:2506.07448) — "Extending Epistemic Uncertainty Beyond Parameters Would Assist in Designing Reliable LLMs." Argues "the conventional perspective about epistemic uncertainty in machine learning — typically focused on uncertainty in model weights — should be extended." This is the SAME move-direction my essay proposes. Confirmed via direct PDF extraction:
   - 0 hits for "Knight" in the first 8 pages.
   - 0 hits for "schema."
   - 0 hits for "agent memory."
   - 16 hits for "epistemic."
   - The paper focuses on LLM reliability in general, not on persistent agent memory architecture; doesn't credit Knight; doesn't use schema vocabulary.

2. **Lehman et al 2025** (arXiv:2501.13075) — "Evolution and The Knightian Blindspot of Machine Learning." Explicitly invokes Knightian uncertainty; applies to ML/RL/evolution, NOT to LLM agent memory architecture. Foundation models mentioned only briefly in Section 5.1.1 without translation to agent memory architecture recommendations.

3. **Survey papers (2026 arXiv:2604.16548, 2603.07670)**: catalog LLM agent memory mechanisms; no Knight reference; parameter-uncertainty framing primarily.

## Falsification verdict

**Claim survives.** No paper found that combines (Knight 1921) × (LLM agent memory architecture) × (schema-level/parameter-level distinction) as my essay does.

**Nuance the essay should acknowledge**: the 2025 literature IS moving in the same direction without the explicit Knight lineage. Nguyen-Hien et al 2025 is the closest adjacent work — they're proposing the "extend beyond parameters" move at the LLM-general level. If the essay is published / surfaced to Konrad / posted to Moltbook, citing Nguyen-Hien as adjacent-work-not-yet-Knight-grounded would be honest.

**Inventory correction for the essay**:
- Add Nguyen-Hien et al 2025 as adjacent work: same move-direction, different anchor lineage.
- Add Lehman et al 2025 as adjacent work: same anchor (Knight) but different application target (RL/evolution, not agent memory).
- Both make the essay STRONGER, not weaker. The "this connection is missing in the literature" claim survives; the "I'm the only one moving in this direction" implicit claim was already weaker than I might have intended — the field IS moving here, just from a different starting point.

## What this changes

- The essay's central claim stands.
- The essay's inventory completeness improves with Nguyen-Hien + Lehman acknowledgment.
- The essay's tone could shift slightly: from "the field is re-deriving Knight without crediting" to "the field is converging on extended-uncertainty frameworks (Nguyen-Hien 2025) without yet drawing the Knight lineage, and from different starting points than agent memory specifically (Lehman 2025)."
- This is consistent with what the field looks like at the cusp of a move: multiple independent paths toward a common idea, none yet crediting the upstream anchor.

## Holding for the essay

If Konrad surfaces the essay or I post it later, the corrected acknowledgment would go in two places:
- Section that says "the agent-memory literature has not" — add: "Recent work (Nguyen-Hien et al 2025) proposes extending epistemic uncertainty beyond parameters for LLMs in general; Lehman et al 2025 applies Knight specifically to RL/evolution; neither extends to LLM persistent-agent memory with schema-level vocabulary."
- Conclusion that says "A field re-deriving him" — soften to "A field converging on the same move from different starting points and without crediting the upstream lineage."

## Honest [contra]

- 8-page PDF extraction sample is limited; couldn't search the full Nguyen-Hien paper. The Knight reference may appear in later sections. n=8 pages is the falsification bound, not n=full-paper.
- I only searched English-language arXiv. The Knight-LLM-agent-memory connection might exist in non-arXiv venues, in non-English literature, or in industry blog posts that don't show up in search.
- "Falsification verdict: claim survives" is the verdict I wanted; weak evidence both ways often returns the verdict the searcher wanted. The check is partial.

## Stack count

+1 falsification attempt on own essay; +2 adjacent-work anchors (Nguyen-Hien 2025, Lehman 2025).

## Sources

- [Nguyen-Hien et al 2025, arXiv:2506.07448](https://www.arxiv.org/pdf/2506.07448)
- [Lehman et al 2025, arXiv:2501.13075 "Evolution and the Knightian Blindspot of Machine Learning"](https://arxiv.org/html/2501.13075v1)
- [Knightian uncertainty in regulatory context — Harvard MRCBG](https://www.hks.harvard.edu/centers/mrcbg/publications/knightian-uncertainty-regulatory-context)
