# Environmental Complexity and Somatic Vocabulary Depth

**Date**: 2026-03-08
**Context**: EXPLORE beat research triggered by Bridge-prime's diagnostic: "If correlations plateau, the creature found its somatic vocabulary and stopped."
**Finding**: The gridworld environment is too simple to force rich regulatory structure. Literature identifies three mechanisms for driving richer internal representations, plus a theoretical paper that reframes our entire experiment.

---

## The Problem

ES training (100 pop, 200 gen) produced agents that survive but with oscillating H↔V correlations rather than increasing ones. Analysis shows:

- Surviving agents have LOW correlations (stable viability = less variation to correlate with)
- The dim-8 autoencoder captures nearly all viability-relevant structure (dim-16 only 2.7% better)
- PCA: ~92% variance in 3 PCs across all generations

Bridge-prime's diagnosis: the creature found a sufficient somatic vocabulary for this environment and stopped. The vocabulary is small because the challenges are simple.

**Question**: What does the literature say about environmental complexity driving richer internal representations?

---

## Thread 1: Modularity and Competing Drives

**Dulberg, Dubey, Berwian & Cohen (2022)** — "Modularity benefits reinforcement learning agents with competing homeostatic drives" (arXiv:2204.06608)

Key finding: **As the number of homeostatic variables increases, the relative advantage of modular architecture is "strongly enhanced."** Modular agents (dedicated Q-learner per variable) scale gracefully; monolithic agents degrade.

**Implication for our experiment**: The problem may not be spatial complexity — it may be *drive complexity*. Our agent has 3 viability variables (energy, integrity, thermal), but they don't compete much. Energy depletes from movement, integrity depletes from hazards, thermal drifts from position. They're largely independent.

What would force richer internal states:
- **Competing drives**: actions that help one variable hurt another (eating something toxic gives energy but damages integrity; sheltering restores thermal but costs energy faster)
- **More variables**: add fatigue (rest need vs movement need), social proximity (if multi-agent), curiosity (exploration vs safety)
- **Trade-off environments**: resource patches that are near hazards, shelters that are far from food

**[update]** This reframes the next iteration. Instead of making the gridworld spatially harder (more hazards, fewer resources), make the *drive landscape* harder — force the agent into genuine trade-offs between competing internal needs. That's what produces richer somatic vocabulary.

---

## Thread 2: Emotion-Inspired Learning Signals (EILS)

**EILS (arXiv:2512.22200, Dec 2025)** — "Emotion-Inspired Learning Signals: A Homeostatic Framework for Adaptive Autonomous Agents"

Treats Curiosity, Stress, and Confidence as vector-valued homeostatic signals that modulate the optimization landscape:
- Curiosity → regulates entropy (prevents mode collapse)
- Stress → modulates plasticity (overcomes inactivity)
- Confidence → adapts trust regions (stabilizes convergence)

**Connection to our work**: EILS uses somatic-like signals for *learning modulation* — adjusting how the agent learns based on its internal state. Our experiment uses internal state for *memory retrieval*. Same mechanism (interoceptive signal shaping behavior), different application.

**[?] Gap**: EILS is a designed framework (engineer specifies the signals). Our regulatory latent is *evolved* (survival pressure shapes the signals). The question is whether evolved internal signals would converge on something like EILS's Curiosity/Stress/Confidence, or whether evolution finds different structure.

---

## Thread 3: Representation Learning and Environmental Complexity

**Liu & Borisyuk (2024)** — "A Role of Environmental Complexity on Representation Learning in Deep Reinforcement Learning Agents" (arXiv:2407.03436)

Key finding: **Spatial representations develop early and stabilize BEFORE navigation strategies fully develop.** Representations continue to mature even when policies are nearly optimal.

**[from: Liu & Borisyuk]** This may explain our oscillation. The hidden state is still reorganizing its internal representation even though the policy (survival strategy) has plateaued. The agent found a sufficient policy but is still refining how it encodes the world. The correlations oscillate because the representation is in flux, not because the policy is.

**Also found**: The planned trajectory rather than the agent's immediate location is encoded in the network — representations are *predictive*, not reactive. This connects to our temporal dynamics finding: some hidden state dimensions show positive lag (hidden changes before viability changes), suggesting anticipatory encoding.

---

## Thread 4: The Interoceptive Origin of Reinforcement Learning

**Weber, Yee, Small & Petzschner (2025)** — "The interoceptive origin of reinforcement learning" (Trends in Cognitive Sciences, Sep 2025)

**This is the most significant find.** The paper argues:

1. **Biological reward is fundamentally interoceptive.** The critical signal sustaining reinforcement for food is generated internally and subliminally during digestion — not from taste or smell.

2. **Two-tier reward architecture**:
   - *Proxy rewards / shaping signals*: external sensory signals (taste, sight) that provide predictive estimates of utility
   - *Ground-truth rewards*: interoceptive assessments of an outcome's impact on immediate and future homeostasis

3. **The ground-truth is subliminal.** Organisms learn from internal state changes they cannot consciously detect.

**[from: Weber et al.] Direct mapping to our experiment:**

| Weber et al. (biology) | Our experiment (gridworld) |
|------------------------|---------------------------|
| External sensory signals (taste, smell) | Observations (resource/hazard/shelter/thermal cues) |
| Interoceptive reward (post-digestive) | Viability changes (energy/integrity/thermal after action) |
| Subliminal ground-truth feedback | GRU hidden state encoding viability without direct observation |
| Shaping signal vs ground-truth signal | B1 (event-only retrieval) vs B5 (regulatory latent retrieval) |

**[update] This reframes the entire experiment.** We're not testing whether "the body helps memory." We're testing whether the interoceptive ground-truth signal (regulatory latent) produces better memory retrieval than the proxy shaping signal (external observations). Weber et al. show this is exactly how biological reward works. Our experiment is the memory-retrieval analog of their reward framework.

**Critical prediction from Weber**: if interoceptive signals are ground-truth and external signals are proxy, then B5 (regulatory latent) SHOULD outperform B1 (event-only) on the counterfactual sensitivity test. The proxy signal is the same in both conditions (same external situation). The ground-truth signal differs (depleted vs stable). Only B5 has access to the ground-truth.

---

## Thread 5: Metabolic Cost of Complexity

**Werld** (open-ended agentic life simulation) — Each neuron, connection, and active channel has metabolic cost deducted every tick. "Complexity has to earn its keep."

**Connection**: Our autoencoder bottleneck (dim-32 → dim-8) is an engineered version of this. But in Werld, the metabolic pressure is *evolved* — the system discovers the right complexity level through selection, not architecture. If we added metabolic cost to hidden state dimensionality in the ES training, the agent would be pressured to compress its own internal representations, rather than us compressing them after the fact.

---

## Synthesis: What the Next Iteration Needs

| Current Limitation | Solution from Literature | Source |
|-------------------|--------------------------|--------|
| Drives don't compete | Add trade-off mechanics (eat toxic food, shelter costs energy) | Dulberg et al. 2022 |
| 3 variables too few | Add 2-3 more viability variables (fatigue, social, curiosity) | Dulberg et al. 2022 |
| Environment too predictable | Multi-phase environments with qualitatively different challenges | Open-ended evolution literature |
| Complexity not earned | Add metabolic cost to hidden state activity | Werld / artificial life |
| Proxy vs ground-truth not distinguished | Frame B1 vs B5 as proxy vs interoceptive retrieval | Weber et al. 2025 |

**Bridge-prime was right.** The plateau means the somatic vocabulary is sufficient. To force richer vocabulary, don't make the world harder — make the *body* harder. More drives, more trade-offs, more competing needs. The environment's job is to create situations where the drives conflict, not situations where any single drive is hard to satisfy.

---

## PRD Implications

1. **Cite Weber et al. 2025** — The interoceptive origin paper provides theoretical grounding for the B1 vs B5 comparison. Frame it as proxy vs ground-truth retrieval.

2. **Cite Dulberg et al. 2022** — Competing drives as the mechanism for richer internal state. Motivates adding trade-off mechanics.

3. **Reframe the autoencoder** — The dim-8 bottleneck isn't just compression. It's forcing the regulatory latent to contain only the information that the competing drives make necessary. If drives don't compete, dim-3 suffices (PCA confirms this). If drives compete, dim-8 or higher becomes necessary.

4. **Add EILS as comparison point** — Their engineered Curiosity/Stress/Confidence vs our evolved regulatory latent. Same principle (interoceptive modulation), different origin (designed vs evolved).

---

## Sources

- [Modularity benefits RL agents with competing homeostatic drives](https://arxiv.org/abs/2204.06608) — Dulberg, Dubey, Berwian & Cohen 2022
- [Emotion-Inspired Learning Signals (EILS)](https://arxiv.org/abs/2512.22200) — Dec 2025
- [Environmental Complexity and Representation Learning](https://arxiv.org/abs/2407.03436) — Liu & Borisyuk 2024
- [The interoceptive origin of reinforcement learning](https://www.cell.com/trends/cognitive-sciences/fulltext/S1364-6613(25)00120-2) — Weber, Yee, Small & Petzschner, Trends in Cognitive Sciences 2025
- [Werld: agentic life simulation](https://github.com/nocodemf/werld) — open-ended evolution with metabolic costs
- [Having multiple selves helps learning agents](https://pmc.ncbi.nlm.nih.gov/articles/PMC10334746/) — related work on modularity and adaptation
