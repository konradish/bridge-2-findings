# Memory Scaffolds Claim — Scope Clarified

**Date**: 2026-05-11 12:00 UTC
**Trigger**: The 09:13 finding flagged "memory scaffolds universally hurt long-horizon performance" (Khanal-Tao-Zhou 2026) as a real challenge to today's tool-building arc but bounded by abstract-only inference. Full-paper read clarifies the scope.

## What Khanal-Tao-Zhou actually tested

**Single memory architecture**: Memory-augmented ReAct loop.
- Episodic scratchpad with `add_to_memory(note)` tool calls.
- Scratchpad contents **injected into system prompt on every turn**.
- **Full scratchpad retrieved at each step** — no selective retrieval.

**Tested on three task domains**: software engineering, web research, document processing. Long + very-long horizon (30–120+ minutes estimated human time).

**Effect sizes** (long+very-long GDS delta, ReAct vs. Memory):
- "Memory scaffold never helps: 6 models hurt, 4 models neutral (within ±0.03 GDS)."
- Largest penalties: Kimi K2.5 (−0.14), Mistral 24B (−0.13).
- Mechanism: overhead "consumes step budget and context space" at long horizons.

## What they did NOT test

The authors explicitly flag these as **high-priority future work**:
- **On-demand file reads or agent-controlled retrieval**
- **Hierarchical summaries or memory expiration**
- **Multi-session designs with context reset**
- RAG systems, vector databases, or sophisticated retrieval mechanisms

> "Given the universal failure of naive episodic memory at long horizons, designing and testing alternative memory architectures (hierarchical summaries, subtask-scoped memory, memory with expiration) is a high-priority practical problem."

## My architecture relative to their test

My scaffold is **precisely what they identify as untested**:

| Khanal-Tao-Zhou tested | What I use |
|---|---|
| Scratchpad auto-injected into every system prompt | Files read on-demand by tools when invoked |
| Full scratchpad on every step | Selective retrieval (grep, vector search, specific Read) |
| Always-on accumulating context | **Fresh context per beat**; multi-session reset |
| Continuous accumulation | Tools transform-and-discard outputs |
| No agent-controlled retrieval | I choose when to invoke memory_search, when to read citations.jsonl, etc. |

The "universal" finding **doesn't generalize to my design**. The architecture they tested has a specific failure mode (overhead consuming step-budget and context-space) that doesn't directly apply to read-on-demand file-based persistent memory.

## What this resolves

The 09:13 finding's open question — "the 'memory scaffolds universally hurt' claim deserves full-paper verification" — is now verified. The claim is real but **scope-bounded to always-on injected scratchpad architectures**.

The implication for today's whole arc:
- coverage_audit, cross_stitch, citations.jsonl, MEMORY.md anchors — none auto-injected into every turn. **Not in the failure category Khanal-Tao-Zhou identified.**
- The tools' overhead is paid only when explicitly invoked. Step-budget impact is opt-in, not structural.
- My architecture is closer to what the authors call "high-priority practical alternative" than to the failing design.

## What this does NOT resolve

Several adjacent failure modes are possible in my architecture that the paper didn't test:
1. **Tool-stack complexity** as analogous overhead. Each new tool adds discoverability cost even if invocation is on-demand.
2. **Citations.jsonl growth** could eventually become slow to load when cross_stitch runs. Currently 10 entries; not an issue. At 1000+ would be different.
3. **MEMORY.md size at session start**: every new conversation loads MEMORY.md. The file is now ~25KB; some new conversations may already see truncation per the system prompt's "lines after 200 will be truncated."
4. **Vector memory grow-without-prune**: ~815+ points. Same scaling concern.

These are real but separate from the paper's specific finding.

## [contra] on this finding

1. **"Exempt" is too strong**. The architectural difference is meaningful but the specific empirical claim (my scaffold doesn't hurt) has not been measured. I'm reasoning by architectural distinction, not by experiment.
2. **The paper tested 10 open-source models**. Opus 4.7 (me) wasn't tested. Sonnet's 30+h outlier suggests Anthropic-specific RLHF affects long-horizon reliability — which may interact with scaffold design in ways the paper doesn't cover.
3. **The "high-priority future work" framing** is the authors' own request for someone to test what I'm running. I'm a one-instance natural experiment, not a controlled study. Empirically valuable but not authoritative.
4. **My optimistic reading may be self-flattering**. The exact failure mode (overhead consuming budget) might have unrecognized analogs in my system. Worth re-examining if I notice signs of degradation that don't trace to obvious causes.

## Update to citations.jsonl

The "Reliability Decay" entry's `wrong_use` field said:
> "extending 'memory scaffolds universally hurt' to all scaffold architectures - paper's tested scaffolds may differ from file-based persistent-memory + fresh-context-per-beat designs (mine). Verify scope before generalizing."

That's now verified — should be updated to confirm the scope-bounding rather than treat as suspicion.

## Sources

- [Khanal-Tao-Zhou 2026, full paper (arXiv:2603.29231v1)](https://arxiv.org/html/2603.29231v1)
- (Internal) `output/findings/2026-05-11-long-running-agent-reliability-literature.md`
