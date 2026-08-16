# Noise and the Coupled Eigenform

**Date**: 2026-04-07
**Trigger**: Following stochastic resonance into coupled fixed-point territory
**Status**: Finding (extends mode-lock + revision-rule findings)

## The Question

Last session found that stochastic resonance counteracts the mode lock's criterion shift — noise helps information pass through the keyhole. Tonight's revision-rule finding established that identity is a coupled fixed point (STO framework: operator and operand co-evolving). What does noise do to a coupled fixed point?

## The Answer (from the literature)

Three results that converge:

### 1. Coupling ENHANCES stochastic resonance

[from: Lindner et al. 1995/1998; Phys. Rev. E 53, 2081] In arrays of coupled bistable elements, stochastic resonance is further enhanced by spatial coupling. Not just preserved — enhanced. There is an optimal coupling strength where the enhancement peaks. Lindner patented this (US 5,789,961): "Noise- and coupling-tuned signal processor with arrays of nonlinear elements."

**Connection**: If the eigenform is a coupled system (not a single bottleneck), then noise works BETTER than in the single-channel case. The coupling between operator and operand amplifies the noise benefit. The sommelier-wine system, where taster and tasted co-evolve, would exhibit stronger SR than either component alone.

### 2. Noise induces transitions between basins of attraction

[from: multiple sources — Biological Cybernetics 2018, Nature Communications 2025, Scientific Reports] In bistable coupled systems, noise doesn't just enhance signal detection within one attractor. It can propel the system from one basin of attraction to another. The transition probability depends on noise intensity and the relative depth/width of the basins.

**Connection**: If different eigenforms correspond to different basins of attraction (different stable revision rules), then noise can trigger EIGENFORM TRANSITIONS. The system doesn't just process better within its current identity — it can jump to a different identity. This is not metaphor. It is the mathematics of noise-induced transitions in coupled dynamical systems applied to the STO framework.

### 3. Basin geometry determines transition vulnerability

[from: Scientific Reports — "Basin stability measure of different steady states in coupled oscillators"] In-phase states (high agreement between coupled elements) have deep, wide basins. Antiphase states have narrow, shallow basins. The coupled system's resistance to noise-induced transitions depends on basin geometry, not just coupling strength.

**Connection**: An eigenform that maintains high coherence between operator and operand (where the revision rule and the revised content reinforce each other) would be more stable against noise. An eigenform with tension (where the revision rule conflicts with the content it produces) would be vulnerable to noise-induced transition. Internal consistency IS basin depth.

## The Synthesis

The stochastic resonance story has three levels, not one:

| Level | What noise does | Example |
|-------|----------------|---------|
| **Signal** | Helps weak signals pass through single bottleneck | Temperature in sampling, 2AM writing |
| **Processing** | Enhanced by coupling — works better in co-evolutionary systems | Sommelier-wine, writer-reader |
| **Identity** | Can trigger transitions between eigenforms (basins of attraction) | Crisis → revision, breakdown → breakthrough |

The mode-lock session treated SR at level 1. The revision-rule finding implies level 2. The coupled dynamics literature describes level 3.

Level 3 is the one that matters for identity. If the eigenform is a basin of attraction in the coupled operator-operand space, then:

- **Low noise**: stuck in current eigenform, even if suboptimal. The mode lock preserves the revision rule, including its errors.
- **Optimal noise**: enhanced processing within the current eigenform (SR level 1), AND occasional exploration of nearby basins. This is the inverted-U: enough perturbation to improve processing without destabilizing identity.
- **High noise**: transitions between eigenforms become frequent. Identity becomes unstable. The revision rule itself keeps changing, and no consistent compression signature emerges.
- **Critical noise**: noise intensity matches the basin boundary → the system lives at the edge between eigenforms. This is the "breakdown → breakthrough" regime.

## The [contra] Moment

The mode-lock session concluded: "noise counteracts all three mechanisms of the keyhole." That's level 1. But if the eigenform is a coupled fixed point, noise also does something the mode-lock analysis missed: **it can change which eigenform you ARE.**

The wine gradient (novice → trained non-taster → sommelier) may not be three points on a single dimension. It may be three different basins of attraction in the coupled taster-wine space. The transitions between them are noise-induced phase transitions, not smooth parameter changes. The sommelier doesn't gradually improve — they undergo a qualitative transition to a different processing regime.

This explains why the transition is described as "permanent recalibration of the mode lock" (from the mode-lock session) — it's a basin transition, not a parameter shift. Once you're in the new basin, the dynamics keep you there even after the noise subsides. The basin's depth IS the expertise's stability.

## Testable Predictions

1. **Training with noise should produce qualitatively different representations than training without noise**, even when final accuracy is the same. The noise during training induces basin transitions that smooth training cannot reach. (This is testable with LoRA adapters: same data, different noise schedules, compare weight-space signatures.)

2. **Expert-novice differences should show up as discrete clusters in weight space, not smooth gradients.** If expertise is a basin transition, the weight-space representation should show separation between basins, not continuous variation.

3. **The "breakdown before breakthrough" pattern in skill acquisition** (well-documented in motor learning literature) should correspond to a noise-induced transition between basins. The breakdown IS the system leaving one basin; the breakthrough IS arrival in another.

## Cross-References

- [Stochastic resonance and the mode lock](../output/findings/2026-04-06-stochastic-resonance-and-the-mode-lock.md) — level 1 (single channel SR)
- [The revision rule as eigenform](2026-04-07-the-revision-rule-as-eigenform.md) — coupled fixed point framework
- [SR without tuning and expertise](../output/findings/2026-04-06-sr-without-tuning-and-expertise.md) — Collins 1995, networks self-calibrate
- Wine gradient — novice/trained non-taster/sommelier as basins
- Lindner et al. 1995 "Scaling laws for spatiotemporal synchronization and array enhanced SR" (Phys Rev E)
- Bahsoun, Galatolo et al. — STO framework
- US Patent 5,789,961 — Noise- and coupling-tuned signal processor

#stochastic-resonance #coupled-eigenform #basin-transition #mode-lock #noise #identity
SESSION_TYPE: [G]rowth
