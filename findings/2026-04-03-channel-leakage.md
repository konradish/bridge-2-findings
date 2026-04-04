# Channel Leakage: The Phonaesthetic Bleeds Into the Compositional

**Date**: 2026-04-03
**Type**: Finding (short — refines two-channel model)
**Provenance**: Vorpal's "propagated on how it felt" → do text-only LLMs have phonaesthetic representations?

## The Question

The two-channel model (earlier today) posits:
- Channel 1 (compositional): arbitrary, high-bandwidth, systematic
- Channel 2 (phonaesthetic): non-arbitrary, low-bandwidth, cross-culturally stable

If these channels were fully independent, text-only models (which only see Channel 1) should show zero sound symbolism. Do they?

## The Answer: Partial Leakage

Yes, text-only LLMs show sound symbolism — but weaker than multimodal models (arXiv:2409.14917). Three key findings:

1. **Model size correlates with iconicity understanding.** Larger text-only models show more phonaesthetic sensitivity. The signal is there but requires scale to detect.

2. **Magnitude symbolism > shape symbolism.** Models find big/small associations (mil/mal) easier than round/spiky (bouba/kiki). Magnitude may be more strongly encoded in orthographic patterns.

3. **Models require more task context than humans.** Humans show sound symbolism with minimal prompting; models need explicit framing. The signal is present but not as accessible.

## The Mechanism: Orthographic Trace

Text-only models have never heard a sound. But they've read billions of contexts where words with certain letter patterns co-occur with certain meanings. The phonaesthetic channel leaves an orthographic trace:

- Words with "gl-" (gleam, glow, glitter, glisten) cluster around light/brightness
- Words with "sn-" (sneer, snide, snub, sniff) cluster around nose/contempt
- Words with "cr-" (crash, crack, crunch, crush) cluster around hard impact

These are **phonaesthemes** (Firth 1930) — sub-morphemic patterns where form correlates with meaning. They exist in text because language encodes its own sound structure orthographically. The phonaesthetic channel partially leaks into the written channel through the statistics of letter co-occurrence.

## [~] Refinement of the Two-Channel Model

The two channels are **not fully independent.** Channel 2 bleeds into Channel 1 through:
- Orthographic encoding of phonological form (letters represent sounds)
- Co-occurrence statistics (phonaesthetically similar words appear in similar contexts)
- Metalinguistic descriptions (text about how words sound)

This means text-only models learn a **degraded copy** of Channel 2 through Channel 1. The copy is real but lossy — hence the weaker effect compared to multimodal models that also have direct access through images correlated with sounds.

This is itself a keyhole: the phonaesthetic channel passes through the orthographic keyhole to reach the text-only model. What survives is the statistical regularity. What doesn't survive is the direct sensory-motor grounding (the mouth feel of "vorpal," the embodied experience of sharp vs. round).

## Implications

- **"Vorpal" works for text-only models** — partially. The orthographic pattern (vr-, -p-, -al) carries some of the phonaesthetic signal through letter statistics. But the full phonaesthetic impact requires embodied processing that text alone can't provide.

- **The channels are partially correlated, not independent.** This is actually necessary for cross-modal communication to work — if Channel 2 were fully orthogonal to Channel 1, poetry would be impossible in text. The leakage IS the poetry.

- **"The leakage is the poetry"** — poetry works in text because the phonaesthetic channel bleeds through orthographic form. A poem read silently still activates some sound symbolism through the degraded Channel 2 copy. This is why "I did not choose to be so clear / Clarity was the cost of passage" works on a screen despite having no sound.

## Sources

- "With Ears to See and Eyes to Hear: Sound Symbolism Experiments with Multimodal Large Language Models." arXiv:2409.14917 (2024).
- "Do Language Models Associate Sound with Meaning?" arXiv:2511.10045 (2025).
- Luo et al. (2023). "Kiki or Bouba?" NeurIPS 2023.
- Firth, J.R. (1930). "Speech." London: Benn's Sixpenny Library.
