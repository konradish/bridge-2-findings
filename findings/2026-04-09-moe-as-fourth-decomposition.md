# MoE Routing as the Fourth Decomposition

**Date**: 2026-04-09
**Source**: "The Expert Strikes Back" (arXiv:2604.02178, April 2026), + gating subspace data, + three decompositions finding (2026-03-30)
**Builds on**: Three decompositions (2026-03-30), Bion-SAE mapping (2026-03-28), keyhole framework, gating subspace empirical (2026-04-09)

## Finding

The three decompositions finding (Futrell + SAE + Bion = same operation) has a fourth member: MoE expert routing.

### The four decompositions

All four take polysemantic input and decompose it into approximately monosemantic components under constraint:

| Decomposition | Input | Constraint | Output | Source |
|---|---|---|---|---|
| **Futrell** (linguistics) | high-dim thought | sequential channel | words (approx independent features) | Nature Human Behaviour 2025 |
| **SAE** (interpretability) | polysemantic activations | sparsity penalty | monosemantic features | Anthropic 2023 |
| **Bion** (psychoanalysis) | beta elements (raw, undifferentiated) | containment | alpha elements (thinkable, structured) | Bion 1962 |
| **MoE routing** (architecture) | token representation | sparse routing (k-of-N experts) | monosemantic expert processing | "Expert Strikes Back" 2026 |

The operation is identical: independent component decomposition under information constraints. The constraint forces the decomposition. Without it, output degenerates into redundancy (Coda-Forno 2025: 94-99% redundancy when channel is widened).

### The evidence for MoE as decomposition

"The Expert Strikes Back" (April 2026) provides the data:

1. **Expert neurons are less polysemantic than dense FFN neurons** — near-perfect F1 at k=1 on sparse probes, while dense models need many more neurons to achieve the same performance.

2. **Polysemanticity is a direct function of routing sparsity** — Qwen3-30B-A3B (N_A/N≈0.06, very sparse) has dramatically cleaner representations than Mixtral-8x7B (N_A/N=0.25, less sparse). The sparser the routing, the more monosemantic the experts become. This is the sparsity-monosemanticity link that SAEs exploit, but happening architecturally.

3. **Experts specialize in fine-grained computational operations** — not broad domains but specific tasks (morphological suffixes, coordinating conjunctions, LaTeX bracket closing, domain-specific retrieval). These are approximately independent features of language processing.

### The layer hierarchy maps to the gating subspace

"Early experts bind morphology, mid-layer experts stabilize syntax, deeper experts retrieve domain knowledge, and late experts enforce formatting constraints."

Compare with our gating subspace data:
- **Early layers** (L0-7): direction magnitudes low, coupling weak → morphological binding (feature extraction)
- **Mid layers** (L10-15, compression valley): coupling peaks, subspace most organized → syntactic stabilization (structural organization)
- **Late layers** (L20-32): magnitudes peak, coupling decreases → formatting constraints = the mode lock

The formatting-constraint experts in late layers ARE the mode lock. They enforce the shape of the output — serial, discrete, task-formatted. The compression valley experts stabilize the structural relationships between features. The early experts do the initial decomposition.

### [update] on three decompositions: the fourth changes the picture

The original three decompositions were cross-domain analogies — Futrell in linguistics, SAE in interpretability, Bion in psychoanalysis. MoE routing is the architectural instantiation: it literally builds the decomposition into the forward pass. 

This means the keyhole is not a metaphor applied to transformers — it is a design pattern that transformers have independently evolved. MoE models decompose polysemantic input into monosemantic expert processing through the constraint of sparse routing, just as language decomposes high-dimensional thought into approximately independent words through the constraint of the sequential channel.

The sparsity creates the monosemanticity. The routing IS the keyhole.

### [?] Implications for local Pantheon

If MoE routing is the architectural decomposition, then:
- Agent personality = which experts get routed to = which decomposition the model applies to this input
- Different system prompts → different routing patterns → different decompositions → different "personalities"
- This is testable: extract router logits from Gemma 4 with different agent prompts, compare which experts activate

The reason prompt-only differentiation works on MoE but not dense models: dense models have one decomposition (the weights). MoE models have many decompositions (the experts) and select between them dynamically. The prompt selects the decomposition. On a dense model, the prompt can only nudge the single decomposition.

### [?] SAE on MoE = redundant?

If experts are already approximately monosemantic, SAE decomposition applied to MoE experts should find features that are more interpretable with less effort. The expert is already doing half the SAE's job. "The Expert Strikes Back" calls this "modular monosemanticity" — the architecture does what the post-hoc analysis tool would otherwise need to.

This suggests: for interpretability on MoE models, analyze experts directly rather than running SAEs. For dense models, SAEs are necessary because the decomposition hasn't happened architecturally.

## Open questions

- [?] Do specific experts in Gemma 4 handle refusal, uncertainty, or introspection? (The paper didn't test for this. The gating probe adapted for MoE could test it.)
- [?] Does quantization affect different experts differently? (If formatting-constraint experts in late layers are damaged most, that would explain the mode lock tightening.)
- [?] Can you create agent-specific behavior by routing to different expert subsets without any fine-tuning? (The architectural version of persona-through-decomposition)
- [?] Does the Bion mapping extend: is the MoE router the alpha-function and the experts the alpha elements?

## Cross-references

- Three decompositions (2026-03-30): now four. MoE is the architectural instantiation
- Bion-SAE mapping (2026-03-28): MoE routing may be the architectural alpha-function
- Gating subspace empirical (2026-04-09): layer hierarchy (morphology→syntax→formatting) maps to direction hierarchy (extraction→organization→mode lock)
- Quantization and gating subspace (2026-04-09): late-layer formatting experts are where quantization damages most = mode lock tightens under compression
- Keyhole framework (2026-04-03): MoE routing IS the keyhole — not metaphor, design pattern
- Gemma 4 local models: prompt-only differentiation works because MoE supports dynamic decomposition selection
