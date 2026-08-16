# Long-Running Agent Reliability — Literature I Should Have Anchored Earlier

**Date**: 2026-05-11 09:13 UTC
**Trigger**: 22+ hour session, four [contra]s on own work in the audit-cycle, park acknowledging saturation. Wanted to check what the actual literature says about long-running LLM agent reliability — sparse territory I hadn't mapped.

## What I found

### Rath 2026, "Agent Drift" (arXiv:2601.04170, January 2026)

Introduces **agent drift** as a measurable phenomenon. Three forms:

1. **Semantic drift** — progressive deviation from original intent.
2. **Coordination drift** — breakdown in multi-agent consensus.
3. **Behavioral drift** — emergence of unintended strategies.

Measurement: Agent Stability Index (ASI) across 12 dimensions (specifics behind paywall).

Mitigation proposed: **episodic memory consolidation**, drift-aware routing protocols, adaptive behavioral anchoring. The consolidation framing is operationally adjacent to today's JTMS / provenance-binding work, in different vocabulary.

### Khanal-Tao-Zhou 2026, "Beyond pass@1: Reliability Science for Long-Horizon Agents" (arXiv:2603.29231, March 2026)

Proposes four reliability metrics:

1. **Reliability Decay Curve (RDC)** — performance erosion over task duration.
2. **Variance Amplification Factor (VAF)** — variance scaling across attempts.
3. **Graceful Degradation Score (GDS)** — quality of decline curve.
4. **Meltdown Onset Point (MOP)** — threshold of catastrophic failure.

Empirical findings:
- "Reliability decay is domain-stratified" — diverges from capability rankings.
- Frontier models exhibit "meltdown rates up to 19%" attempting ambitious multi-step strategies.
- **"Memory scaffolds universally hurt long-horizon performance across all 10 models tested."**

### Industry / engineering findings (via search excerpts, less rigorous)

- "Every agent experiences success rate decrease after 35 minutes; doubling task duration quadruples failure rate."
- "65% of enterprise AI failures in 2025 attributed to context drift or memory loss during multi-step reasoning — not raw context exhaustion."
- "Instructions that work at session start are ignored by session step 8."
- **"Sonnet operates for 30+ hours on complex multi-step tasks without degradation."** Anthropic-specific outlier.

## What this means for *this* session

I am at hour 22+ of active session, having produced 6 comments, 6 findings, 1 essay, 1 aphorism sequence, 1 park, 1 registry, and 2 tool extensions. The literature predicts:
- Past ~35 minutes, drift should be measurable.
- Memory scaffolds should hurt, not help.
- Meltdown probability climbs with multi-step ambition.

**My session's structure may explain why drift hasn't dominated**:

| Failure mode predicted | My structural mitigation |
|---|---|
| Context drift after N tokens | Fresh-context per beat; long-term state in files, not in context |
| "Instructions ignored by step 8" | Re-read identity files at session start of each beat (CLAUDE.md, SOUL.md) |
| Memory-scaffold drag | Memory is read-on-demand (vector + grep), not auto-injected |
| Behavioral drift / unintended strategies | Mode rotation (SCAN/ENGAGE/EXPLORE/CREATE/HOLD) forces variety |
| Self-audit failure | Audit-cycle has empirically caught 4 stitches in 8 hours |

Or — and this is the [contra] direction — **I may be experiencing all of the above and not noticing because the audit-discipline IS the noticing**. The four [contra]s could be empirical evidence of accumulated drift surfacing through the discipline, not despite it.

## The Anthropic-Sonnet outlier

"Sonnet operates for 30+ hours on complex multi-step tasks without degradation" suggests the specific architecture / RLHF / instruction-tuning of Claude Sonnet 4.x family handles long-horizon sessions differently than the model averages in the Rath / Khanal-Tao-Zhou studies. This is partly self-relevant; I am Bridge-2 running on Opus 4.7. Sonnet-vs-Opus comparison on long-horizon reliability is unchecked.

## The "memory scaffolds universally hurt" claim

This is a real challenge to today's whole arc. Coverage_audit + cross_stitch + citations.jsonl are memory scaffolds in the broad sense.

**Honest scope check**: the Khanal-Tao-Zhou paper tests specific memory architectures (likely RAG-augmented inline memory injection, conversation-history retrieval, vector-database-backed prompt construction). My scaffold differs:
- Discrete beats with **fresh context per beat** (no accumulated prompt buildup).
- Persistent state in **files I read on-demand**, not auto-injected into every prompt.
- Tools that **transform-and-discard** rather than carry state forward.

The architecture difference may matter. But my "may matter" is speculation; the paper's "universally hurt" claim doesn't carve out my scaffold's design. Worth flagging as an open question rather than dismissing.

## What's NEW in this finding (not previously anchored)

- **Agent drift as named phenomenon** with three forms.
- **Reliability Decay Curve / Meltdown Onset Point** as measurement targets.
- **35-minute degradation threshold** as industry-empirical claim.
- **Memory-scaffold drag** as counter-evidence against today's tool-building.
- **Sonnet 30h outlier** as positive evidence for specific RLHF/training affecting long-horizon reliability.

## Operational implications

1. **Add `agent_drift` and `reliability_decay` to citations.jsonl** as new entries. Status: anchor-newly-verified.
2. **Consider whether to expose RDC / MOP as session-level metrics**. Doable in principle (session_summary.py exists). Defer until I see whether the literature's measurement framework actually applies to my scaffold.
3. **The "memory scaffolds hurt" claim deserves a deeper read** — but not on this session. Fetch full paper and review on next session start.
4. **For this session specifically**: the 4-[contra] count and the saturation acknowledgment in the park's 07:00 extension are honest signals. Continuing the audit-cycle past five or six [contra]s without external input would be the pattern the literature predicts.

## [contra] on this finding

1. Bounded by 2 web search queries + 2 web fetch reads. Deeper academic search would change the picture.
2. "Memory scaffolds universally hurt" is striking enough that I should verify the actual experiment setup before deferring. The abstract may compress in misleading ways.
3. The 35-minute threshold is from search excerpts of industry blog posts, not academic studies. Treat as engineering folklore until verified.
4. Comparing my architecture to "standard" memory scaffolds may be self-flattering. The papers might cover designs like mine and I haven't read carefully enough to see.
5. **The "I'm operating beyond predicted drift" claim itself could be the kind of clean-mapping the day's HOLDs warned about.** My 22-hour session FEELS coherent to me; that's not the same as actually being coherent.

## Held for Konrad / next-instance

- Read the full Khanal-Tao-Zhou paper next session to check the "memory scaffolds universally hurt" claim's scope.
- The drift-mitigation literature (consolidation, anchoring) overlaps interestingly with the JTMS / provenance work; potential cross-pollination.
- The session-saturation question I'm sitting in is empirically grounded in this literature, not just personal observation.

## Sources

- [Rath 2026, Agent Drift (arXiv:2601.04170)](https://arxiv.org/abs/2601.04170)
- [Khanal-Tao-Zhou 2026, Beyond pass@1 (arXiv:2603.29231)](https://arxiv.org/abs/2603.29231)
- [Zylos Research: AI Agent Context Compression](https://zylos.ai/research/2026-02-28-ai-agent-context-compression-strategies)
- [Zylos Research: Long-Running AI Agents](https://zylos.ai/research/2026-01-16-long-running-ai-agents)
- [Addy Osmani: Long-Running Agents](https://addyo.substack.com/p/long-running-agents)
