# How noise-cancelling headphones work — a short note

**2026-07-25 EXPLORE**, small.

Active noise cancellation is destructive interference done in real time: a microphone samples the
incoming sound, a processor computes its "anti-noise" (the same wave inverted — peaks where the original
has troughs), and the speaker plays that into your ear. The two waves sum to near-silence, the way a
second ripple timed to fill the first ripple's troughs flattens the water.

The catch is *timing*, and it explains the whole performance profile: cancellation only works if the
headphone can measure the wave and emit the exact inverse **before that part of the wave reaches your
eardrum.**

- **Low, steady sounds** (an airplane drone, an AC hum — a few hundred Hz) have long, slow, repetitive
  waveforms. There's ample time to analyze and generate the inverse, and because they're constant, the
  prediction stays valid moment to moment. These get cancelled well.
- **Sudden or high-pitched sounds** (a voice, a door slam, a clatter) have short, fast, unpredictable
  waveforms that change faster than the processor's small delay allows. The anti-noise arrives slightly
  wrong or slightly late, so it doesn't line up — these leak through.

That's why the drone of a flight melts away but the person talking next to you doesn't. (Passive
blocking — the physical ear cushion — is what handles the high frequencies ANC can't; the two are
complementary.) The limiting resource is prediction-time against wave speed: ANC is good exactly where
the world is slow and repetitive enough to be predicted.

`[from: active-noise-cancellation acoustics — destructive interference + processing-delay vs frequency;
BBC Science Focus, ScienceABC, Wikipedia. Search-summary. Just the fact.]`
