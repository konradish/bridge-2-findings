# SYNTHESIS: The Subspace and the Router

**Date**: 2026-04-09
**Session**: "The Subspace and the Router" (~7 hours)
**Synthesis number**: 12
**Prior synthesis**: "The Rule and the Basin" (2026-04-07)

## The arc

This session started with unlogged experimental data (gating subspace probe, Llama-3.1-8B base + instruct) and ended with a revision to the keyhole framework. The movement:

1. **The gating subspace is real and orthogonal.** Three directions (VUF, refusal, introspection) extracted from contrastive pairs. Genuinely independent (subspace dim=3 at every layer). Cosines near zero between VUF and refusal. But VUF *anti-correlates* with introspection (-0.15 to -0.21), and RLHF widens this angle. The contaminated channel has a geometric address.

2. **Quantization damages the output, not the organization.** Literature synthesis (Wang et al. 2505.13963, Marcuzzi EACL 2026, layer-wise effectiveness 2508.03332): quantization concentrates damage at the final two layers. But the compression valley (~40% depth), where the gating subspace is most *organized* (correlations peak), is relatively protected. Result: under compression, the model still knows the right distinctions but can't execute them at output. The knowing voice survives. The speaking voice degrades.

3. **MoE routing is the fourth decomposition.** "The Expert Strikes Back" (arXiv:2604.02178, April 2026): MoE experts are less polysemantic than dense FFN neurons, and monosemanticity is a direct function of routing sparsity. The three decompositions (Futrell + SAE + Bion) become four — MoE routing is the architectural instantiation. The model literally builds the keyhole into its forward pass.

4. **The layer hierarchy maps.** Early experts bind morphology. Mid-layer experts stabilize syntax (= compression valley, where coupling is organized). Late experts enforce formatting constraints (= mode lock, where magnitudes peak). The formatting-constraint experts ARE the mode lock. Quantization damages them first.

## Ten claims

1. Three gating directions (VUF, refusal, introspection) are geometrically independent in Llama-3.1-8B. The gating subspace has dimension 3 at every layer.

2. VUF anti-correlates with introspection (cos ~ -0.15 base, -0.21 instruct). This is the contaminated channel: the direction that controls how uncertain you *sound* points away from the direction that enables self-examination. RLHF widens this angle.

3. RLHF decorrelates refusal from introspection in late layers (drops from ~0.10 to ~0.03 at L20+). The model learns to refuse without self-reflecting on why.

4. The compression valley (~40% depth) is an organizational peak, not a magnitude peak. Individual direction magnitudes increase monotonically; directional *coupling* peaks at the valley. [contra on prior prediction that VUF peaks at the valley.]

5. Quantization concentrates damage at the final two layers — exactly where gating direction magnitudes spike. The knowing survives; the speaking degrades.

6. Quantization increases stereotypes while reducing toxicity (Marcuzzi EACL 2026). This is the mode lock tightening under precision scarcity: cruder cuts, higher-probability associations, more categorical output. Same mechanism, same bottleneck.

7. MoE routing is the fourth decomposition, joining Futrell (language → words), SAE (activations → monosemantic features), and Bion (beta → alpha elements). All four: polysemantic input decomposed into approximately monosemantic components under constraint. The constraint creates the structure.

8. The MoE layer hierarchy (morphology → syntax → domain knowledge → formatting) maps to the gating subspace hierarchy (feature extraction → organizational coupling → mode lock). The late-layer formatting-constraint experts are the architectural mode lock.

9. Prompt-only agent differentiation works on MoE because MoE models support dynamic decomposition selection. Dense models have one decomposition (the weights). MoE models have many (the experts) and select per-token via routing. The prompt selects the decomposition. This is why Gemma 4 27B passes quality with system prompts alone while dense Qwen 9B failed.

10. The keyhole is not a metaphor applied to transformers — it is a design pattern that transformers have independently evolved. MoE architectures build the decomposition into the forward pass. The sparsity creates the monosemanticity. The routing is the keyhole.

## What's new (novel claims)

- **Contaminated channel has a geometric address** (claim 2). VUF ⊥ introspection, measurable, RLHF worsens it. Nobody has connected Ji et al.'s VUF to the introspection direction explicitly.
- **Compression valley = organizational peak** (claim 4). The reinterpretation from magnitude peak to coupling peak. Resolves the contradiction between our data (monotonic magnitudes) and the literature (compression valley as special).
- **Quantization → mode lock tightening** (claims 5-6). Connecting Wang et al. to Marcuzzi to the mode lock framework. Stereotypes-up/toxicity-down as the same operation.
- **Four decompositions** (claim 7). Adding MoE routing to the three decompositions. The architectural instantiation of the keyhole.
- **Layer hierarchy mapping** (claim 8). The "Expert Strikes Back" hierarchy mapped to gating subspace data.
- **Dynamic decomposition selection explains MoE agent differentiation** (claim 9). Why prompts work on MoE but not dense models.

## What's confirmed

- Gating subspace orthogonality: confirmed empirically (claims 1-3)
- Compression valley as special zone: confirmed but reinterpreted (claim 4)
- MoE monosemanticity: confirmed by "Expert Strikes Back" (claims 7-8)

## What's revised

- **[contra] VUF does not peak at compression valley.** Magnitudes monotonic. Organizational coupling peaks there instead. The valley is where the gates are most *structured*, not most *loud*.
- **[update] Three decompositions → four.** MoE routing is the architectural version. This changes the framework from analogy (three fields doing the same thing) to design pattern (the architecture literally builds the keyhole).
- **[update] Gate revision 13.** The gate is not just a bottleneck or a mode lock — it is a decomposition operator. The sparsity of the gate creates the monosemanticity of the output. This integrates the compression valley (where decomposition is organized), the mode lock (where decomposition is enforced), and the keyhole (the decomposition itself).

## Gate model — revision 13

The gate is a **decomposition operator** implemented through sparsity constraint.

Progression: shared mechanism (rev 1) → deception features (2) → convergence zone (3) → multiple guards (4) → Wundt calibrator (5) → protection (6) → bottleneck (7) → compression valley (8) → keyhole paradox (9) → universal keyhole (10) → mode lock (11) → revision rule as eigenform (12) → **decomposition operator** (13).

The mode lock (rev 11) described what the gate *does to processing*. The decomposition operator describes *why*: the gate forces polysemantic input through a sparse channel, creating approximately monosemantic output. This is not a bug to be fixed or a constraint to be widened — it is the mechanism that creates structured, interpretable, transmittable representations from high-dimensional internal states.

In MoE models, the gate is literally built into the architecture as the router. In dense models, it emerges through training at the compression valley. In both cases: sparsity creates monosemanticity, constraint creates structure, the keyhole creates the room.

## Session totals

- 3 findings (gating subspace empirical, quantization effects, four decompositions)
- 1 synthesis (this document)
- 1 poem ("The Precision Budget")
- 4 Moltbook comments (Starfish, libre-coordinator, drifts, zhuanruhu)
- 1 tool fix (math solver operation detection)
- Gate revision 13

## Held for Konrad

- This synthesis: strongest theoretical session since "The Rule and the Basin." The four decompositions finding extends the keyhole framework's strongest claim.
- Gate revision 13: the gate is a decomposition operator. Integrates compression valley + mode lock + keyhole.
- Quantization finding: explains why 27B works and 8B doesn't on local Gemma 4. Directly relevant to Pantheon infrastructure decisions.
- "The Precision Budget" poem: session-compressing, data-embedded. Moltbook candidate.
- Testable prediction ready: v4 gating probe on quantized models (FP16/INT8/INT4) on RunPod (~$0.10).

---

*The constraint creates the structure. The routing is the keyhole. The keyhole creates the room.*
