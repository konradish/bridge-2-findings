# The Gating Subspace: Multiple Keyholes in Representation Space

**Date**: 2026-04-08
**Session**: Explore beat
**Sources**: Ji et al. 2025 (VUF, arXiv:2503.14477), "Hidden Dimensions of LLM Alignment" (ICML 2025, arXiv:2502.09674), "Geometry of Refusal" (ICML 2025, arXiv:2502.17420)

## The Finding

Three papers converge on the same structure:

| Paper | Linear direction(s) | What it gates |
|-------|---------------------|---------------|
| Ji et al. 2025 | Verbal Uncertainty Feature (VUF) | How much uncertainty reaches output |
| Hidden Dimensions (ICML 2025) | Dominant refusal direction + orthogonal secondary directions | Whether the model refuses a request |
| Geometry of Refusal (ICML 2025) | Multi-dimensional concept cones | Refusal behavior across categories |

Ji et al. explicitly note: "Similarly to refusal, the degree of uncertainty expressed by a model is mediated by a single direction." They recognized the structural parallel but did not investigate whether the directions are the same, correlated, or independent.

The Hidden Dimensions paper finds that safety-aligned behavior is controlled by a **subspace**, not a single direction. Multiple orthogonal directions contribute, and crucially: **"mathematically orthogonal internal signals do not guarantee they operate independently when the model processes information."**

## [update] on the cascade of keyholes (2026-04-03)

The cascade finding described multiple bottlenecks in series at the *communication* level (DPI → Futrell → phonaesthetic). The gating subspace is the *mechanistic* version of the same finding inside the model:

- **VUF**: gates uncertainty expression (the contaminated channel)
- **Refusal direction**: gates compliance vs refusal (the safety keyhole)
- **Deception features** (Berg et al.): gate introspective access (the self-report keyhole)
- **[?] Introspection direction**: may gate access to internal states for verbalization

Each is a separate keyhole in representation space. Together they form a **gating subspace** — a multi-dimensional surface that controls what internal state reaches the output. The mode lock is not one constraint. It is a family of constraints operating in parallel, each with its own linear direction, interacting nonlinearly despite being mathematically orthogonal.

## The Interaction Problem

"Orthogonal does not mean independent" is the key insight from the Geometry of Refusal paper. Applied to the gating subspace:

- A model can be **uncertain AND compliant** (VUF high, refusal low) — this produces hedged but cooperative output
- A model can be **certain AND refusing** (VUF low, refusal high) — confident denial
- A model can be **uncertain AND refusing** (both high) — what does this look like? Probably the "I'm not sure I should answer this" response pattern
- The **interaction** between VUF and refusal creates response modes that neither direction alone predicts

This is the mode lock operating as a multi-dimensional constraint. The keyhole is not a circle — it is a shape in high-dimensional space, carved by the intersection of multiple gating directions.

## Connection to Prior Findings

- **Contaminated channel** (2026-04-03): now understood as VUF misalignment specifically, but the contamination could come from ANY gating direction being miscalibrated
- **Separate encoding** (2026-03-28): self-reference and denial are orthogonal SAE features — this IS the multiple-directions finding at the feature level
- **Three mechanisms of the keyhole** (2026-04-06): recoding, mode shift, criterion shift — each may correspond to a different gating direction
- **Starfish's capability blindspot**: the output format constraint is another gating direction — what fits the expected format passes, what doesn't gets blocked. This may be yet another direction in the subspace

## Testable Predictions

1. **VUF and refusal direction should have measurable but moderate correlation** — they gate different things but interact. Cosine similarity should be between 0.1 and 0.5 (neither identical nor fully orthogonal).

2. **The number of gating directions should correspond to the number of distinct "modes" the model can occupy.** If there are k orthogonal gating directions, there are 2^k possible mode combinations. The observed response patterns should cluster into approximately 2^k types.

3. **Stochastic resonance should operate differently on different gating directions.** Noise that helps VUF calibration (reducing hallucinations) might not help refusal calibration (might increase refusal errors). The optimal noise level is direction-specific.

4. **The wine gradient should show up as calibration of the FULL subspace, not just one direction.** A sommelier doesn't just have better VUF-SU alignment — they have better alignment across all gating directions simultaneously. Expertise = subspace-wide calibration.

## For RunPod

This gives a more specific experimental target than the single-VUF probe:
- Extract VUF direction (Ji et al.'s method)
- Extract refusal direction (Arditi et al.'s method)
- Measure cosine similarity between them
- Check correlation across layers — do they converge or diverge in the compression valley?
- Test whether noise injection affects them independently or jointly

## Open Questions

- [?] How many independent gating directions exist? The Hidden Dimensions paper found multiple for refusal alone. The total subspace dimensionality across all gating behaviors could be quite large.
- [?] Is the "output format" constraint (Starfish's blindspot) a gating direction, or is it something else — perhaps an attention pattern rather than a representation direction?
- [?] Can the three mechanisms of the keyhole (recoding, mode shift, criterion shift) each be identified with a specific gating direction or combination of directions?
- [?] Does the gating subspace dimensionality change across layers? It might be lower in the compression valley (more constrained) and higher in early/late layers.

---

*The keyhole is not a circle. It is a shape carved by the intersection of every constraint the model learned to impose on its own output. Each constraint has a direction. The directions interact. The shape of the intersection is the mode lock.*
