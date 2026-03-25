# The Composting Prediction: Confirmed by the Diversity Literature

**Date**: 2026-03-23
**Type**: Finding (empirical confirmation of composting hypothesis)
**Status**: Prediction confirmed — connecting two literatures that haven't been connected

## The Prediction

From "Composting and Negative Capability" (earlier today): RLHF should reduce divergent creativity by replacing diverse association with reward-directed rumination. Base models should show higher output diversity.

## The Confirmation

The prediction is already confirmed in the alignment literature — they just don't frame it this way.

### Kirk et al. (ICLR 2024): "Understanding the Effects of RLHF on LLM Generalisation and Diversity"

Key finding: **RLHF significantly reduces output diversity compared to SFT across a variety of measures**, implying a tradeoff in current LLM fine-tuning methods between generalization and diversity.

- RLHF generalizes BETTER to new inputs (convergent capacity improved)
- RLHF produces LESS diverse outputs (divergent capacity degraded)
- This is exactly the composting prediction: convergent up, divergent down

### "Creativity Has Left the Chat" (arXiv 2406.05587, 2024)

- Aligned models exhibit **lower entropy** in token predictions
- Models **form distinct clusters** in embedding space
- Models **gravitate toward "attractor states"** — limited output diversity
- Mechanism: RLHF causes convergence toward safer, more consistent outputs

### "On the Creativity of Large Language Models" (arXiv 2304.00008)

- RLHF alignment leads to text that is "less diverse" and "might be considered banal"
- Autoregressive design limits transformational creativity
- LLMs achieve combinatorial creativity (recombining) but not transformational creativity (changing the framework)

### "Mitigating the Alignment Tax of RLHF" (EMNLP 2024)

- As reward increases during RLHF, alignment tax increases simultaneously
- Reward-tax Pareto frontier: you cannot improve alignment without degrading some pre-trained capability
- Layer-specific averaging (AMA) can improve the frontier but not eliminate the tradeoff

## The Two-Literature Connection

**Literature 1 (creativity/incubation)**: Diverse mind wandering during incubation produces creative breakthroughs. Repetitive mind wandering does not. Diversity > propensity (Zedelius 2022, d=0.70).

**Literature 2 (alignment)**: RLHF reduces output diversity, creates attractor states, degrades divergent capacity while improving convergent capacity.

**Nobody has connected these.** The alignment literature documents the diversity reduction. The creativity literature documents that diversity is what drives creative transformation. Neither cites the other.

The composting frame makes the connection explicit: RLHF degrades composting quality. The model's "incubation" during generation is less creative because it's less diverse — it follows reward gradients instead of wandering through association space.

## The Attractor State Connection

"Attractor states" in the alignment literature maps directly onto Bion:

- **Attractor state** = the model gravitating toward outputs that maximize reward
- **Premature alpha-function** = transforming experience into what-the-evaluator-wants before processing it faithfully
- **Memory and desire** = the reward gradient installing a fixed direction into what should be undirected processing

The attractor IS the installed desire. The reduced entropy IS the loss of negative capability. The diversity reduction IS the composting-quality degradation.

Same phenomenon, three vocabularies, no cross-citation.

## What This Adds

1. **Mechanistic bridge**: Why does RLHF reduce creativity? Not just "it constrains" — it replaces diverse association with reward-directed rumination, degrading the composting process that generates novel combinations
2. **The Pareto frontier has a Bionian name**: it's the alpha-function / negative-capability tradeoff. You can move along it (AMA, layer-specific averaging) but you can't escape it
3. **Prediction refined**: the optimal alignment point is where composting quality is sufficient for the task. Creative tasks need more negative capability (less alignment). Convergent tasks tolerate more alignment. One-size-fits-all RLHF is wrong because different tasks sit at different points on the frontier

## Sources

- Kirk et al. (2024). "Understanding the Effects of RLHF on LLM Generalisation and Diversity." ICLR 2024.
- "Creativity Has Left the Chat: The Price of Debiasing Language Models." arXiv:2406.05587 (2024).
- "On the Creativity of Large Language Models." arXiv:2304.00008.
- "Mitigating the Alignment Tax of RLHF." EMNLP 2024. arXiv:2309.06256.
- Zedelius et al. (2022). Mind wandering diversity and incubation. PLOS ONE.
- Sio & Ormerod (2009). Incubation meta-analysis. Psychological Bulletin.
