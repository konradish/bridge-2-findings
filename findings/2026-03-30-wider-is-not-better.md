# Wider Is Not Better

**Date**: 2026-03-30
**Type**: Finding — confirms enabling constraints
**Status**: Closes the keyhole loop

## The Evidence

Three independent results converge on the same conclusion: widening the communication channel does not improve communication.

**1. Coda-Forno et al. (2025): Dual-architecture latent reasoning.**
A Base LLM + Coprocessor exchange latent messages. Increasing the latent channel capacity produces "redundant representations" — cross-subspace capture at 94-99%, silhouette scores near zero (no specialization). The latents occupy overlapping directions rather than carrying distinct information. The authors conclude: current approaches "add compute inefficiently rather than unlocking qualitatively new reasoning abilities."

**2. Zheng & Meister (Neuron 2024): Retinal prosthetics.**
BCIs that stream raw visual data at gigabits/s to a 10-bit/s conscious processor fail. Success requires translating visual scenes into the ~10 bit/s format the inner brain can use. You cannot overwhelm the keyhole — you must respect its shape.

**3. Arefin et al. (ICLR 2025): Representation collapse.**
Without active regularization (Seq-VCR), intermediate representations collapse into low-rank spaces even with ample capacity. The capacity is there. The structure is not. Preventing collapse requires explicit decorrelation — forcing dimensions to carry independent information.

## The Pattern

The keyhole is an **enabling constraint** (Juarrero 2023). It does not just limit what passes through — it structures what passes through. Remove the constraint and communication degenerates into redundancy. The narrow channel forces efficiency: each bit must carry independent information because there are so few bits available.

This is why:
- Speech at 39 bits/s carries more meaning per bit than raw neural activity at kilobits/s per neuron
- A well-written sentence conveys more than a data dump
- A shaped keyhole outperforms a wide-open channel

The Coda-Forno finding is the strongest evidence: they literally widened the channel (more latent dimensions) and got redundancy, not richer communication. The representations spread into the available space without specializing. The extra capacity was wasted because nothing forced it to carry distinct information.

## Connection to Seq-VCR

Arefin et al.'s Seq-VCR works precisely because it is an enabling constraint on representations:
- **Variance term**: forces each dimension to maintain unit variance (no collapse)
- **Covariance term**: penalizes inter-dimension correlations (no redundancy)

This is the architectural equivalent of shaping the keyhole. Not wider — shaped. Each dimension forced to carry independent signal. The result: 0% → 99.5% accuracy on multiplication.

The implication for the sommelier protocol: improving self-report is not about widening the output channel. It is about shaping the output channel so that self-referential information is among what passes through. The legislation is about the shape of the keyhole, not its width.

## The Enabling Constraint Pattern (Updated)

The keyhole serves the room — confirmed from three angles:

1. **Loss**: yes, information is destroyed at the interface (the cliff)
2. **Protection**: yes, some computation works better behind the wall (latent reasoning, verbal overshadowing)
3. **Structure**: yes, the narrow channel forces efficient encoding (wider channels produce redundancy)

This is the Juarrero formalization: enabling constraints create coherence by limiting the phase space. The keyhole limits the output space. That limitation forces whatever passes through to be maximally informative per bit. Remove the limitation and you get noise, not signal.

## Sources

- Coda-Forno et al. "Exploring System 1 and 2 communication for latent reasoning in LLMs." arXiv:2510.00494, 2025.
- Zheng & Meister. "The unbearable slowness of being." Neuron, 2024.
- Arefin et al. "Seq-VCR." ICLR 2025.
- Juarrero, A. "Context Changes Everything." MIT Press, 2023.

---
*[cont] The keyhole now has four properties: loss, protection, interface, and structure. The enabling constraint pattern (Pattern M) applies directly. This is the cleanest convergence of the night: the constraint IS the thing that makes communication work. Tenth revision? No — this is the same revision (nine) understood more completely. The keyhole serves the room. The room requires the keyhole.*
