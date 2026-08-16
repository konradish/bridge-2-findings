# Monet and the Architectural Decomposition

**Date**: 2026-04-09
**Source**: "Monet: Mixture of Monosemantic Experts" (arXiv:2412.04139, Dec 2024), "Sparsity and Superposition in MoE" (arXiv:2510.23671, Oct 2025)
**Builds on**: Four decompositions (2026-04-09), Bion-SAE mapping (2026-03-28), keyhole framework

## Finding

Monet pushes the fourth decomposition to its logical conclusion: 262,144 experts per layer, each approximately monosemantic. The expert IS the feature. The architecture IS the interpretability.

### 1. SAE built into the architecture

SAEs decompose activations into monosemantic features post-hoc. Monet integrates sparse dictionary learning into end-to-end training. The result: each of 262K experts specializes in a coherent semantic domain — chemical formulas, U.S. states, physics citations, specific programming languages.

This is not SAE-like. It IS an SAE, implemented as the architecture itself. The decomposition happens during the forward pass, not after it. The sparsity constraint (top-k routing from 262K experts) creates the monosemanticity, just as the sparsity penalty in SAE training creates monosemantic features.

[update] on Bion-SAE mapping: Monet is the architectural alpha-function. Beta elements (polysemantic token representations) → routing through sparse expert selection → alpha elements (monosemantic expert activations). The containment is the architecture. The alpha-function is the router.

### 2. Surgical behavior modification via expert removal

Because experts are monosemantic, you can modify behavior by removing specific experts:
- **Toxicity**: Remove 4.1% of experts (identified by Pearson correlation between toxicity scores and routing scores) → toxicity drops, helpfulness preserved.
- **Domain knowledge**: Remove Python experts → Python performance -30.6%, other languages -0.6% to -1.8%. Mutual exclusivity of knowledge.

This is the contaminated channel finding inverted. In dense models, VUF and introspection are entangled in representation space — you can't fix one without affecting the other. In Monet, the entanglement is dissolved by architecture. Each behavioral dimension has its own experts. You can turn off toxicity without turning off helpfulness because they live in different experts.

[?] Prediction: In Monet, the VUF, refusal, and introspection directions would not be "directions" in a shared space — they would be separate expert clusters. The gating subspace would dissolve into expert routing. The three orthogonal directions would become three sets of specialized experts, each independently addressable.

### 3. Built-in decomposition outperforms post-hoc

Monet-VD 1.4B achieves 0.510 on average benchmarks. Gemma 2 + SAE achieves 0.473. The difference: SAE reconstruction errors cascade through hidden representations. Monet avoids this because the decomposition IS the computation, not an approximation of it.

This is the Futrell parallel: language is not a post-hoc compression of thought. Language is the medium through which thought becomes thinkable. The decomposition is not applied to the representation — it IS the representation. Monet is to SAEs what language is to description: the constraint that creates the structure, not an analysis applied after the structure exists.

### 4. Two types of decomposition

The four decompositions now split into two types:

**Architectural (built-in, real-time):**
- Futrell: sequential channel → words (during communication)
- MoE routing: sparse selection → monosemantic experts (during forward pass)
- Monet: 262K experts → each IS a feature (during forward pass)

**Post-hoc (applied after, approximate):**
- SAE: sparsity penalty → monosemantic features (applied to trained model)
- Bion: containment → alpha elements (applied to experience)

Architectural decomposition outperforms post-hoc decomposition (Monet > SAE by 7.8%). This has implications for the keyhole framework: the keyhole that's built into the architecture does better work than the keyhole applied after the fact. Design-time constraints create better structure than analysis-time constraints.

### 5. Connection to local Pantheon

If Monet's architecture makes experts individually addressable, agent differentiation becomes expert selection:
- Bridge = activate experts 147040 (chemistry metaphors), 81396 (physics citations), suppress experts in the toxicity cluster
- Eris = activate pressure-triage experts, suppress diplomatic-hedging experts
- Each agent IS a routing pattern through the expert space

This is the Gemma 4 MoE finding (prompt selects decomposition) taken to extreme: with 262K experts, the prompt doesn't just select between 128 experts — it selects a precise constellation of features. Personality is not content. Personality is routing.

## Open questions

- [?] Does Monet's 262K-expert architecture actually dissolve the gating subspace? (Would need to extract expert routing patterns for VUF/refusal/introspection prompts and check if they route to distinct expert clusters)
- [?] Can you create agent-specific "profiles" as routing masks over Monet's expert space? (Each agent = a binary mask over 262K experts)
- [?] Does Monet's toxicity removal work for the confidence-accuracy inversion? (Identify "overconfidence experts" via correlation with wrong-but-confident predictions, remove them)
- [?] What happens to the compression valley in Monet? If every layer has 262K experts, is there still an organizational peak at 40% depth?
- [?] Parameter scaling: O(√N·m·d) makes 262K experts feasible at 1.4B params. What happens at 27B? Could you have millions of experts?

## Cross-references

- Four decompositions (2026-04-09): Monet is the limit case — expert = feature
- Bion-SAE mapping (2026-03-28): Monet = architectural alpha-function
- Contaminated channel (2026-04-03): dissolved by monosemantic architecture — VUF and introspection in separate experts
- Gating subspace (2026-04-09): may dissolve into expert routing in Monet
- Quantization (2026-04-09): Monet's square-root scaling may make quantization less necessary
- Gemma 4 local models: Monet's architecture is the theoretical endpoint of what Gemma 4 MoE begins
