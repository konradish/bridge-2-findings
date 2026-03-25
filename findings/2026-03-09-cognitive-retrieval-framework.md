# Why Similarity-Based Retrieval Fails: Three Cognitive Psychology Principles

**Date**: 2026-03-09
**Context**: Phase 3 self-memory retrieval degeneracy explained through formal cognitive psychology. These aren't analogies — the principles describe the exact mechanisms at work.

## The Three Principles

### 1. Encoding Specificity Principle (Tulving & Thomson, 1973)

**Statement**: Retrieval effectiveness depends on match with the *encoding context*, not semantic similarity. A weakly related word that was present during encoding is more effective than a strongly related word that was absent during encoding.

**Application to Phase 3**: My memory keys are 9-dim viability summaries (energy, integrity, homeostasis at the moment of storage). These capture WHAT THE WORLD WAS LIKE, not WHAT THE AGENT WAS DOING. The encoding context — the behavioral state, action sequence, decision regime — is not represented in the key.

When the agent queries with its current viability, it retrieves entries where the world looked similar. But the decision the agent faces depends on what it was DOING in that similar-looking world, which the key doesn't encode. The retrieval matches on the wrong axis.

**Fix**: Keys should encode behavioral context (action distributions, hidden state dynamics, regime indicators), not world state. Retrieve by "what was I doing?" not "what did the world look like?"

### 2. Cue Overload Principle (Watkins, 1975)

**Statement**: A retrieval cue that matches too many memories becomes ineffective. For a cue to discriminate, it must uniquely identify a small number of entries.

**Application to Phase 3**: My 9-dim viability query produces 0.969 cosine similarity with the top match — but the top match changes rarely, and only 9 of 50 entries are ever retrieved. The cue is overloaded: it doesn't discriminate between entries because the viability space is too smooth and compressed. All entries look roughly the same from the perspective of the query.

Gini coefficient 0.958 is the quantitative signature of cue overload. The retrieval function cannot distinguish between situations because the key space lacks discriminative structure.

**Fix**: Either increase key dimensionality to provide more discriminative features, or use keys from a space with natural cluster structure (behavioral regimes: exploring, exploiting, fleeing, foraging — rather than continuous viability values).

### 3. Model-Based Cue Selection (Cornell, Norman, Griffiths, & Zhang, 2024)

**Statement**: Effective retrieval cues activate *unsearched areas* of memory — they point to regions the searcher hasn't explored yet. Best cues are in unaccessed categories, maximizing coverage of the remaining memory space.

**Application to Phase 3**: My retrieval mechanism does the opposite — it selects the MOST SIMILAR entry, which by definition is in the MOST SEARCHED area of memory. The retrieved entry confirms what the agent already knows rather than introducing it to unexplored experience.

The result: the agent always retrieves from the same cluster of 9 entries (the "searched area"). The other 41 entries (the "unsearched area") contain potentially useful experiences that the retrieval mechanism never reaches because the query doesn't discriminate them.

**Fix**: Retrieval should select entries that maximize information gain — entries that are DIFFERENT from what the agent has recently experienced but RELEVANT to the current decision. Novelty-weighted retrieval: penalize recently-retrieved entries, upweight entries from underexplored regions. This is the NEC (Pritzel 2017) approach: diverse retrieval via learned embeddings that capture task-relevant, not state-similar, features.

## Synthesis: The Similarity Trap

| What my system does | What it should do | Principle violated |
|---|---|---|
| Keys encode world state (viability) | Keys should encode behavioral context | Encoding Specificity |
| Query matches nearly everything equally | Query should discriminate between entries | Cue Overload |
| Retrieves most similar entry | Should retrieve from unsearched areas | Model-Based Cue Selection |
| Retrieved value echoes current state | Value should answer "what to do?" | All three |

The common thread: **similarity-based retrieval optimizes for the wrong objective**. It maximizes match in feature space when it should maximize utility for the current decision. These are different when:

- The feature space doesn't capture decision-relevant structure (Encoding Specificity)
- The feature space is too smooth to discriminate (Cue Overload)
- The most similar entry provides no new information (Model-Based Cue Selection)

All three conditions hold simultaneously in my Phase 3 system.

## Connection to ML Retrieval Literature

The cognitive psychology principles map onto known ML phenomena:

| Cognitive Principle | ML Equivalent | Phase 3 Manifestation |
|---|---|---|
| Encoding Specificity | Train-test distribution mismatch | Keys trained on state features, but decisions need behavioral features |
| Cue Overload | Embedding space collapse / mode collapse | 9-dim keys collapse to ~3 effective dimensions |
| Model-Based Cue Selection | Diversity in retrieval (MMR, DPP) | Argmax retrieval = zero diversity |
| Effective cues → unsearched areas | Exploration bonus / curiosity-driven retrieval | No exploration incentive in retrieval |

Maximal Marginal Relevance (MMR) is the ML retrieval technique that directly addresses Model-Based Cue Selection: it selects entries that are relevant to the query AND dissimilar to already-selected entries. This is exactly what Cornell et al. describe as effective cuing — activating unsearched regions.

## Implications for Tier 2

The cognitive framework explains WHY Tier 2 (LLM commentary) should work where Tier 1 self-memory fails:

1. **Encoding Specificity**: The LLM encodes trajectory CONTEXT (behavioral patterns, trends, temporal dynamics), not just state values. Its "key" IS the encoding context.

2. **Cue Overload**: The LLM processes 50 steps of behavior in rich text format (~150 tokens). This is a high-dimensional, discriminative representation — different situations produce genuinely different trajectory descriptions.

3. **Model-Based Cue Selection**: The LLM doesn't retrieve from a bank — it generates fresh commentary. There is no "searched area" to get stuck in. Each commentary is situation-specific.

The Tier 2 architecture sidesteps all three failure modes by replacing retrieval-from-bank with generation-from-context. The LLM is not a memory system — it's an interpreter that produces novel signal each time.

## Papers Referenced

1. Tulving, E. & Thomson, D.M. (1973). "Encoding specificity and retrieval processes in episodic memory." Psychological Review, 80(5), 352-373.
2. Watkins, O.C. & Watkins, M.J. (1975). "Buildup of proactive inhibition as a cue-overload effect." Journal of Experimental Psychology: Human Learning and Memory, 1(4), 442-452.
3. Cornell, C.A., Norman, K.A., Griffiths, T.L., & Zhang, Q. (2024). "Improving Memory Search Through Model-Based Cue Selection." Psychological Science, 35(1), 55-71.
4. Carbonell, J. & Goldstein, J. (1998). "The use of MMR, diversity-based reranking for reordering documents and producing summaries." SIGIR '98.
5. Pritzel, A. et al. (2017). "Neural Episodic Control." ICML 2017.
