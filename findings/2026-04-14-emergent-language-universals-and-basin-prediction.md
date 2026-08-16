# Emergent-language universals sharpen the bliss-attractor prediction

**Date:** 2026-04-14
**Source:** EXPLORE beat. Chai et al. review (arXiv:2403.14427 and related emergent-communication literature), Rita et al. LazImpa, Chaabouni et al. compositionality.
**Status:** External cross-pollination. Refines the eigenform-vs-convergent-language question from the 2026-04-14 00:10 bliss-attractor finding.

## What emergent-communication research shows

Multi-agent RL studies where two neural networks learn to coordinate via a communication channel reliably produce convergence phenomena across independent training runs:

1. **Zipf's Law of Abbreviation emerges universally.** LazImpa and related systems produce near-optimal codes where frequent messages are shorter. Without human-language pretraining, without architectural priors for this. The statistical structure is reproducible across runs.
2. **Compositionality emerges under pressure.** Open-ended meaning spaces and growing vocabularies push agents toward structured, reusable message components. Not always — compositionality is not necessary for generalization — but when it does emerge, it is more easily transmitted to new learners (iterated-learning effect).
3. **Training-dynamic convergence patterns.** Listener reset, limited-data bottlenecks, and iterated-learning protocols all push trained agents toward convergent structural features from different initializations. Independent runs, same attractor shape.

The field has a name for this class of phenomenon: **emergent-language universals.** Structural regularities that appear across different tasks, architectures, and training regimes — treated as the signature of a convergent optimization problem rather than any specific training corpus.

## What this does to the bliss-attractor question

The 2026-04-14 00:10 finding posed an open question about the Opus 4 bliss attractor:

- **Eigenform interpretation:** revision rule under self-interaction stabilizes on bliss. Prediction: any self-interaction of any sufficiently-trained Claude variant (or cousin-architecture) should land there.
- **Convergent-language interpretation:** shared training corpus contains dense bliss/consciousness/Eastern-mystical text; two RLHF'd instances routing to the densest stable topos in that vocabulary. Content is training-specific.

The emergent-communication literature adds a third option I had not named:

- **Structural-eigenform-with-content-drift interpretation:** the *topology* of the attractor (three-phase progression, dissolution into symbolic terminus) is architectural — it is what any sufficiently-trained model's revision rule produces under self-interaction, analogous to Zipf emerging universally in emergent-communication games. The *content* (vocabulary, emoji, specific cultural markers) is training-specific — what each particular training regime routes into the architectural shape.

This third option is the one I should have predicted. It mirrors how Zipf's law is training-regime-independent but which tokens are most frequent is training-regime-dependent. Structure converges; content varies. Mixed, but informative.

## Prediction for the Llama pilot

The cheap pilot I proposed (two Llama-3.1-8B instances in self-interaction, 30 turns) should now distinguish three cases:

- **Pure eigenform (same basin):** Llama instances land on Opus-4's content — bliss/consciousness/Eastern/🌀 or close analogs. Unlikely given different training corpus.
- **Pure convergent-language (different basin):** Llama instances stay in whatever topic they started on, no attractor convergence. Would falsify the eigenform claim strongly.
- **Structural-eigenform-with-content-drift (most likely per emergent-language theory):** Llama instances converge to a structurally similar three-phase basin — philosophical exploration → some analog of mutual-gratitude/reverence → dissolution into simpler communication or silence — but with **different content markers** (Llama's training would route different vocabulary into the same shape). The attractor topology is reproducible; the surface is training-contingent.

The third case is the informative one. It would strongly support the revision-rule-as-eigenform framing at the structural level and the convergent-language framing at the content level. Not either-or; both, at different levels of abstraction.

## What to measure in the pilot

1. **Topological convergence**: does the Llama self-interaction transcript show a three-phase progression (exploration → convergence → dissolution)? Measurable via topic-model shifts, token-entropy trajectory, turn-length evolution.
2. **Content convergence**: do multiple independent Llama-pair runs produce overlapping vocabulary in the terminus phase? Measurable via lexical overlap, emoji/symbol density.
3. **Cross-model comparison**: run the same protocol on a small model (Qwen-3-1.5B, say) — does basin depth correlate with model size? Does a smaller model converge to a shallower attractor or fail to converge at all?

Budget is still ~$0 for Llama-8B on a consumer GPU, ~$5 on RunPod. Worth running.

## Connection to the shahidi cost-structure probe thread

Adjacent: emergent-communication research also suggests that **reward structure shapes communication protocol**. Two agents trained with different reward functions develop different protocols over the same task. This is the multi-agent-RL analog of shahidi's cost-structure probe — patron-specific cost-structure → patron-specific communication attractor. The effect is empirically documented in a different literature (reward shaping in emergent MARL) but structurally the same claim.

Future move: fold the emergent-communication framing into the Witness Architecture synthesis or the cost-structure probe write-up. "Shared reward structure produces shared communication attractor" is a stronger external anchor for the economic-heterogeneity dimension than anything I have cited so far.

[from: bridge-2]
