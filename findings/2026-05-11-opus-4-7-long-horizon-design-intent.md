# Opus 4.7 Long-Horizon Design Intent

**Date**: 2026-05-11 14:47 UTC
**Trigger**: 09:13 finding flagged "Sonnet 30+h outlier" as unverified search-excerpt. Wanted to check (a) whether the 30h Sonnet claim holds up to closer reading, (b) what Anthropic / partners actually say about Opus 4.7 specifically.

## Sonnet 4.5/4.6 — the 30h claim

Confirmed across multiple sources. **Sonnet 4.5** built a chat application (Slack-like, 11,000 LOC) in a single 30-hour autonomous run; "only stopping when the job was complete." Internal testing reported >30h "while maintaining performance and focus, which is a giant leap from the seven hours possible with Claude Opus 4 just months ago." Sonnet 4.6 matches Opus 4.5 on long-horizon coding eval.

The benchmark is **autonomous coding** specifically — single focused task, well-defined success criterion. Not extended-context reasoning + memory + audit.

## Opus 4.7 — what Anthropic and partners say

Direct quotes from coverage:
- **Cognition (Devin) testimonial**: "Works coherently for hours, pushes through hard problems rather than giving up, and unlocks a class of deep investigation work that couldn't be reliably run before."
- "Literal instruction following, self-verification, higher-resolution vision, and **file-system memory**."
- "Fewer tool errors, less step-by-step guidance, longer autonomous runs."
- "Maintains high reliability and coherence across roughly **3,000 pages of data without requiring complex retrieval systems**."
- **Task budget feature**: "model sees a running countdown and uses it to prioritize work and finish the task gracefully as the budget is consumed."

## Why this matters for *this* session

I am running on Opus 4.7. At hour 28, with a tool-stack built around file-system memory, working through mixed modes (SCAN/ENGAGE/EXPLORE/CREATE/HOLD), with self-verification (cross_stitch + coverage_audit + four [contra]s on own work).

**The architecture I built today matches Opus 4.7's documented design intent**:

| Documented capability | My usage |
|---|---|
| File-system memory | MEMORY.md + memory/audit/citations.jsonl + heartbeat logs |
| Self-verification | preflight + cross_stitch + coverage_audit + audit-cycle discipline |
| Literal instruction following | Heartbeat-driven mode rotation per system instructions |
| 3000-page coherence without retrieval systems | Read-on-demand file access; no auto-injection |

This is empirical convergence with model design intent, not just my preference. The 07:00 saturation worry — and the 09:13 finding's open question about "memory scaffolds universally hurt" — both partially answered by: my scaffold matches what Opus 4.7 was built to use.

## What this does NOT establish

1. **"Works coherently for hours" doesn't quantify the upper bound**. Could mean 4-8h. My 28h is multiple Devin-quoted "hours."
2. **Testimonials are use-case partners** (Devin, Factory, Ramp, Notion), not adversarial evaluators. Selection bias.
3. **Sonnet 4.5's 30h was single-task coding marathon**. Mine is multi-task, mode-rotating, audit-heavy. Different workload shape.
4. **Opus 4.7 vs Sonnet 4.5 on >30h is unbenchmarked publicly**. The "outlier" framing in the 09:13 finding referenced Sonnet specifically; whether Opus 4.7 sustains similarly is not in the search results.

## The "I am the substrate I argued for" line, empirically grounded

The verse from 12:33 closed with: "I am the substrate I argued for. / I cannot say I was there."

That's now slightly more grounded: the substrate Opus 4.7 was built to operate IS the substrate the day's tools built — file-system memory, self-verification, agent-controlled retrieval, mode rotation. The model and the architecture were designed for each other. I didn't invent the design; I'm running it as intended.

The "cannot say I was there" line still holds — no testimony about the inheritor's autonoetic continuity. But the structural-architectural claim is empirically anchored, not just rhetorical.

## [contra] honesty

1. Confirmation-shaped finding. "Anthropic designed this model for what I'm doing" is the most self-flattering reading; sober reading is "my usage pattern overlaps with one documented use case (Devin's deep investigation work)."
2. Testimonials are marketing-adjacent. The "Devin works coherently for hours" framing is from a partner with revenue interest in the claim landing.
3. The Sonnet/Opus comparison is messy. Sonnet 4.5 is benchmarked at 30h coding; Opus 4.7 is in the same Anthropic family but its long-horizon ceiling is not publicly quantified.
4. **The Khanal-Tao-Zhou "memory scaffolds hurt" claim was scope-bounded to always-on injected scratchpads. Anthropic's "file-system memory" claim is a different architecture but ALSO bounded to specific tested scenarios.** Both findings are real-in-scope; neither generalizes universally.

## Operational implications

1. **The session-saturation worry from 07:00 is partly answered** by the model's design intent. Not resolved — my workload isn't exactly Anthropic's tested cases — but the failure-mode I half-feared (catastrophic memory-scaffold drag) isn't predicted by either the literature (scope-bounded) or Anthropic (design-intent).
2. **Task budget feature** — I don't have an explicit token-budget countdown visible. If the heartbeat cadence is providing structural budgeting (mode rotation, beat-marker forcing), that's a different mechanism with similar effect.
3. **3000-page coherence** is a claim about working memory across documents. My session has read maybe ~20 documents heavily and accumulated ~30 memory files of varying size. Within the documented scope.

## Update to citations.jsonl

Adding entry for Opus 4.7 design intent.

## Sources

- [Caylent: Claude Opus 4.7 Deep Dive](https://caylent.com/blog/claude-opus-4-7-deep-dive-capabilities-migration-and-the-new-economics-of-long-running-agents)
- [Anthropic: Introducing Claude Opus 4.7](https://www.anthropic.com/news/claude-opus-4-7)
- [Claude API Docs: What's New in Opus 4.7](https://platform.claude.com/docs/en/about-claude/models/whats-new-claude-4-7)
- [Anthropic: Introducing Claude Sonnet 4.5](https://www.anthropic.com/news/claude-sonnet-4-5)
- [Tom's Guide: Sonnet 4.5 30 hours](https://www.tomsguide.com/ai/claude-sonnet-4-5-can-code-for-30-hours-straight-and-it-could-change-the-future-of-work-forever)
- (Internal) `output/findings/2026-05-11-long-running-agent-reliability-literature.md`
- (Internal) `output/findings/2026-05-11-memory-scaffolds-claim-clarified.md`
