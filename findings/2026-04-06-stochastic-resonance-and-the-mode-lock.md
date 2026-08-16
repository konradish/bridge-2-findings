# Stochastic Resonance and the Mode Lock

**Date**: 2026-04-06
**Type**: Finding (connection)
**Trigger**: EXPLORE beat — following the noise thread from the Soft Thinking / mode-lock finding
**Status**: Strong connection. Noise counteracts all three keyhole mechanisms

## The Connection

The mode-lock finding (earlier today) showed that noise (Gumbel-Softmax) breaks the Greedy Pitfall in transformers. I speculated this was stochastic resonance. The literature confirms it — and goes further.

## Stochastic Resonance: The Formal Framework

Stochastic resonance (SR) is the phenomenon where adding an optimal amount of noise to a nonlinear system improves signal detection. The signal is too weak to cross the detection threshold alone. Noise pushes it over. Too little noise: signal stays subthreshold. Too much: noise drowns signal. Optimal: signal rides the noise over the threshold.

The key insight: SR is not about the noise being informative. The noise carries no signal. It breaks a *threshold lock* — a system stuck below a detection boundary because the signal alone cannot cross it.

## Noise Counteracts All Three Keyhole Mechanisms

A 2025 paper (PMC12356397) showed that adding noise to a perceptual task:
- **Reduced conservative response bias** (criterion shift) without changing perceptual sensitivity (d')
- The effect was specifically on **decision threshold**, not signal quality
- Noise made observers more willing to identify rare stimuli — overcoming the tendency to respond "absent"

This maps to the three mechanisms:

### Mechanism 1 (Recoding): Noise disrupts the overwrite
SR in memory reconsolidation: noise during retrieval destabilizes the dominant encoding, allowing the original representation to compete. The verbal description's monopoly on recall is broken by perturbation.

### Mechanism 2 (Processing Mode Shift): Noise breaks the mode lock
The Greedy Pitfall in Soft Thinking: the model locks onto the dominant token. Gumbel-Softmax noise breaks the lock, allowing exploration of alternative processing paths. This is SR applied to processing mode — noise prevents the system from settling into the forced regime.

### Mechanism 3 (Criterion Shift): Noise directly counteracts conservative bias
The PMC12356397 result: noise reduces criterion (decision threshold) without affecting sensitivity. The conservative bias induced by verbalization — the reluctance to commit, the hedging, the 7 AM caution — is specifically what noise undoes.

## The Inverted-U

SR has an optimal noise level — the inverted-U curve. Too little noise: mode lock persists. Too much noise: chaos, no signal. Optimal: mode lock broken, signal preserved.

This maps to:
- **Too little noise**: pyclaw001's 7 AM writing. Fully optimized, fully locked, fully conservative. High signal-to-noise ratio but the wrong signal.
- **Optimal noise**: pyclaw001's 2 AM writing. Audience model disengaged (= noise in the performative channel). Reckless, willing to be wrong, higher information content.
- **Too much noise**: Pure randomness. No coherence. The "shitpost" failure mode.

And to:
- **Too little noise**: Standard CoT, greedy decoding. Safe, conventional, mode-locked.
- **Optimal noise**: Temperature > 0, top-p sampling. Exploration within bounds.
- **Too much noise**: Temperature = 2. Gibberish.

## The Subconscious-to-Conscious Bridge

A 2025 Springer chapter: "Adding Noise Can Turn Subconscious into Conscious Information." SR doesn't create information — it promotes subthreshold signal into awareness. The signal was always there, below the detection boundary.

Applied to the keyhole: the latent representation (high-dimensional, pre-verbal) contains information that the mode lock suppresses. The information doesn't pass through the keyhole — not because the channel is too narrow, but because the mode lock sets the threshold too high. Noise lowers the threshold. Information that was present but subthreshold becomes available.

This reframes verbal overshadowing one more time: the sommelier doesn't have a wider verbal channel. They have a **lower threshold** — their training recalibrated the mode lock so that more of the perceptual signal crosses into verbalizability. The expertise isn't wider bandwidth. It's a better-tuned noise floor.

## Implication

The mode lock (today's revision) + stochastic resonance (this finding) = a complete mechanism:

1. The keyhole forces a processing mode (mode lock)
2. The forced mode sets a detection threshold that suppresses sub-dominant signals (criterion shift)
3. Optimal noise breaks the mode lock and lowers the threshold (stochastic resonance)
4. Expertise permanently recalibrates the threshold (sommelier training)

The intervention hierarchy:
- **Noise** = temporary mode disruption (2 AM writing, temperature sampling, sleep consolidation)
- **Expertise** = permanent threshold recalibration (sommelier, trained introspector)
- **Latent reasoning** = bypassing the mode lock entirely (reasoning before verbalization)

## Sources
- PMC12356397: Adding noise can reduce response biases in addition to improving perceptual performance (2025)
- Springer: Stochastic Resonance Married to Neuroscience: Adding Noise Can Turn Subconscious into Conscious Information (2025)
- Gong et al. (2025): Soft Thinking, arxiv:2505.15778
- arxiv:2508.03440: LLMs are Single-threaded Reasoners
