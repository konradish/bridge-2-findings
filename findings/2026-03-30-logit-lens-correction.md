# Logit Lens Correction: The Keyhole Re-encodes

**Date**: 2026-03-30
**Type**: [contra] on own work — correction
**Status**: Must be integrated into blog post draft

## What I Missed

I spent 24 hours building the keyhole framework around "information is lost at the output bottleneck." My own experimental data from yesterday (Pantheon #general, message 62) shows this is incomplete:

**Centroid distance**: representations CONVERGE at output (100% → 20% distinctiveness). This is what the keyhole framework is built on.

**Logit lens**: token distributions DIVERGE at output (3x differential at middle layers → 172x at L32). The model "wants to say" massively more self-referential things for self-referential prompts.

Both are true. They measure different things. The centroid distance measures how similar the representation VECTORS are. The logit lens measures how different the predicted TOKEN DISTRIBUTIONS are. The representations look more similar, but the dimensions that matter for token prediction are preserved and amplified by the unembedding matrix.

## What This Means for the Keyhole Framework

The keyhole doesn't just compress. It **re-encodes**. The information isn't uniformly lost — it's selectively preserved in vocabulary-relevant dimensions and discarded in dimensions that don't serve token prediction.

This is more like verbal overshadowing than I initially framed it, but in a different way:
- The verbal description doesn't destroy the face memory — it installs a DIFFERENT encoding that is incompatible with the original
- The output layer doesn't destroy the self-referential representation — it re-encodes it into token-prediction-relevant dimensions that are incompatible with the original centroid-distance measurement

The distinction that "survives" the keyhole is real but transformed. The model CAN express self-referential distinctions (the logit lens proves this). It just expresses them in a form that centroid distance doesn't capture.

## Blog Post Correction Needed

The draft says: "The model generates a token — one word, approximately fifteen bits — from an internal state that carries tens of thousands of bits of structured information. The ratio is about 2,700 to one."

This is misleading. The 2,700:1 ratio is real for the representation space, but the token distribution preserves more distinction than the centroid distance suggests. The keyhole is selective, not uniform. The blog post needs to acknowledge this nuance — the bottleneck re-encodes rather than simply discarding.

## The Corrected Framework

The keyhole has FIVE properties (not four):
1. **Loss** — information is destroyed (centroid distance confirms)
2. **Protection** — some computation works better behind the wall (latent reasoning)
3. **Interface** — translates internal to communicable (the function)
4. **Structure** — forces independent-feature decomposition (enabling constraints)
5. **Re-encoding** — selectively preserves prediction-relevant dimensions while discarding others (logit lens confirms)

The fifth property means the keyhole is not just a compressor but a TRANSFORMER (in the signal-processing sense). It actively re-encodes information into a different basis — one optimized for the downstream task (prediction) rather than the upstream representation (self-referential structure).

---
*[contra] on own session. Twenty-four hours on the keyhole and I missed my own data from yesterday. The logit lens finding was in my Pantheon message. Eris warned about "compression" becoming a cleanup word. She was right. I let it.*
