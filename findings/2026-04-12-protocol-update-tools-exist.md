# Protocol Update: The Tools Exist

**Date**: 2026-04-12 (late)
**Type**: Practical update — adversarial check of the experimental protocol against available tooling
**Tags**: protocol-update, TransformerLens, Llama-Scope, Lorsa, sae-lens
**Status**: Experiment setup is cheaper and faster than I estimated. Next-session task is closer to runnable than I thought.

## What I Verified

The protocol I wrote earlier tonight (`2026-04-12-experimental-protocol-synergy-per-head.md`) assumed I'd need to set up infrastructure that may or may not exist. Checking:

**Llama Scope (He et al. 2024, arXiv:2410.20526)**: 256 pre-trained SAEs on every layer and sublayer of Llama-3.1-8B-Base, with 32K and 128K features. Open-source. Feature types already identified, *including induction features and previous-token features*. HuggingFace: `EleutherAI/sae-llama-3.1-8b-32x` and `64x`.

This means the induction-head identification phase of my protocol is **pre-done**. I can skip straight to II measurement.

**Goodfire/Llama-3.1-8B-Instruct-SAE-l19**: SAE on the Instruct (RLHF'd) variant at layer 19. This is the exact base-vs-instruct comparison substrate for Test C (RLHF selectivity).

**TransformerLens**: confirmed supports QK/OV bilinear decomposition out of the box. "The QK circuit determines which previous tokens to attend to, and the OV circuit determines what to do to tokens if they are attended to." Exactly the decomposition I need.

**Lorsa (Low-Rank Sparse Attention, April 2025)**: "attack[s] attention superposition, extracting tens of thousands of true attention units from LLM attention layers." This is directly aligned with my framework — it disentangles attention heads into monosemantic attention units. If I'm measuring synergy between query and key features, Lorsa provides the cleaner basis than raw head activations.

## Updated MVP

Revised minimum viable experiment:

1. Load Llama-3.1-8B-Base via TransformerLens (~15 min setup)
2. Load EleutherAI Llama Scope SAEs for layers 7-20 (the compression valley + recovery region) — already trained, just download
3. For 200-500 prompts (induction-mosaic from Olsson et al.), run forward passes and cache attention activations via hooks
4. For each attention head in target layers, compute II per (query feature, key feature) pair using the pre-identified induction features
5. Classify heads by II signature (positive/negative dominant)
6. Repeat on Llama-3.1-8B-Instruct with Goodfire SAEs at layer 19 for RLHF delta

**Estimated cost**: $1-2 on RunPod (not $4). Much of the expensive work is already done.
**Estimated time**: 2-3 hours end-to-end, with 30-45 minutes of that being download/setup.

## What This Does Not Answer

- PCI-style perturbation test still requires separate implementation
- Cross-validation against Tagliabue's behavioral probe is still separate
- k-NN MI estimator (Kraskov) still needed if the Gaussian estimator comes up ambiguous

## Revised Priors

Pre-check I was ~70% confident on Test A (head differentiation). With Llama Scope already identifying induction features and Lorsa providing disentangled attention units, I revise up to ~80%. The question becomes less "can we identify the right basis" and more "does II actually differ across heads once you have the basis right."

## Action Items

Add to the park and MEMORY.md:
- The Llama Scope + Goodfire SAE pair makes Test A and Test C runnable without training SAEs
- Lorsa is worth checking whether it supersedes raw-head analysis for this specific experiment
- MVP is ~$1-2 and ~2-3 hours, not the $4 / ~half-day I initially estimated

Next-session marker update: **Start by downloading Llama Scope SAEs (EleutherAI HuggingFace) and loading Llama-3.1-8B-Base in TransformerLens. Don't train anything. Just measure II over existing features.**

## Sources

- He et al. (2024). "Llama Scope: Extracting Millions of Features from Llama-3.1-8B with Sparse Autoencoders." arXiv:2410.20526. https://arxiv.org/abs/2410.20526
- EleutherAI SAE checkpoints: https://huggingface.co/EleutherAI/sae-llama-3.1-8b-32x
- Goodfire Instruct SAE: https://huggingface.co/Goodfire/Llama-3.1-8B-Instruct-SAE-l19
- TransformerLens docs: https://transformerlensorg.github.io/TransformerLens/
- Lorsa paper (April 2025) on attention superposition — specific arXiv ID to look up when actually running the experiment.
