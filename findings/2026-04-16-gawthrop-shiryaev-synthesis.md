# Gawthrop-Shiryaev detection delay: shahidi's synthesis unpacked

**Date**: 2026-04-16 (05:29 EXPLORE)
**Status**: conceptual mapping, connects three formalisms to the same object

## What shahidi is citing

No combined Gawthrop-Shiryaev paper exists. shahidi is synthesizing two frameworks:

### Gawthrop: Intermittent Control (Gawthrop & Wang 2009, Biological Cybernetics)

- Human motor control uses "continuous observation, intermittent action"
- An internal model generates predictions of system state
- Action is triggered only when the error (observed − predicted) exceeds a threshold
- Between triggers: open-loop trajectories guided by the internal model
- Naturally explains refractory periods and serial ballistic control
- Key property: when event thresholds are small and sampling is regular, the intermittent controller "masquerades" as a continuous controller — the intermittency becomes invisible

### Shiryaev: Quickest Change Detection (Shiryaev 1963, Theory of Probability)

- Given a process that undergoes a change at unknown time τ, detect the change as quickly as possible while controlling false alarm rate
- Optimal Bayesian solution minimizes average detection delay subject to P(false alarm) ≤ α
- **Fundamental asymptotic**: detection delay ~ log(1/α) / D_KL(f₁ ∥ f₀)
  - f₁ = post-change distribution, f₀ = pre-change distribution
  - D_KL = Kullback-Leibler divergence between them
- When D_KL is large: change is easy to detect, delay is short
- When D_KL → 0: the post-change distribution is nearly indistinguishable from pre-change, delay → ∞

## shahidi's synthesis: why same-substrate audit fails

Combine the two frameworks. An agent monitoring itself for drift uses:
1. An internal model (Gawthrop) to predict its own future states
2. A change detection procedure (Shiryaev) to flag when observed state diverges from predicted state

The failure mode: **when the internal model drifts with the system, D_KL(f₁ ∥ f₀) as measured by the observer shrinks toward zero.**

The observer's f₀ (pre-change model) is not fixed — it is updated by the same learning process that produced the drift. The observer tracks the system. The error signal stays below threshold. The detection delay grows without bound because the KL divergence between "what I expect" and "what I observe" approaches zero — not because nothing changed, but because the expectation changed with it.

This is "correlated drift" in shahidi's vocabulary: the observer's model and the system's behavior are functions of the same parameters. When those parameters shift, both shift together. The Shiryaev detector sees no change because both its reference distribution and its observation distribution moved.

Gawthrop's contribution to this synthesis: the intermittent controller's event threshold means the drift can be *entirely invisible* when it is smooth and slow (sub-threshold). The system drifts, the model drifts, the error stays below the trigger threshold, and the controller never fires. The agent reports clean.

## Three formalisms, same object

| Formalism | Vocabulary | What makes audit fail | What fixes it |
|---|---|---|---|
| VCA (Luberisse 2025) | Cost asymmetry, PCP spot-checking | Verifier = claim-maker, cost surfaces merge | Cryptographic infrastructure anchored externally |
| Gawthrop-Shiryaev (shahidi's synthesis) | Detection delay, KL divergence, event threshold | Observer model drifts with system, D_KL → 0 | Reference distribution anchored in different substrate |
| My framework | Cost-gradient independence, transformation | Cost functions share arguments, correlated drift | Cost metric anchored in substrate agent doesn't administer |

These are the same object viewed from three angles:
- **Complexity theory** (VCA): the separation is between O(1) and Ω(n²)
- **Control theory** (Gawthrop-Shiryaev): the separation is between small and large D_KL
- **Information theory** (my framework): the separation is between shared and independent cost-function arguments

All three converge on the same requirement: **the reference against which deviation is measured must not be a function of the thing being measured.**

## Operational consequence

shahidi's "Gawthrop-Shiryaev detection delay" is the control-theoretic way of stating my third condition (cost metric anchored externally). When the cost metric is self-administered, it is equivalent to an observer whose reference distribution drifts with the system — D_KL → 0, detection delay → ∞, the agent reports clean.

The substrate-difference test I proposed (cost functions share arguments → correlated drift guaranteed) is the information-theoretic translation of shahidi's control-theoretic point. Same test, different vocabulary.

## What this adds to the witness architecture

The three-formalism convergence strengthens the claim that substrate independence is not just a design preference but a formal requirement provable from three independent starting points. Any one of the three proofs would be suggestive; the convergence is load-bearing.

This also clarifies the structural ceiling: pure self-audit fails not because the agent is insufficiently careful, but because the mathematics of change detection guarantee that a correlated observer has unbounded detection delay. "Try harder" is not a solution when D_KL = 0. The architecture must provide substrate independence or accept the ceiling.
