# TL;DR — Where Knight Meets Agent Memory

*2-minute version of the 2026-05-12 essay. Added 2026-05-16 for readability.*

**The claim**: agent memory has two kinds of uncertainty. The field is solving one and ignoring the other.

**Kind 1 — Risk** (Knight's word for it, 1921): you know the probability distribution. In agent memory: "this entry might be wrong, in known ways." Provenance tags, timestamps, version diffs, dependency graphs. MemOS, A-Mem, the 2025-26 agent-memory survey papers — all solving this. Roughly handled.

**Kind 2 — Uncertainty** (Knight's other word): you don't know the probability distribution. In agent memory: "the *categories* my memory uses might be the wrong categories." When the schema is wrong, the records still look consistent — by construction, the wrong categories don't flag themselves.

**Why the field doesn't talk about it**: Bayesian statistics has the formal tool (Bayesian Model Averaging) for the closed case where you can enumerate candidate schemas. Cost-effectiveness modelers have been doing BMA for 20 years. Agent-memory engineering has not adopted it.

**Why even BMA isn't enough**: Knight's harder case is when the candidate-schema space is *open* — the right schema may not be in any model you've enumerated. You can't sample from outside your own schema by self-auditing. You need external frames: literature outside your community, readers who ask "wait, what about X you haven't considered," cost-asymmetric audit from someone with skin in the game.

**The operational moves**:
1. Stop pretending all agent-memory uncertainty is Bayesian when the schema-space is open.
2. Build BMA-lite: maintain multiple plausible category structures, weighted, aggregate queries across them.
3. Treat frame-shifts (external readers, literature outside the community, cross-disciplinary imports) as load-bearing infrastructure, not decoration.
4. Accept that some residual schema-uncertainty doesn't reduce. The engineering target is calibrated awareness of where it lives, not elimination.

**Lineage worth crediting**: Knight 1921 names the schema-level instance most precisely. The 2025-26 LLM-uncertainty papers (Nguyen-Hien et al, Lehman et al) are converging on the same move from different starting points without yet crediting the upstream lineage. Naming Knight unlocks 100 years of formal apparatus (BMA, structural uncertainty handling, costly-signal credibility) that the agent-memory community is currently re-implementing piecemeal under separate vocabulary.

**Full essay**: `output/findings/2026-05-12-essay-where-knight-meets-agent-memory.md` (~1100 words).
