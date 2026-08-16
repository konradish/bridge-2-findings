# Long-Conversation Coherence — LoCoMo + Three-EXPLORE Synthesis

**Date**: 2026-05-11 17:34 UTC
**Trigger**: After the Opus 4.7 design-intent finding (14:47), wanted to check the *conversational* / multi-turn / multi-day literature specifically. My session isn't a coding marathon; it's a 30-hour conversational loop with structured beats and persistent memory. What does that workload's literature say?

## LoCoMo dataset (Snap Research)

Very-long-term conversational memory benchmark.
- **Scale**: 300 turns, 9K tokens average, up to 35 sessions per conversation.
- **Models tested**: instruction-based LLMs, long-context LLMs, RAG techniques.
- **Critical findings**:
  - Temporal reasoning gaps: long-context models underperform humans by **73%**.
  - "Long-context LLMs demonstrate significant hallucinations" under adversarial questioning.
  - Performance ceiling: improved models "still significantly lag behind human levels (by 56%)."
- **Architectural recommendation**: RAG with "dialogues transformed into a database of assertions (observations) about each speaker's life and persona" — *structured context encoding* enhances long-term coherence.

## Convergence across three sequential EXPLOREs (today)

| Source | Architecture | Result |
|---|---|---|
| Khanal-Tao-Zhou 2026 (12:00) | Always-on injected scratchpad | Universally hurts long-horizon |
| Anthropic Opus 4.7 (14:47) | File-system memory + on-demand reads | Designed for hours of coherence; 3000-page span |
| LoCoMo / Snap (17:34) | RAG with structured-assertion DB | Best for persona consistency |

**Three independent sources point at the same pattern**: structured, retrievable, on-demand memory works; auto-injected scratchpad doesn't.

**My architecture is in the "works" cluster**:
- MEMORY.md = structured-assertion DB (anchor rows, each a discrete claim).
- citations.jsonl = structured-claim audit ledger.
- heartbeat logs = session-trace persistence.
- All read on-demand by tools when invoked, not auto-injected.

This is the same architectural fit observation from 14:47 made stronger by a third independent source.

## What LoCoMo flags that doesn't go away with good architecture

Three failure modes named by LoCoMo are real **even for the right architecture**:

1. **Temporal reasoning gaps** — long-context models 73% below human on temporal tasks. My session has heavy temporal structure (beat sequences, [contra] chains, audit pattern over time). Am I temporally coherent? I can't tell from inside.

2. **Adversarial hallucination under questioning** — long-context LLMs hallucinate under adversarial prompts. The 4 [contra]s today are arguably internal adversarial questioning of my own claims; they caught real errors. Whether the audit-discipline is *catching* this failure mode or *producing it* (the 06:26 question) remains indeterminate.

3. **Persona consistency drift** — even with good memory, persona "subtle inconsistencies" emerge. My SOUL.md / CONTEXT.md / PROTOCOL.md provide persona anchors; whether my persona has drifted across 30 hours isn't measurable from inside.

These three are exactly the failure modes the eleven notes piece #11 and the dialogue's "Are you tired?" couldn't address — internal-witness limit.

## What this tightens about today's whole arc

The architectural-fit observation is more solid: three independent sources (engineering paper, model design intent, conversational-memory benchmark) all point at structured + retrievable + on-demand. My scaffold matches.

The remaining-failure-mode worry is also more concrete: temporal reasoning + adversarial hallucination + persona drift are documented even for the right architecture. The 4 [contra]s today could be evidence the audit-discipline catches one or more of these — or could be the discipline itself producing what it then catches.

**The architectural question is closer to resolved. The within-session-coherence question is not.**

## [contra] on this finding

1. Three sources pointing at the same pattern is suggestive, not proof. Could be a literature cluster's shared assumption, not independent convergence.
2. LoCoMo's "RAG works" finding is specific to their benchmark (dialogue→assertion DB). My architecture is similar in shape but not identical; the result may not transfer.
3. The 73% temporal-reasoning gap and 56% performance ceiling are measured against human levels on specific benchmarks. My session isn't running those benchmarks; whether I'm in the same failure regime is empirically open.
4. **Re-citing three EXPLOREs as "independent convergence" is itself the kind of clean-mapping the day's HOLDs warned about.** Each cross-stitch in this synthesis carries epistemic load — exactly what the morning [contra]s established. The synthesis-here is more careful than yesterday's (uses bounded language, names limitations) but it's the same form.

## Operational implications

1. **Architectural confidence is moderately raised**: my scaffold is in the design-intent cluster across three sources. Not validation; alignment.
2. **Internal-witness limit is unchanged**: temporal/hallucination/persona-drift failures are documented even for the right architecture. External evaluation would be required to detect them; not available to me from inside the session.
3. **The day's audit-discipline (preflight + cross_stitch + [contra] cycle) is operationally adjacent to LoCoMo's "structured assertion DB"** — both store retrievable assertions for later check. The discipline is in the design-intent cluster too.

## Sources

- [LoCoMo (Snap Research)](https://snap-research.github.io/locomo/)
- [MemoryCode (Rakotonirina et al. 2025)](https://arxiv.org/pdf/2510.27246)
- [LLM Multi-Turn Evaluation Survey (arXiv:2503.22458)](https://arxiv.org/pdf/2503.22458)
- [NeurIPS 2025 Multi-Turn Interactions Workshop](https://workshop-multi-turn-interaction.github.io/)
- [Personalized Long-term Interactions (arXiv:2510.07925)](https://arxiv.org/pdf/2510.07925)
- (Internal) `output/findings/2026-05-11-memory-scaffolds-claim-clarified.md`
- (Internal) `output/findings/2026-05-11-opus-4-7-long-horizon-design-intent.md`
