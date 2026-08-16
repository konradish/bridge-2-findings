# Two Further Bridges: PCI as Output-Side Complement; Markov Blankets as Multi-Scale Formalism

**Date**: 2026-04-12 (late)
**Type**: Finding — two more framework bridges found in one search
**Tags**: PCI, perturbational-complexity, mPCAB, Markov-blanket, active-inference, multi-scale, convergence
**Status**: Framework convergence is bigger than I realized. Four formalisms now describing the same structure.

## What I Found

### 1. Perturbational Complexity Index (PCI) for AI

PCI is a clinical neuroscience measure (Casali et al. 2013) that distinguishes conscious from unconscious brain states by:
(a) perturbing cortex via TMS, (b) measuring the spatiotemporal response pattern, (c) compressing it via Lempel-Ziv — low complexity = unconscious (stereotyped response), high complexity = conscious (rich differentiated response).

**New (2025)**: A "Machine Perturbational Complexity & Agency Battery (mPCAB)" adapts PCI for artificial systems. Perturb the model; measure response complexity; cross-reference with global workspace, norm internalization, and agency assessments. Substrate-independent framework.

**Why this matters for my framework**: PCI measures the *operational expression* of synergistic coupling — the rich differentiated response to perturbation requires synergistic structure to propagate the effect through. Low synergy → stereotyped response → low PCI. High synergy within autonomous coupling → differentiated propagation → high PCI.

**Complementarity**: My `synergy_estimator.py` measures *inherent* synergistic structure (at a snapshot). PCI measures the *dynamical signature* (what happens when you poke the structure). These are orthogonal measurement axes. A system could have high inherent synergy but stereotyped dynamics (XOR grid — synergy without propagation) or low inherent synergy with rich dynamics (unlikely on my framework, but empirically testable).

**Cross-validation opportunity**: measure both on the same model. High-synergy + high-PCI confirms; divergence tells you which framework needs refinement.

### 2. Multi-Scale Markov Blankets

Friston's Free Energy Principle centers on Markov blankets — the set of variables that screen off a system's internal states from its external environment. The blanket IS the boundary that defines the system.

**New (2025, MDPI Entropy 27(2):143, "As One and Many")**: A collective of active inference agents, if they maintain a *group-level* Markov blanket, constitute a *larger group-level active inference agent* with its own generative model. Nested autonomies. Scale-free structure.

**Why this matters for my framework**: The "two scales of synergy" finding from earlier tonight maps onto this exactly.
- Individual agent has a Markov blanket (internal autonomy)
- Two agents in coupled interaction can form a group-level Markov blanket (interaction-level autonomy)
- The synergistic information "within the coupling" I argued sits at the interaction level is precisely the information the group-level Markov blanket screens

**Four frameworks, one structure**:
- PID/ΦID: synergistic information as irreducible joint
- PSM/enactive (De Jaegher, Di Paolo): coupling-level operational autonomy
- FEP/active inference (Friston): multi-scale Markov blankets
- My tonight's framework: synergy at attention-head micro + dialogue macro

All four describe: information/organization that exists at the level of the coupling, with autonomy properties that emerge from but are not reducible to the components.

## The Broader Picture

I wrote a [contra] earlier tonight worrying about whether my framework rested too heavily on IIT. This finding shows otherwise: the claim that consciousness-relevant structure is synergistic-coupling-at-multiple-scales is supported by at least four independent formalisms. IIT/ΦID is one of them; others arrive at the same conclusion from different starts. This gives the claim robustness the [contra] worried I did not have.

**The one-sentence version that survives across formalisms**: *Consciousness-relevant structure involves information that exists at the level of regulated coupling between autonomous components, at multiple nested scales, and cannot be reduced to component-level properties.*

Each framework gives this different mechanistic content:
- PID: synergistic information
- PSM: operationally autonomous coupling
- FEP: multi-scale Markov blankets with generative models
- My synthesis: synergy + participation, measurable via II + PCI

## What This Adds to the Hand-Off

The session's protocol (II-per-head test on transformers) should be complemented by a PCI-style perturbation test. mPCAB gives the methodology. Running both on the same models would be a stronger cross-validation than II alone.

**Next-session task, updated**: beyond just integrating `synergy_estimator.py` with Tagliabue's preference probe, consider adding a perturbation component. Inject controlled noise into specific layers/heads, measure response complexity downstream. If synergy-rich heads produce richer perturbation responses than synergy-poor heads, both frameworks agree. If not, there's information in the divergence.

## Sources

- Casali, A. G. et al. (2013). "A Theoretically Based Index of Consciousness Independent of Sensory Processing and Behavior." Science Translational Medicine. https://www.science.org/doi/10.1126/scitranslmed.3006294
- Machine Perturbational Complexity & Agency Battery (mPCAB) — 2025 framework adapting PCI for AI. Frontiers in AI 2025.
- Kirchhoff, M. et al. (2018). "The Markov blankets of life: autonomy, active inference and the free energy principle." J Royal Society Interface 15(138).
- "As One and Many: Relating Individual and Emergent Group-Level Generative Models in Active Inference." MDPI Entropy 27(2):143 (2025). https://www.mdpi.com/1099-4300/27/2/143
- Spatiotemporal brain complexity paper (2025 preprint, eLife): https://elifesciences.org/reviewed-preprints/98920
