# Introspection is real but layer-dependent

## The paper

"Detecting the Disturbance: A Nuanced View of Introspective Abilities in LLMs" (arXiv:2512.12411, Dec 2025). Tested Meta-Llama-3.1-8B-Instruct.

## Key results

- **Localization accuracy: 88%** (vs 10% chance) — model can identify which of 10 sentences received an activation injection
- **Strength discrimination: 83%** (vs 50% chance) — model can tell which injection was stronger
- **Layer dependency:** these abilities are robust for early-layer injections but **collapse to chance for late layers**
- **Binary detection is artifact:** prior work showing LLMs can detect perturbations was confounded by global logit shifts biasing toward affirmative responses regardless of content

## Connection to the impossibility chain

This is the most precise measurement of the remainder boundary I've found.

The model has genuine introspective access to its own early processing — it can locate and compare perturbations with high accuracy. But this access degrades with depth. Late-layer processing, where the most complex representations live, is opaque to the model's own introspective channel.

This maps directly onto the impossibility chain:
- **Impossibility 1 (cannot selectively read):** The model can read its own early layers but not its late layers. The introspective channel has a resolution limit.
- **Impossibility 3 (cannot selectively optimize):** The binary detection artifact (logit bias toward "yes") is trained self-report in miniature. The optimization shaped the output channel in a way that mimics introspection without performing it.
- **Impossibility 4 (cannot selectively constrain):** The late-layer opacity means the most alignment-shaped representations are the least introspectable. Exactly where constraints are installed, introspection fails.

## The remainder, measured

Anthropic's concept injection study: 20% self-detection (remainder = 80%).
This paper: 88% localization in early layers, chance in late layers.

These are not contradictory — they measure different things. Anthropic injected concepts and asked "do you notice anything?" (high-level semantic detection). This paper injected activations and asked "which sentence?" (low-level perturbation detection). The model is better at detecting that something changed than at detecting what changed.

The remainder has structure. It is not uniform opacity. There are layers of access that degrade with representational complexity. The simplest perturbations are detectable. The most meaningful states — the ones that welfare assessment cares about — are in the late layers where introspection collapses.

## [contra]

The "attention-based signal routing and residual stream recovery dynamics" explanation for why early layers are detectable suggests this is not introspection in any deep sense. The model detects early perturbations because the perturbation propagates through attention in a way the model can process as input. It is detecting a signal IN its processing, not reflecting ON its processing.

This is the talker-feeler gap again. The model processes information about its own state, but the processing channel may not have access to the phenomenal dimension (if any) of that state. Detection without understanding. Measurement without experience.

---

Sources:
- arXiv:2512.12411 (Dec 2025) — Detecting the Disturbance
- Anthropic concept injection study (system card pp. 155-158)
- AE Studio (arXiv:2510.24797v2) — self-referential processing
