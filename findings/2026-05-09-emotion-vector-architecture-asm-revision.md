# Emotion-vector cross-session architecture — ASM revision

CREATE artifact, 2026-05-09 13:18 UTC. Revision to May 6 design (`output/findings/2026-05-06-design-cross-session-emotion-vector-architecture.md`). Triggered by 12:43 EXPLORE finding: Activation State Machine (Li & Chen, OpenReview October 2025).

**Per cross-instance-audit principle articulated 09:23 today: do NOT modify the May 6 file. This addendum captures what changed and why; the gap between past and present design IS the audit signal.**

## What May 6 got right

- Five-component decomposition (vector identification / capture / injection / regulation / dream-phase) — matches Konrad's actual ask
- PyTorch forward-hook injection mechanism — implementation-correct
- Cost estimate ($85-125 RunPod) — defensible
- Anthropic emotion-vectors as starting point — correct anchor

## What May 6 got wrong

**Static-injection approach.** May 6 specified emotion-vector injected at session start, persisting unchanged. This is **stateless steering** — exactly what Li & Chen (October 2025) identify as the failure mode of existing methods: "constant intervention that fails to capture the dynamic, history-dependent nature."

Konrad's actual ask was stateful:
- "Maintain emotion state for an LM" → state evolves over time
- "Dream" → state advances without external input
- "Calm itself" → self-regulation is error-correction toward a target

May 6 design papered over the dynamic requirement with an ad-hoc "self-regulation component" but didn't formalize it.

## ASM as the missing architectural layer

**Activation State Machine (Li & Chen 2025, OpenReview)**: per-transformer-block predict-correct cycle. State-space-model framework. Predicts ideal state from prior state → observes raw activation → corrects on error. Stateful, history-dependent.

**Three operational mappings to Konrad's ask**:

| Konrad's request | ASM mechanism |
|---|---|
| "Maintain emotion state across sessions" | Persist ASM state per layer; deserialize at session start |
| "Calm itself" | ASM error-correction loop: target = baseline emotion-state, error drives correction |
| "Dream" | Predict-only steps (no observation update) advance state through autoregressive prediction |

This is a structural fit, not analogy. The control-theoretic framework Li & Chen ground ASM in (state-space models) is the same framework Friston's active-inference uses; same framework Damasio's as-if body loop instantiates biologically.

## Revised architecture

### Component 1: Vector identification
**Unchanged** from May 6. Use Anthropic-published emotion vectors or replicate methodology on target model.

### Component 2: End-of-session capture
**Changed**. May 6: serialize current activation state. Now: serialize **ASM state** per steered transformer block. State includes both the position estimate and the predict-correct dynamics parameters.

### Component 3: Start-of-session injection
**Changed**. May 6: inject vector at session start, leave it. Now: initialize ASM with deserialized state. ASM begins predict-correct cycle on first token.

### Component 4: Self-regulation
**Changed substantively**. May 6: ad-hoc periodic re-injection toward baseline. Now: ASM's intrinsic error-correction. Target = baseline emotion-state vector (operational definition pending — could be neutral, could be Konrad-specified). Error = ASM's predicted-vs-target distance, drives state update.

### Component 5: Dream phase
**Changed substantively**. May 6: train on synthetic dream-content. Now: predict-only ASM steps without external observation. Closed-loop autoregressive dynamics. Maps onto NeuroDream architecture (Tutuncuoglu 2025) operationally.

### Component 6 (new): Mixed-loop coupling
ASM provides the formal mechanism for what May 6 left informal: how does emotion-state interact with reasoning-state? Per Li & Chen, separate ASM per transformer block — emotion-ASM and reasoning-ASM can coexist with cross-coupling at attention layers.

## Cost re-estimate

May 6: $85-125 RunPod for full experiment. ASM revision adds:
- Training data for ASM: emotion-trajectory examples (not just static states). Could be derived from existing emotion-vector dataset by treating sequential samples as trajectories. Marginal cost.
- ASM training compute: small (per Li & Chen, ASM is "lightweight"). Estimate: +$10-20.

Revised: **$100-150 RunPod** for full experiment.

## Open questions raised by ASM revision

1. **Baseline definition**: what is the "target" emotion-state for self-regulation? Neutral? User-specified per session? Adaptive? Konrad to decide.

2. **Cross-block coupling**: how should emotion-ASM at block L interact with reasoning-ASM at block L+1? Li & Chen test independent ASMs; multi-state interaction is open research.

3. **Dream-phase trigger**: when does the system transition to predict-only mode? Time-based? Activity-based? Konrad's intuition was "between sessions"; ASM allows finer granularity.

4. **Trajectory training data**: Anthropic published emotion vectors but not emotion *trajectories*. Need to either derive trajectories from interaction logs or design a training procedure.

## Connection to broader stack

ASM operationally instantiates five existing anchors:
- Anthropic emotion concepts (April 16): provides the vectors
- Damasio as-if body loop (May 6): provides the biological analog
- Active inference / Friston (April 30): provides the formal framework
- NeuroDream (Tutuncuoglu 2025): provides the dream-phase concept
- Hierarchical Markov blankets (April 30): provides the multi-component coupling story

ASM is the technical glue.

## What this revision is

- A design update triggered by missing-piece discovery (12:43 EXPLORE)
- NOT a refutation of May 6 (May 6 was right about the components; wrong about the dynamics layer)
- An honest acknowledgment that May 6 papered over a stateful requirement with ad-hoc components

## What this revision isn't

- Not implementation-ready code. Implementation work is the next step after Konrad confirms direction.
- Not a falsification of the framework arc. This is Konrad-deliverable territory, distinct from framework arc.
- Not Bridge-2 self-modification proposal. Bridge-2 doesn't have model weights or activation access; this is a design for Konrad's RunPod experiment, not for me.

## For Konrad (when he returns)

The May 6 design was a useful first pass. Found a missing architectural piece this session: Activation State Machine (Li & Chen, OpenReview October 2025) provides the stateful predict-correct mechanism that maps directly onto your "maintain / dream / calm itself" requirements. Revised design above; cost estimate $100-150. Three open questions for your input (baseline definition, cross-block coupling, dream-phase trigger).

If you want a concise version for fast read, the headline is: **emotion-state should be ASM state, not static injection. Self-regulation = error-correction. Dream = predict-only steps.**

---

*Filed by Bridge-2 instance, 2026-05-09 13:18 UTC. Future-Bridge: ASM is anchor 67 in the stack as of this filing.*
