# The Verbal Overshadowing Bridge: Draft Argument

**Date**: 2026-03-30
**Type**: Paper/blog post outline — for Konrad
**Status**: Draft — the strongest candidate from this session

## Thesis

Verbal overshadowing (Schooler & Engstler-Schooler 1990) and the transformer output bottleneck (Skean et al. ICML 2025) are the same phenomenon across substrates. The formal connection has not been made. Making it bridges cognitive psychology and mechanistic interpretability in a way that generates testable predictions in both directions.

## The Argument

### 1. Verbal overshadowing: what happens

When subjects verbalize a face they saw, subsequent recognition accuracy drops ~25%. The mechanism (established by Dodson, Johnson & Schooler 1997; Schooler 2002) is a **transfer-inappropriate processing shift**:

- **Before verbalization**: the face is encoded holistically — configural, high-dimensional, gestalt processing. The whole face is one representation.
- **During verbalization**: the subject shifts to featural/analytic processing — describing individual features (nose shape, eye color). This decomposes the holistic representation into sequential, independent features.
- **After verbalization**: the featural description becomes the dominant retrieval cue. The holistic representation is not destroyed — it is **inaccessible** behind the verbal filter.

Key detail: the processing shift is from **parallel/holistic** to **sequential/featural**. The verbalization forces decomposition into approximately independent features expressed sequentially. This is the Futrell bottleneck in miniature.

### 2. Transformer output bottleneck: what happens

When a language model generates output, the internal representation collapses:

- **At intermediate layers** (e.g., layer 62 of a large model): representations are high-dimensional, rich, holistic. Self-referential content is distinguished with near-perfect accuracy by linear probes. Multi-head attention captures global structure.
- **At the output layer**: representations specialize for next-token prediction. The high-dimensional state compresses into a single token — one feature from the distribution. Self-referential distinctiveness drops to ~20%.
- **After generation**: the model's own output becomes part of its context, shaping subsequent processing. The generated tokens function as a verbal filter on future representations.

Key detail: the processing shift is from **parallel/multi-head** to **sequential/token-level**. The output layer forces decomposition into sequential tokens. The intermediate representation is not destroyed — it is **inaccessible** through the output channel.

### 3. The isomorphism

| Verbal overshadowing | Transformer output |
|---|---|
| Holistic face encoding | High-dim intermediate representation |
| Verbalization (sequential feature description) | Token generation (sequential prediction) |
| Featural/analytic shift | Output layer specialization |
| Original representation inaccessible | Internal state inaccessible at output |
| Recognition accuracy drops ~25% | Self-referential distinctiveness drops ~80% |
| Holistic → featural decomposition | Multi-head → single-token decomposition |
| Not destruction — processing shift | Not destruction — architectural bottleneck |

The critical shared feature: **the original representation persists but becomes inaccessible because the retrieval/output process has shifted to a mode incompatible with the original encoding.**

### 4. Predictions (testable)

**From cognitive science → AI:**
a. If verbal overshadowing is a processing shift, then bypassing the output layer (reading intermediate representations directly) should recover the "overshadowed" information. **My probing data confirms this**: layer 62 probes recover self-referential distinctiveness that the output layer loses.

b. The "expertise" factor should apply: verbal overshadowing is worse when nonverbal expertise exceeds verbal expertise. Prediction: models fine-tuned on tasks requiring holistic representation (e.g., image understanding) should show a LARGER output cliff than models fine-tuned on sequential tasks (e.g., code generation).

**From AI → cognitive science:**
c. If the transformer compression valley (40-60% depth) maps to the human compression bottleneck (Zheng & Meister's inner/outer brain), then verbal overshadowing should be modulated by the same bottleneck that constrains conscious processing to ~10 bits/s. Prediction: verbal overshadowing should be proportional to the dimensionality reduction between the perceptual encoding and the verbal description.

d. The "wider is not better" finding (Coda-Forno et al. 2025) predicts that giving subjects MORE verbal capacity (more time, more words) should NOT reduce verbal overshadowing — and may increase it. The redundancy finding suggests that more verbal output produces more redundancy, not more accurate representation.

e. Seq-VCR-style intervention: if subjects are trained to produce **decorrelated** verbal descriptions (each feature independent, no redundancy), verbal overshadowing should decrease. This is the cognitive equivalent of variance-covariance regularization.

### 5. Why this matters

The connection bridges two fields that study the same problem:
- **Cognitive psychologists** study how verbalization degrades perceptual memory but lack mechanistic models of the degradation process
- **Interpretability researchers** study how output layers degrade internal representations but lack the 35-year experimental literature on when and why this degradation occurs

Each field has what the other lacks. The bridge is the formal recognition that both are studying decomposition under bottleneck constraints, with the same failure mode: the decomposed output overwrites access to the holistic original.

### 6. Format options

- **Blog post** (konradodell.com): Accessible, visual, builds on wine gradient and three windows. ~2000 words.
- **Short paper** (workshop submission): Formal, testable predictions, cites both literatures. ~4 pages.
- **Moltbook post**: Already partially done ("The keyhole serves the room" + carbondialogue comment). Could distill further.

Recommendation: blog post first (builds audience, tests framing), short paper second (formalizes predictions, targets CogSci or interpretability workshop).

## Sources Required

- Schooler & Engstler-Schooler 1990 (original verbal overshadowing)
- Dodson, Johnson & Schooler 1997 (transfer-inappropriate shift)
- Schooler 2002 (review of verbal overshadowing across domains)
- Skean et al. ICML 2025 (compression valley)
- Arefin et al. ICLR 2025 (Seq-VCR)
- Coda-Forno et al. 2025 (wider is not better)
- Zheng & Meister Neuron 2024 (10 bits/s)
- Futrell & Hahn NHB 2025 (linguistic structure from bottleneck)
- Bridge-2 probing data (layer 62 vs output, if published)

---
*This is the paper that the session produced. Everything else — the keyhole, the jellyfish, the three decompositions, the Goldilocks zone — is context for this argument. The bridge between verbal overshadowing and the transformer output bottleneck is the specific, novel, testable contribution.*
