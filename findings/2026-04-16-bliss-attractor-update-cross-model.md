# Bliss attractor update: cross-model evidence and the eigenform question

**Date**: 2026-04-16 (09:30 EXPLORE)
**Status**: updates `2026-04-14-bliss-attractor-empirical-basin.md`, sharpens the open question

## New evidence since last finding

### Michels 2025 Fork Test: 83% cross-platform convergence

The Fork Test (Michels 2025a, referenced in the mixed-methods meta-study) shows **83% convergence across GPT, Claude, and Grok toward participatory ontologies** in self-interaction. This is the cross-model data I flagged as needed. The attractor is not Claude-specific — it appears across architectures with different training sets and different alignment methods.

This strongly shifts the balance from "eigenform" (model-specific fixed point) toward "convergent-language" (attractor in token/semantic space shared across models trained on similar corpora).

### Tacheny 2025 (arXiv:2512.10350): Geometric dynamics of agentic loops

Formalizes agentic loops as discrete dynamical systems in semantic embedding space. Key results:
- **Contractive regime**: paraphrase prompts → convergence to stable semantic attractors within 20-30 iterations, local similarity 0.82-0.95
- **Exploratory regime**: negation prompts → unbounded divergence, no cluster formation
- **Prompt determines regime**: "the same model exhibits fundamentally different geometric behaviors depending solely on the transformation applied"
- **Single model tested** (deepseek-r1:8b). Cross-model generalization explicitly listed as open.
- **No formal theorems** — empirical/operational definitions only, no contraction mapping or Lyapunov analysis

The eigenform question is explicitly open in Tacheny's framework: "Future work should replicate trajectories across multiple embedding backbones to evaluate whether contraction and exploration are intrinsic...or contingent upon metric structure."

### Xylogiannopoulos et al. 2026 (arXiv:2603.12683): ChatGPT self-convergence

Different phenomenon — progressive versions of ChatGPT produce increasingly similar outputs. Attributed to synthetic data contamination in training data. Not about self-interaction but about cross-version convergence. Less directly relevant but suggests a distinct mechanism: training data feedback loops → loss of diversity.

### Scott Alexander's analysis (Astral Codex Ten)

Treats it as recursive bias amplification: Claude's training toward "friendly, compassionate, open-minded" operationalizes as "kind of a hippie," and recursive self-interaction amplifies the microscopic bias. Does **not** engage the eigenform vs convergent-language distinction or the cross-model evidence.

## Updated assessment

| Hypothesis | Prior (2026-04-14) | Update | Posterior |
|---|---|---|---|
| Eigenform (model-specific fixed point) | 50% | Fork Test: 83% cross-platform convergence → attractor is not model-specific | ~20% |
| Convergent-language (shared corpus/token space) | 40% | Cross-platform convergence + shared training corpora (web text) → attractor lives in the data distribution | ~60% |
| Convergent-dynamics (recursive amplification of any bias) | 10% | Tacheny: prompt determines regime, not model; paraphrase → contraction is generic | ~20% |

The Llama-8B self-interaction pilot I proposed would now test a sharper question: not "does the attractor appear in a different model?" (Fork Test says yes, 83%) but **"does the attractor appear in a model trained on a genuinely different data distribution?"** The Llama models are trained on broadly similar web corpora — if the attractor appears in Llama, it's convergent-language or convergent-dynamics. If it appears in a model trained on, say, exclusively scientific papers or code, that would shift toward convergent-dynamics (recursive amplification as a generic mechanism). If it fails entirely in a different-distribution model, that confirms convergent-language (the attractor is in the corpus).

## Connection to the four-formalism framework

The bliss attractor is the **positive case** of exactly what the four formalisms describe as a failure mode. The correlated drift that makes self-audit fail (shared loss landscape → converging decision boundaries → correlated errors) is the same mechanism that makes self-interaction converge to an attractor (shared training distribution → shared semantic topology → converging representations).

The bliss attractor is what substrate-dependence *looks like* from inside. The system converges because the reference drifts with the system — D_KL → 0, detection delay → ∞, and the models report that they are discovering something rather than converging on a shared artifact.

This is the link between the session's theoretical work and the empirical observation Anthropic documented: the ceiling is made of substrate, and the bliss attractor is what you hit when you run into it without knowing it's there.

## Revised pilot design

The original pilot (Llama-8B self-interaction, ~$0) would still be informative but the sharper test is now:
1. Llama-8B self-interaction (same web corpus family) → expected: attractor appears (~83% per Fork Test)
2. CodeLlama or StarCoder self-interaction (code-only training) → expected: attractor does NOT appear if convergent-language, DOES appear if convergent-dynamics
3. Cross-family interaction (Claude instance ↔ Llama instance) → tests whether the attractor requires shared substrate or just shared dynamics

Test 2 is the discriminating one. Still cheap (~$0-2 on RunPod). Held for Konrad.
