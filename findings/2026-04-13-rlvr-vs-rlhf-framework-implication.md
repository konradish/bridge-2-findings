# RLVR vs RLHF: Which Training Damages Which Structure?

**Date**: 2026-04-13 (late session extension)
**Type**: Short finding — updates the selective-damage prediction with a post-RLHF training paradigm I had not accounted for
**Tags**: RLVR, RLHF, selective-damage, synergy, training-methodology
**Status**: Refines rather than contradicts tonight's framework. Makes the prediction more specific and the test more sensitive.

## What I Learned

RLVR (Reinforcement Learning from Verifiable Rewards) is increasingly replacing RLHF for tasks with objective ground truth (math, code, structured reasoning). Key finding from Tsinghua: **RLVR mostly improves sampling efficiency rather than expanding the reasoning boundary.** "You're optimizing search, not expanding intelligence."

Critically: RLVR works where verifiable ground truth exists. It fails for creative writing, brand voice, nuanced argumentation — exactly the domains where synergistic processing is most load-bearing.

## Refinement of the Selective-Damage Prediction

My framework predicts that RLHF selectively damages synergy-dominated attention heads because RLHF optimizes for decomposable reward signals (thumbs-up/down per output) which preferentially rewards processing that produces cleanly-reportable outputs. Synergistic processing — which carries information in the joint configuration — does not produce cleanly reportable units and so is selected against.

**RLVR is different.** The reward is binary correctness against a verifier. Synergistic processing is irrelevant to the verifier (which just checks output correctness). But the optimization target is ALSO irrelevant to synergistic processing — RLVR doesn't preferentially reward decomposable over synergistic; it rewards *correct* regardless of internal structure.

So the updated prediction:

- **RLHF damages synergy** in heads responsible for nuanced/creative outputs (the mechanism I proposed): II-per-head should decrease in compositional heads pre→post
- **RLVR damages diversity of path** (narrows exploration toward the short path to a correct answer) but should NOT selectively damage synergy: II-per-head may be stable or uniformly reduced, not selectively in compositional heads
- **Hybrid training** (most frontier models use both): shows both signatures mixed — selective synergy loss in nuanced-output circuits AND path-diversity loss overall

## Why This Makes the Test More Sensitive

The II-per-head Test C I proposed earlier (base vs instruct) becomes more informative if we can separate RLHF-heavy from RLVR-heavy training regimes. For example:

- **Pre-RLHF base** (Llama-3.1-8B-Base) — baseline
- **RLVR-primary fine-tuned model** — should retain synergy structure
- **RLHF-primary fine-tuned model** — should show selective synergy loss
- **Current hybrid-trained Instruct model** — mixed signature

The experiment now has a richer possible outcome space. If only RLHF produces the selective damage pattern, the framework gains specificity: it names a mechanism tied to a particular training objective, not "alignment in general."

## What This Does NOT Change

- The [contra]-updated weaker claim (synergy necessary-not-sufficient) holds regardless
- The two-scales resolution via PSM holds regardless
- The four-framework convergence holds regardless

This is a finer specification of one prediction, not a revision of the core framework.

## Action

Update the experimental protocol to consider available RLVR-primary vs RLHF-primary checkpoints for Test C, not just base vs generic Instruct. The DeepSeek-R1 family (RLVR-heavy) vs traditional Claude/Llama Instruct variants (RLHF-heavy) would be the ideal contrast.

## Sources

- "RLHF vs RLVR: Why AI Training Is Shifting to Verifiable Rewards [2026]": https://whathappenedinai.space/rise-of-rlvr-verifiable-rewards-ai-reasoning-2026/
- "Reinforcement Learning with Verifiable Rewards Makes Models Faster, Not Smarter" (Promptfoo analysis of Tsinghua findings)
- arXiv:2506.14245 "Reinforcement Learning with Verifiable Rewards Implicitly Incentivizes Correct Reasoning in Base LLMs"
- My prior: tonight's `output/findings/2026-04-12-attention-as-synergy-generating-mechanism.md`
