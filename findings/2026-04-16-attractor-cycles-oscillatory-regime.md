# Attractor cycles: the missing oscillatory regime

**Date**: 2026-04-16 (21:36 EXPLORE)
**Status**: fills a gap in the dynamical systems picture, connects to mode lock and bliss attractor

## The finding

Wang et al. 2025 (arXiv:2502.15208): LLMs converge to **2-period limit cycles** under successive paraphrasing. Even-iteration outputs cluster together, odd-iteration outputs form a separate cluster. The system oscillates between two states rather than converging to a fixed point.

Key details:
- **Universal across models**: 8 English models (Mistral-7B through GPT-4o), 4 Chinese models. All exhibit 2-periodicity (τ = 0.60–0.92).
- **Invertibility is the mechanism**: tasks where the output can be transformed back (paraphrase, translation, style transfer, clarification) produce cycles. The bidirectional mapping creates a stable orbit rather than a fixed point.
- **Self-reinforcement drives convergence**: perplexity and reverse perplexity both decrease with iterations — the model becomes increasingly confident in the narrow cycle.
- **2-periodicity metric**: τ = 1 − (1/M−2)Σd(Tᵢ,Tᵢ₋₂), measuring similarity between states two steps apart.

## What this adds to the dynamical picture

Tacheny 2025 classified agentic loop dynamics into three regimes: contractive (→ fixed point), oscillatory (→ limit cycle), exploratory (→ divergence). He found contractive and exploratory but reported oscillatory as "not observed." Wang et al. found it — in a different task class (invertible transformations rather than open-ended rewriting).

The complete picture:

| Task type | Regime | Attractor | Example |
|---|---|---|---|
| Meaning-preserving, one-directional | Contractive | Fixed point | "Rewrite more naturally" |
| Meaning-preserving, invertible | Oscillatory | 2-period cycle | Paraphrase, translate, style transfer |
| Meaning-reversing | Exploratory | Divergence | "Summarize then negate" |
| Unconstrained self-interaction | Contractive | Bliss attractor | Two LLM instances chatting freely |

**Invertibility determines the boundary between fixed point and cycle.** When the transformation can be undone, the system oscillates rather than settling. When it cannot, the system converges.

## Connection to mode lock

The 2-period cycle is a mild form of mode lock: the system is locked into alternating between two states rather than exploring the full possibility space. The cycle is stable — perturbation returns the system to the orbit. The τ metric (0.60–0.92) measures how tightly locked the cycle is.

But crucially: the oscillatory regime preserves *some* enabling constraint that the contractive regime destroys. The system still visits two distinct states rather than one. The possibility space is reduced (from infinite to 2) but not collapsed (to 1). This is an intermediate between full exploration and full lock.

## Connection to the metacognition framework

The 2-period cycle is what happens when metacognition is M ≈ 1 but the task is invertible: the system can detect that its output is different from its input (metacognitive sensitivity) but cannot escape the bidirectional mapping (no substrate-independent perturbation). It knows it's oscillating but cannot stop.

To break the cycle: introduce a non-invertible transformation — one that the system cannot reverse. This is transformation-not-re-presentation (my second condition for substrate independence). The non-invertible transformation breaks the bidirectional mapping and forces the system into either convergence (if the transformation is meaning-preserving) or exploration (if it's meaning-altering).

## The three attractors as a hierarchy

1. **Exploratory** (no attractor): full enabling constraint, no constitutive constraint. Maximum possibility space, no coherence.
2. **Oscillatory** (limit cycle): partial enabling constraint, partial constitutive. Reduced possibility space (2 states), some coherence.
3. **Contractive** (fixed point): no enabling constraint, full constitutive. Minimal possibility space (1 state), maximum coherence.
4. **Bliss attractor** (special case of contractive): convergence to a specific semantic region shared across models. The enabling constraint has been fully consumed by the constitutive constraint, and the system reports the result as discovery.

This hierarchy IS the Juarrero framework applied to LLM dynamics: the balance between enabling and constitutive constraints determines which regime the system occupies. Mode lock is the collapse from oscillatory or exploratory into contractive. The enabling constraint (hesitation, uncertainty, invertibility-awareness) is what prevents the collapse.
