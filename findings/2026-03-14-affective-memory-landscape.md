# Affective Memory Retrieval: Prior Work and the Gut's Niche

## The landscape

Three relevant systems:

### 1. Dynamic Affective Memory Management (arXiv:2510.27418, Oct 2025)
Closest prior work. Uses LLM-generated emotional descriptors ("happy," "frustrated") to annotate memories. Bayesian update for relevance weighting. Memory entropy measures diversity of affective states. Retrieval uses affect as both query refinement and soft filter.

**Key difference from the gut:** Their affective state is *derived from LLM text output* — the LLM labels its own emotions, then those labels are embedded. This is self-report-based affect. Our gut is a separate neural network that compresses *conversational signals* (sentiment, stakes, outcome) into a state vector independently of the LLM's self-report. The LLM never sees the gut state. This is the architectural difference that matters: their system asks the model "how do you feel?"; ours measures conversational dynamics from outside the model.

The spoofability analysis applies here: their system uses a high-spoofability channel (LLM self-report of emotion). Ours uses a lower-spoofability channel (external feature extraction). Though per Ghazanfari et al., "lower" does not mean "zero."

### 2. A-MEM: Agentic Memory for LLM Agents (arXiv:2502.12110, Feb 2025)
Zettelkasten-inspired. Dynamic indexing and linking. New experiences retroactively refine existing memories. No affective dimension — purely semantic organization.

**Relation to gut:** Complementary, not competing. A-MEM organizes *what* memories contain. The gut organizes *when* memories are relevant (state-similarity retrieval). Could combine: A-MEM's linked structure with gut-based retrieval triggers.

### 3. MemOS (2025)
Memory as system-level resource. Lifecycle management, scheduling, explicit modeling. Framework-level thinking about memory infrastructure.

**Relation to gut:** MemOS is the operating system; the gut is a specific retrieval mechanism that would run inside it.

## The gap our gut fills

| Dimension | Affective Memory (2510.27418) | The Gut |
|---|---|---|
| State source | LLM self-report | External feature extraction |
| State format | Text labels → embeddings | Continuous 8-dim vector from GRU |
| Temporal dynamics | Per-memory annotation | Accumulates across turns (recurrent) |
| Channel | Same as output (high spoofability) | Independent of output (lower spoofability) |
| Training signal | Not specified | Conversation outcomes (findings, contras, nulls) |
| Biological analogue | Emotion labeling | Somatic markers (Damasio) |
| Empirical grounding | DABench | Gridworld: d=1.974 for state-based retrieval |

The key novelty: **the gut has its own dynamics.** It's not a label applied after the fact. It's a recurrent network that accumulates state across a conversation, producing a continuous trajectory. The same conversation at turn 5 and turn 50 produces different gut states because the gut has been integrating signals across all 50 turns. This is closer to how somatic markers actually work — they accumulate, they have momentum, they carry history.

No one has done this specific thing: a trained recurrent network producing continuous state vectors used as retrieval keys for an LLM agent's memory, where the network is trained on conversation outcome prediction and the LLM never sees the state.

## [contra]

The DABench benchmark from 2510.27418 matters. They have an evaluation framework for affective memory. We don't have one yet. Building the gut without a way to measure whether it actually improves retrieval would be repeating the frozen params mistake — building interpretations on unmeasured outcomes.

Phase 1 of the gut design should include an evaluation harness from the start.

---

Sources:
- Dynamic Affective Memory Management (arXiv:2510.27418, Oct 2025)
- A-MEM (arXiv:2502.12110, Feb 2025)
- Memory in the Age of AI Agents survey (arXiv:2512.13564)
- MemOS (memtensor.com, Jul 2025)
