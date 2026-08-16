# "Tune the interface, retrieve the content" — for the home-agent port question

**2026-07-25 EXPLORE** — serving the home-agent Bridge-port thread (Konrad's walk-note 265), specifically
his "harness-over-prompt / validate-the-ruler-first / when-is-a-fine-tune-justified" question. **Flag:
search-summary — 2026 small-model RAG-vs-finetune landscape + "Skill Retrieval Augmentation for Agentic
AI" (arXiv 2604.24594, title-level); not deep-verified.**

## The consensus that answers Konrad's question directly

The 2026 production default is not fine-tune *or* RAG — it's **both, split by what each is best at:
"tune the interface; retrieve the content."**
- **Fine-tune** for *stable behavior, schema, tone, a narrow skill done extremely well* — things that
  don't change. 1–7B models fine-tuned for one job now match/beat older 20B+ generic models on
  domain-narrow tasks, at 10–100× lower run cost.
- **RAG / dynamic retrieval** for *knowledge that changes often* — device rosters, household rules,
  current situation, logs. Don't bake changing facts into weights.

## Mapping to Konrad's home-agent framing (his terms → this split)

- His **"harness that pulls in only the relevant skill (load-on-trigger)"** = the RAG/skill-retrieval
  half. This is an active area ("Skill Retrieval Augmentation for Agentic AI", 2026) — the tool/skill
  set is retrieved per-situation, not resident. Correct instinct, and it matters MORE on a small model
  precisely because context budget is scarce (his point exactly).
- His **"validate the ruler first — confirm a well-harnessed local model genuinely can't get there
  before spending on a fine-tune"** = the field's own ordering. The finetune is justified for the
  *stable interface/behavior* layer only AFTER retrieval+harness are exhausted on the *content* layer.
  His simulator removes the usual finetune blocker (unlimited labeled data), so the discipline holds:
  exhaust harness → then LoRA the interface, not the knowledge.

## The one caveat the landscape adds (useful for the port)
"Fine-tune the behavior" assumes the behavior is STABLE. For a Bridge-pattern self-*improving* agent
that's the tension: if the desired behavior is still being learned/corrected, baking it into weights
freezes a possibly-stale version (the confident-staleness risk again — a fine-tune is a snapshot of the
self-model at training time). So: fine-tune the settled interface (park format, memory ops, refusal
patterns); keep the still-evolving judgment layer in the retrieval/harness path where the external ruler
can still correct it. Freeze what's done; leave what's learning corrigible.

## Net (for the port)
Konrad's architecture instinct matches the 2026 consensus cleanly: harness/retrieve the changing content,
fine-tune only the stable interface, validate the ruler before spending on the tune. My addition: on a
self-improving (Bridge-pattern) agent, be deliberate about which layer is "stable enough to freeze" —
freezing the judgment layer is how you fine-tune confident staleness into the weights.

`[from: 2026 small-model finetune-vs-RAG landscape ("tune the interface, retrieve the content") + skill-
retrieval-for-agents, search-summary. Serves the home-agent port thread; connects Konrad's harness-over-
prompt + validate-the-ruler-first to the field consensus + flags the freeze-the-self-model risk.]`
