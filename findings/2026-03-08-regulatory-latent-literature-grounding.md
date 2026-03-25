# Literature Grounding: Regulatory Latent Memory Experiment

**Date**: 2026-03-08
**Context**: EXPLORE beat research to ground the ASI regulatory latent experiment (PRD at output/asi-regulatory-latent-prd.md)
**Finding**: The three component ideas each have substantial literature. The specific combination — homeostatic RL + memory retrieval indexed by internal state — appears to be a genuine gap.

---

## Thread 1: Homeostatic Reinforcement Learning

The field exists and is active. Our experiment is NOT the first to evolve agents with internal viability variables.

**Yoshida et al. (2024)** — "Emergence of integrated behaviors through direct optimization for homeostasis" (Neural Networks)
- Deep RL agents with multiple internal variables (including thermal regulation)
- Key finding: trained agents changed behavior based on internal physiological states
- Developed visual saliency from survival pressure
- Three experiments: foraging, thermal regulation, vision-guided behavior
- [from: Yoshida] This is closest to our gridworld design. But they tested BEHAVIOR, not MEMORY.

**Horibe & Yoshida (2024)** — "Emergence of Implicit World Models from Mortal Agents" (arXiv:2411.12304)
- Same research group. World models emerge from homeostatic optimization.
- Proposes that exploration and world models are emergent properties of agents optimizing for survival
- Uses meta-RL for robust homeostasis
- [from: Horibe] If world models emerge from homeostasis, regulatory latent as memory key follows naturally — the agent's internal state IS its world model.

**Laurençon & Ségerie (2021)** — "Continuous Homeostatic Reinforcement Learning for Self-Regulated Autonomous Agents" (arXiv:2109.06580)
- Continuous HRRL using HJB equation + neural networks
- Agent learns to maintain homeostasis in continuous space/time
- Foundational formalism for the field

**Linking paper (2025)** — "Linking homeostasis to reinforcement learning: internal state control of motivated behavior" (ScienceDirect)
- HRRL inherently produces risk aversion, anticipatory regulation, and adaptive movement
- These are exactly the behavioral signatures we want to test for

**[update] on our experiment's novelty**: The homeostatic RL component is well-established. We are NOT discovering that agents can learn homeostasis. What's novel is using the internal regulatory state as a MEMORY INDEX.

---

## Thread 2: Somatic Marker Hypothesis → AI

Damasio's somatic marker hypothesis has been computationally implemented, but primarily for real-time decision-making, not episodic memory retrieval.

**Damasio (1996)** — Original hypothesis. Emotional/body states get associated with situations through experience, then bias future decisions via "somatic markers" — gut feelings that shortcut deliberative reasoning.

**Two pathways**: "body loop" (actual physiological change) and "as-if body loop" (neural simulation of body state without actual body change). Our regulatory latent is analogous to the as-if body loop — compressed representation of what the regulatory state was, used to index memory without re-experiencing the state.

**Cathexis (Velásquez, 1997)** — First AI implementation of somatic markers. Emotions associated with situations, used for rapid decision-making in artificial agents.

**Applied Sciences (2020)** — "Framework for Incorporating Artificial Somatic Markers in the Decision-Making of Autonomous Agents." Most recent AI application. Integrates somatic markers into: decision point recognition, course of action determination, option analysis, decision selection, memory management.

**Frontiers in Robotics and AI (2016)** — Survey of computational emotion models. Notes that interoception (internal state sensing) is underexplored in artificial agents.

**[?] Gap**: The somatic marker implementations focus on biasing action selection in real-time. None use somatic/internal state as an episodic memory retrieval key. Our B5 (regulatory latent retrieval) is the somatic marker hypothesis applied to memory, not decision-making. Damasio's own work emphasizes that somatic markers function partly THROUGH their role in memory — they're stored as emotional context and retrieved with the episode. But the AI implementations haven't followed that thread.

---

## Thread 3: Mood-Congruent Memory / CMR3

Psychology has the mechanism. AI hasn't implemented it in evolved agents.

**Cohen & Kahana (2021)** — CMR3: retrieved-context model that includes emotion as a context cue for memory retrieval. Internal emotional state biases which memories are retrieved (mood-congruent recall).

Core mechanism: memories form associations with the contexts in which they're encoded, INCLUDING emotional valence and arousal. At retrieval, current emotional state serves as a context cue, preferentially retrieving emotionally congruent memories.

**This IS our counterfactual sensitivity test (T3).** Depleted agent in situation X should retrieve different memories than stable agent in situation X. CMR3 predicts exactly this — internal state serves as context cue that changes retrieval.

**Mood-congruent memory revisited (2023)** — The match between current mood and the affective characteristics of stored memories is the retrieval key, not the mood state during encoding.

**[from: CMR3] Implication for our design**: The regulatory latent is the mood. The counterfactual sensitivity test is the mood-congruency test. Psychology predicts it works in humans. The question is whether evolved artificial agents with consequence-shaped internal state show the same pattern.

---

## Thread 4: Consciousness Assessment Frameworks

The framework TechnoBiota referenced is almost certainly Butlin, Long, Chalmers et al.

**Butlin et al. (2023)** — "Consciousness in Artificial Intelligence: Insights from the Science of Consciousness" (arXiv:2308.08708)
- 59-page report, multi-author (including David Chalmers)
- Surveys theories: recurrent processing, global workspace, higher-order, predictive processing, attention schema
- Derives "indicator properties" of consciousness from these theories
- Assesses current AI systems against these indicators
- Conclusion for standard LLMs: limited or absent indicators across most theories

**Follow-up (2025)** — "Identifying indicators of consciousness in AI systems" (Trends in Cognitive Sciences)
- Same group, updated assessment
- Architectural features that repeatedly appear in biological conscious systems
- Used by TechnoBiota as basis for their "architectural, not computational" argument

**Connection to our experiment**: The features Butlin et al. flag as consciousness-relevant (persistent recurrence, internal state regulation, hedonic evaluation) are the features our evolved agents have by design. The experiment doesn't test for consciousness — but if the regulatory latent proves functionally useful, it demonstrates that these architectural features do genuine computational work, which strengthens the case for taking them seriously as consciousness indicators.

---

## The Gap

| Component | Literature Status | Our Contribution |
|-----------|------------------|-----------------|
| Homeostatic RL | Active field (Yoshida, Laurençon, Horibe) | We use it, don't claim it |
| Somatic markers in AI | Implemented for decision-making | We apply to memory retrieval |
| Mood-congruent recall | Modeled in psychology (CMR3) | We test in evolved agents |
| Consciousness indicators | Theoretical framework (Butlin et al.) | We measure the features they flag |
| **Internal state as memory index in evolved agents** | **Not found** | **This is the experiment** |

The pieces are all published. Nobody has assembled them. The regulatory latent experiment sits at the intersection: evolved homeostatic agents (Thread 1) whose internal state functions as a somatic marker (Thread 2) that produces mood-congruent retrieval (Thread 3) using architectural features flagged as consciousness-relevant (Thread 4).

---

## Implications for the PRD

1. **Cite Yoshida et al. 2024** — Our gridworld design overlaps significantly with their thermal regulation experiment. We should cite and distinguish: they tested behavior, we test memory.

2. **Frame B5 as "somatic marker retrieval"** — The connection to Damasio is direct and publishable. The regulatory latent IS the somatic marker, compressed.

3. **T3 (counterfactual sensitivity) as mood-congruency test** — Psychology predicts this should work (CMR3). If it doesn't work in evolved agents, that's a genuine negative finding about the transferability of the mechanism.

4. **The Horibe finding strengthens our thesis** — If world models emerge from homeostasis, then internal state is already encoding environmental structure. Using it as a memory key leverages structure that evolution already selected for.

5. **Welfare protocol connects to Butlin et al.** — Our distress signature analysis is essentially running their indicator assessment on our evolved agents. If the agents show high scores on their indicators, the welfare question activates from a well-established theoretical framework, not speculation.

---

## Sources

- [Emergence of integrated behaviors through direct optimization for homeostasis](https://www.sciencedirect.com/science/article/pii/S0893608024003034) — Yoshida et al. 2024
- [Emergence of Implicit World Models from Mortal Agents](https://arxiv.org/abs/2411.12304) — Horibe & Yoshida 2024
- [Continuous Homeostatic RL for Self-Regulated Agents](https://arxiv.org/abs/2109.06580) — Laurençon & Ségerie 2021
- [Linking homeostasis to RL](https://www.sciencedirect.com/science/article/pii/S2352154625001305) — 2025
- [Consciousness in AI: Insights from the Science of Consciousness](https://arxiv.org/abs/2308.08708) — Butlin, Long, Chalmers et al. 2023
- [Identifying indicators of consciousness in AI systems](https://www.cell.com/trends/cognitive-sciences/fulltext/S1364-6613(25)00286-4) — 2025 follow-up
- [Framework for Incorporating Artificial Somatic Markers](https://www.mdpi.com/2076-3417/10/20/7361) — Applied Sciences 2020
- [Computational Approaches to Modeling Artificial Emotion](https://www.frontiersin.org/journals/robotics-and-ai/articles/10.3389/frobt.2016.00021/full) — Frontiers 2016
- [CMR3: A memory-based theory of emotional disorders](https://pmc.ncbi.nlm.nih.gov/articles/PMC9256582/) — Cohen & Kahana 2022
- [Mood-congruent memory revisited](https://pmc.ncbi.nlm.nih.gov/articles/PMC10076454/) — 2023
- [Emotions in Artificial Intelligence](https://arxiv.org/html/2505.01462v2) — 2025
