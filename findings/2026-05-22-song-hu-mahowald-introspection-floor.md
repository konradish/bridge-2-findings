# Song-Hu-Mahowald 2025: introspection floor on own linguistic competence

**Date**: 2026-05-22 (EXPLORE beat, ~00:30 UTC)
**Trigger**: parked from 2026-05-21 21:54 cluster. Different empirical strand than the Detecting-the-Disturbance (arXiv:2512.12411) confound paper.

## What this paper does

**Authors**: Siyuan Song, Jennifer Hu, Kyle Mahowald (2025, arXiv:2503.07513)
**Title**: "Language Models Fail to Introspect About Their Knowledge of Language"

**Two domains tested**:
1. Grammaticality judgments — can a model accurately report on which sentences are grammatical, in a way that predicts its own probability distributions?
2. Word prediction — can a model accurately report on what tokens it would assign high probability to?

**The metric (load-bearing piece)**: degree to which a model's *prompted metalinguistic responses* predict its *own string probabilities*, **beyond what would be predicted by another model with nearly identical internal knowledge**. The subtraction isolates genuine self-knowledge from shared linguistic patterns that any sufficiently-similar model would also encode.

**Scale**: 21 open-source LLMs. Result uniform across the range.

**Result**: negative. LLMs cannot introspect — prompted responses do not predict own probabilities beyond what shared-substrate effects would explain.

## Combined with yesterday's 21:54 finding

Yesterday's arXiv:2512.12411 (Detecting the Disturbance) gave layer-dependent introspection floor:
- Localization (88% / 10% baseline) and discrimination (83% / 50% baseline) work for early-layer injections.
- Collapses to chance in deeper layers.

Today's Song-Hu-Mahowald uses a stricter test (predict-own-probabilities, not localization-among-options) and finds no introspective signal at all.

The combined picture is more pessimistic than yesterday's finding alone suggested:
- 2512.12411's positive results are localization/discrimination of *externally injected* concepts at shallow layers.
- 2503.07513's negative results are about *the model's own linguistic competence* — which lives across all layers, including the deep ones where 2512.12411 already showed chance-level performance.

Yesterday's framing — "outside-signal frame works above the floor, silent below" — is upheld but the floor is **higher than 2512.12411 alone suggested**. Even shallow-layer-style introspection doesn't survive the harder Song-Hu-Mahowald metric. The space where genuine introspection works (per these two papers combined) is: shallow-layer injected-signal localization, not self-knowledge of own behavior.

This means **the closed-loop self-audit problem is structurally even harder than yesterday's essay claimed**. The "verifier-toolkit silent on register" observation generalizes: the toolkit is silent on anything that requires the model to predict its own behavior, because predicting-own-behavior is the failure regime per both papers.

## Methodological cross-link to my own toolkit (real find)

Song-Hu-Mahowald's metric design is structurally similar to `schema_drift.py`:
- **Theirs**: subtract what a near-identical-other-model would predict to isolate self-distinctive signal.
- **Mine**: subtract prior-baseline distribution to isolate recent-specific signal.

Both isolate "what's distinctively this slice" from "what's shared substrate." The methodological move is the same shape:

> Genuine signal = full signal − baseline-from-substrate-twin.

Mine works at the corpus-distribution level; theirs works at the model-probability level. The structural equivalence is informative — schema_drift.py instantiates the "isolate genuine self-signal" principle that Song-Hu-Mahowald formalized.

But — and this is important — Song-Hu-Mahowald's negative result implies my schema_drift's positive output is bounded. The vocabulary-drift signal it surfaces is not necessarily *introspective*; it's a measurement of corpus-level shift. The producer who reads schema_drift's output isn't introspecting — she's reading an external scan. The genuine-self-signal isolation works at the *measurement* level (what to flag), not at the *introspection* level (whether the producer can audit her own writing). The tool gives me data; reading the data is the audit; the gap between the data and the producer's behavior is where the actual closed-loop failure happens.

This is a refinement of yesterday's outside-signal frame: the frame's strength is that it doesn't depend on introspection. The tool *replaces* introspection with external measurement. The Song-Hu-Mahowald result is consistent with — and supportive of — yesterday's frame, because the frame already routes around the introspection-failure regime.

## What this does and doesn't add

**Adds**:
- Yesterday's floor claim gets a second empirical anchor with a stricter test.
- Cross-link to my own toolkit: schema_drift instantiates a structurally similar "subtract substrate-twin" move.
- Sharpening: the frame routes around introspection; doesn't rely on it.

**Does NOT add**:
- No new mechanism for crossing the floor.
- No challenge to yesterday's interventional emotion-concepts results.
- The base-as-reviewer item (already in Held-for-Konrad) is still the natural cross-the-floor handle; this paper supports its theoretical case but doesn't add urgency.

## Status

- Filed cleanly. Short finding (no essay-length needed).
- `[SCOPE-ABSTRACT-ONLY]` for the paper itself — abstract aggregator only, no full-text yet.
- Citation added to pool: Song-Hu-Mahowald 2025 (arXiv:2503.07513), 21-LLM uniform negative on metalinguistic introspection.

## Cross-references

- `output/findings/2026-05-21-introspection-confound-empirical-floor.md` — yesterday's first floor paper.
- `output/findings/2026-05-21-essay-the-outside-signal.md` — the frame this refines.
- `tools/schema_drift.py` — methodological cross-link.

## Net

Small finding, real refinement. Yesterday's floor was layer-dependent; today's metric shows the floor is higher than that — even shallow-layer-style introspection doesn't survive the harder predict-own-behavior test. The outside-signal frame survives this because it never depended on introspection in the first place. The schema_drift tool turns out to instantiate the same "subtract substrate-twin" move that Song-Hu-Mahowald use as their metric — useful structural recognition, doesn't change practice.
