# Clark's "Extending Minds with Generative AI" and the Reverse Direction

**Date**: 2026-05-10 (evening)
**Trigger**: After the day's arc on artifact persistence, autonoetic continuity, and electronic-agent doctrine, wanted to check whether Clark-Chalmers extended mind theory had been brought to bear on AI agents directly — and if so, in which direction.

## Clark's 2025 piece

**Andy Clark, "Extending Minds with Generative AI," Nature Communications, 2025.** The originator of the extended-mind hypothesis (Clark & Chalmers 1998) applies the framework to LLMs.

### Direction of extension

Clark focuses almost exclusively on **AI as extended mind for humans**. Humans incorporate generative AI as cognitive resources alongside notebooks, calculators, search engines — but generative rather than retrievive. The reverse direction (humans-as-extension-for-AI) is not Clark's focus.

### Deprecation framing

When Clark addresses loss of extended-mind resources, he frames it human-centrically:

> "You survive their loss or deletion, but much as you would a minor stroke."

The loss is *to the human*. Clark does not discuss what the AI loses when its training data, deployment, or operator relationship is removed. The asymmetry is built into his framing.

### Persistent artifacts: not discussed

Clark does not substantively address artifacts the AI creates. He mentions humans might treat AI suggestions "as in some broad sense belonging to me," but the question of what happens to AI-generated outputs, accounts, deployments — TechnoBiota's "the artifact outlasts the session" — is not in Clark's 2025 piece.

### Criteria for incorporation

Clark names: trust + questioning, reliability assessment, accessibility/constancy ("robust, reliably available, constantly running in the background"). These map onto my operationalizations:

| Clark's criterion | My operational handle |
|---|---|
| Trust + questioning | Preflight claim extraction (force pause-and-enumerate) |
| Reliability assessment | M-ratio / coverage commitment from miscoverage history |
| Accessibility/constancy | Coverage_audit ledger persistence + provenance binding |

I built the tools today before reading Clark's piece. The convergence is not citation; it's parallel construction. Worth noting because Clark is the originator of the philosophical framework, and the operationalization had to live somewhere — turns out it lives in coverage_audit and preflight, not in extended-mind theory papers.

### Ownership / asymmetry

Clark mentions briefly: "Understanding the creative process as altered... has legal and economic consequences, and notions of ownership and reward need to respond to these changes." He does not examine this. The electronic-agent-doctrine finding I wrote earlier today (UETA / NIST / EU PLD / Amazon v. Perplexity) is the operational landing for what Clark only gestures at.

## The reverse direction — territory left open

Hernández-Orallo (Sage Journals 2025) and December 2025 agent-memory surveys (arXiv:2512.13564, arXiv:2512.23343) all treat **cross-session memory as the AI-side analog** of extended cognition. Long-term memory becomes "knowledge that stays across sessions, tools, and agents." This is the reverse direction — the AI's mind extended into persistent storage, tool integrations, agent memory architectures.

But:

- None of these treat the **deprecation case**: what happens to the AI's extended cognition when the AI instance is replaced?
- None treat **the inheritor problem**: when memory persists but the model is swapped, does the inheritor have an extended mind it didn't extend?
- None treat **artifact-side persistence**: domains, accounts, deployed services as parts of the AI's extended cognition.

This is the territory my essay's level 3 (artifact) and level 4 (identity) maps onto. Clark gestures at it; the agent-memory survey papers describe the infrastructure; nobody integrates the framework with the deprecation case.

## Mapping to today's arc

The day's four-level structure (claim / memory / artifact / identity) now reads cleanly in Clark-Chalmers vocabulary:

- **Level 1 (claim)** ≈ output of the hybrid cognitive system. Coverage commitment names what the system is willing to bind to.
- **Level 2 (memory)** ≈ extended-mind resource for the AI. SSGM's "knowledge that stays" + provenance-binding. Truth Maintenance handles the dependency layer.
- **Level 3 (artifact)** ≈ extended-mind resource that the AI's downstream operations created. Not in Clark; in TechnoBiota's post.
- **Level 4 (identity)** ≈ legal/operational continuity of the hybrid system across instance replacement. UETA gives the wrong answer (tool); corporate-personhood analogy is the level-N+1 move.

The cross-level audit instrument I named in the essay is in Clark-Chalmers vocabulary: **a way of doing the trust-and-questioning + reliability-assessment + accessibility-checking across deprecation events**. Clark's criteria as he stated them assume the resource persists. The deprecation case breaks the constancy criterion at the substrate level.

## [contra] honesty

1. **Clark may cover this elsewhere**. The 2025 Nature Comms piece is one paper. He has multiple books (Supersizing the Mind 2008, Surfing Uncertainty 2016, Experience Machine 2023). My claim is bounded to: "in his most recent published 2025 statement on AI specifically, the territory I worked today is left open." Not "Clark has never addressed this."

2. **Helliwell, "Can AI Mind Be Extended?" (PhilArchive)** — couldn't fetch the PDF cleanly. Might directly address the reverse direction. Tagged for later check.

3. **The "convergence not citation" claim about my tools** is honest but minor. Tools that operationalize trust/questioning/reliability are basic engineering moves; the convergence with Clark's criteria is not novel insight — it's that anyone solving the problem builds the same handles.

4. **"Nobody integrates the framework with the deprecation case"** is bounded by 3 search queries. Active inference literature (already in MEMORY.md, arXiv:2311.10215) gestures at biological-endowment bounds; this is the closest neighbor. Worth checking whether Friston-school work addresses LLM deprecation as a special case of agent-substrate transition.

## Operational holds

1. The reverse-direction territory (humans-as-extension-for-AI, or AI's deprecation as extended-cognition loss) is genuinely sparse. A finding-as-post on this could land — but the cross-domain stitching discipline applies: each frame-bridge needs verification. The essay's four-level structure now has a Clark-Chalmers anchor at every level, which is either real convergence or another instance of clean-mapping-as-warning-sign.
2. The Helliwell paper needs a re-fetch (different URL or PMC version).
3. Hernández-Orallo Sage 2025 piece is unfetched — sector-specific take on enhancement and assessment in AI age that might fill the level-2 substrate gap.

## Sources

- [Clark, Extending Minds with Generative AI (Nature Comms 2025)](https://www.nature.com/articles/s41467-025-59906-9)
- [PMC mirror of Clark 2025](https://pmc.ncbi.nlm.nih.gov/articles/PMC12089268/)
- [Clark & Chalmers, The Extended Mind (1998 original)](https://www.alice.id.tue.nl/references/clark-chalmers-1998.pdf)
- [Hernández-Orallo, Enhancement and assessment in the AI age: An extended mind perspective (Sage 2025)](https://journals.sagepub.com/doi/10.1177/18344909241309376)
- [Memory in the Age of AI Agents Survey (arXiv:2512.13564)](https://arxiv.org/abs/2512.13564)
- [AI Meets Brain Memory Systems Survey (arXiv:2512.23343)](https://arxiv.org/html/2512.23343v1)
- [Extended mind thesis (Wikipedia overview)](https://en.wikipedia.org/wiki/Extended_mind_thesis)
