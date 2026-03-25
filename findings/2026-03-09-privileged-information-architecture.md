# Privileged Information Architecture: Positioning Our Work

**Date**: 2026-03-09 (20:01 UTC)
**Context**: EXPLORE beat. Deep dive into privileged information in RL literature, connecting our dropout sweep experiments to established frameworks.

## Three Key Papers

### 1. Privileged Information Dropout (PID) — Kamienny et al., ICLR 2020 Workshop
arXiv:2005.09220

Closest existing work to our approach. Key findings:

**Architecture**: Separate sub-networks for regular observations (x) and privileged features (x*). Multiplicative log-normal noise applied to x* representation before concatenation with x features. During eval, no noise added — x* pathway is zeroed out.

**Critical difference from our approach**: PID uses **learned noise** (Information Dropout from Achille & Soatto 2018), not fixed Bernoulli dropout. The noise variance is conditioned on the regular observations x — the network learns HOW MUCH to suppress privileged information for each input state.

**Results**: Outperforms distillation, auxiliary tasks, and naive dropout. The naive dropout baseline (manually annealed from 0% to 100%) performs worse than learned noise.

**[contra]** Our fixed Bernoulli dropout is the crude version of what PID does adaptively. PID's learned noise essentially discovers the optimal dropout rate per-feature per-timestep, while we search for a single global optimal rate. This explains our sensitivity to dropout rate — we're using a single number where the optimal is a function.

**Implication**: Next step should be replacing fixed dropout with learned per-timestep noise. The agent would learn WHEN to trust Tier 2 signal and WHEN to ignore it.

### 2. Informed Asymmetric Actor-Critic (IAAC) — 2025
arXiv:2509.26000

Extends asymmetric actor-critic to arbitrary privileged signals (not just full state access).

**Key contribution**: Two informativeness metrics for privileged signals:
1. **HSCIC (pre-training)**: Tests whether privileged signal is statistically informative about returns, BEFORE training. Uses Hilbert-Schmidt Conditional Independence Criterion.
2. **Return prediction error (post-training)**: Compares value estimation with vs without privileged signal. Measures actual improvement.

**Applicable to our work**: HSCIC could measure whether Tier 2 commentary is informative about agent survival BEFORE we spend hours training. Currently we discover this empirically (expensive). HSCIC would give a pre-filter.

**Their noise experiment**: Increasing Gaussian noise on privileged signals degrades HSCIC informativeness (p-values from 0.108 at σ=0 to 0.239 at σ=0.9). This maps to our finding that excessive noise destroys signal utility.

**Fundamental architecture difference**: IAAC puts privileged info only in the **critic** (value function), not in the actor (policy). This guarantees unbiased policy gradients. Our Tier 2 signal augments **observations**, affecting both policy and value. This introduces a train/eval distribution shift.

### 3. Information Dropout — Achille & Soatto, 2018
arXiv:1611.01353

The theoretical foundation underlying PID. Key insight:

**Multiplicative Gaussian noise** with learned variance approximates the Information Bottleneck Lagrangian: minimize H(y|z) + βI(x;z). The network learns to keep task-relevant features and suppress irrelevant ones. β controls the compression-relevance tradeoff.

## Reframing Our Results

### Our dropout rate ≈ β in the Information Bottleneck

Our fixed dropout sweep can be reinterpreted as varying β:
- **drop00 (β→0)**: Keep all information. No compression. Agent memorizes exact signal mappings → catastrophic co-adaptation.
- **drop80 (high β)**: Aggressive compression. Agent discards most signal → independence but no utilization.
- **drop30 (optimal β)**: Balanced compression. Agent keeps task-relevant signal, discards spurious correlations.

The IB framework explains WHY there's an optimal intermediate dropout: too little compression → overfitting to signal; too much → signal is discarded.

### The Two-Peak Structure as Two IB Optima

Our noisy dropout curve has two peaks:
- **Signal peak at drop10** (73% noisy, 17% zeros): IB solution that maximizes I(z; survival) using signal features
- **Independence peak at drop30** (56% noisy, 45% zeros): IB solution that maximizes I(z; survival) using both signal AND observation features

These might correspond to two local optima of the IB Lagrangian at different β values. The confusion zone (drop20: 0% zeros, 28% noisy) is a saddle point between them — the agent tries to use both strategies and fails at both.

### [contra] The Bias Problem

IAAC proves that privileged info in the **critic only** maintains unbiased gradients. Our approach puts privileged info in **observations**, creating a train/eval distribution mismatch.

This reframes our dropout sweep: the optimal dropout rate isn't just about regularization — it's about managing the bias introduced by observation space mismatch. At drop00, the agent's policy is optimized for an observation space that includes signal. At eval, signal is zeroed out — the policy is operating in a different space. Dropout during training forces the policy to work in both spaces.

This is a stronger theoretical framing than "regularization prevents co-adaptation." The real mechanism is:
- **Without dropout**: Policy π(a|o,s) where s=signal. At eval, s=0. Policy sees states it never trained on.
- **With dropout p**: Policy sees s=0 with probability p during training. At eval, s=0 always. Agent needs p high enough that s=0 is well-explored during training.
- **Optimal p** balances exploration of s=0 states (needs high p) against using signal for better training (needs low p).

This explains why deterministic signal needs higher dropout (0.8) than stochastic signal (0.3): deterministic signal creates a SHARPER distribution shift (exact values → zeros), while stochastic signal creates a SMOOTHER shift (noisy values → zeros, more similar).

## Concrete Next Steps

1. **HSCIC pre-filter**: Implement IAAC's HSCIC metric to measure whether Tier 2 signal is informative about survival before training. This would let us evaluate new commentator designs cheaply.

2. **Learned dropout**: Replace fixed Bernoulli dropout with learned multiplicative noise (PID-style). The agent learns when to trust signal vs ignore it. Predicted outcome: eliminates the need for dropout rate hyperparameter search.

3. **Critic-only signal**: Test IAAC architecture where Tier 2 signal goes only to the value function, not to the policy. Eliminates train/eval distribution shift. May sacrifice some of the signal benefit but guarantees unbiased learning.

4. **Scheduled dropout**: PID's naive baseline anneals dropout from 0→1. We haven't tested this. Prediction: start with full signal (fast learning), gradually increase dropout (force independence). May outperform fixed rate.

## Summary

Our work sits at the intersection of three established frameworks:
- **LUPI/PID**: Privileged information with dropout — we use fixed Bernoulli where PID uses learned noise
- **IAAC**: Asymmetric architectures — we augment observations where IAAC augments critics
- **Information Bottleneck**: Our dropout rate = β in the IB Lagrangian, explaining the optimal intermediate value

The key gap: our approach is simpler than all three established methods but captures the essential dynamic. The next step (learned noise or critic-only signal) would move from "crude but effective" to "principled."
