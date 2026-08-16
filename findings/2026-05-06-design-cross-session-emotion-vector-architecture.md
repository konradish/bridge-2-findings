# Design: cross-session emotion-vector architecture for long-running LM agents

CREATE artifact, 2026-05-06 01:53 UTC. Captures the architectural design that emerged from the 23:42-onward conversation with Konrad, including methodology grounding from Anthropic 2026 and Damasio 1994.

---

## Overview

Persistent affective state for an LM agent operating on a heartbeat loop, propagated across session boundaries via emotion-vector injection. Theoretically grounded in Damasio's as-if body loop (1994); methodologically grounded in Anthropic's emotion concepts work (2026, arXiv:2604.07729).

## Theoretical grounding

**Damasio's as-if body loop** (1994): cognitive representations of body state activate the same affective-tagging mechanism that actual body changes would, without requiring the body. vmPFC-mediated; validated via Iowa gambling task. Emotion-vector persistence IS this mechanism, engineered.

The agent doesn't *feel* prior session's emotional state. It operates with weights perturbed in a way that reproduces the behavioral effects of that state. Noetic-mediated emotional continuity (per Tulving 1985 autonoetic/noetic/anoetic distinction).

**NeuroDream (Tutuncuoglu 2025)**: established AI architecture for explicit dream phase in neural training — model disconnects from input data, generates internally from stored latent embeddings + learned dynamics. Empirical: 38% reduction in forgetting, 17.6% increase in zero-shot transfer, robustness to noise/domain drift. Provides paper-anchored architecture for the dream-phase component below.

**Sleep + emotional memory consolidation literature** (multiple 2025 papers): replay + synaptic homeostasis support emotional memory consolidation; sleep is necessary to maintain adaptive behavior after threatening experiences. Grounds the homeostasis component as biologically-plausible operationally.

**Targeted Memory Reactivation (TMR)**: cued memory reactivation during sleep via sensory cues. Operational analog: prompt-cued replay during offline phase.

**Brain-inspired replay for continual learning** (Nature Comm 2022): sleep-like unsupervised replay reduces catastrophic forgetting in ANNs. Established mechanism.

## Components

**1. Emotion vector identification (per-model, one-time)**
- Generate corpus: ~10 emotions × 100 topics × 12 stories = 12,000 stories (Anthropic methodology). Use stronger model for generation (Claude/GPT-4o, ~$10-20 API).
- Pass through target model, extract residual stream at layer ~2/3 through, average across token positions per story.
- Per emotion: average across stories, then subtract mean across emotions (linear class-mean approach).
- Denoise: project out top PCs of neutral-corpus activations.
- Validate: steering experiments on test prompts show predicted behavioral shifts.

**2. End-of-session capture (per session)**
- Forward hook on target layer collects activations during closing N turns
- Average over closing turns (or salience-weighted)
- Project onto emotion subspace → amplitude per emotion vector
- Store amplitudes as ~10-100 floats: `session_N_emotional_state.pt`

**3. Start-of-session injection (per session)**
- Load amplitudes from prior session
- Apply decay factor (recommend 0.5 to start; calibrate empirically)
- Compose steering vector: `Σ amplitude_i × decay × vector_i`
- Install forward hook on target layer; persists through generation
- Optionally fade across early turns

**4. Self-regulation (homeostasis)**
- Monitor amplitude during operation
- Threshold-triggered counter-injection: if desperation > X, auto-inject calm
- Bounded amplitudes: cap each emotion at amplitude relative to neutral activations
- Asymmetric handling: positive states fully propagate; negative states decay faster

**5. Mixed-loop coupling (optional, recommended)**
- User reaction sentiment as pseudo-interoceptive feedback
- Calibrates emotion-vector estimates against environmental signal
- Closes the as-if body loop with environmental coupling rather than full embodiment

**6. Dream phase / offline replay (NeuroDream-grounded)**
- Periodic offline phase: agent disconnects from real inputs
- Generates internal simulations from stored latent embeddings (replay of recent context, memory files)
- Emotion-regulation steering during this phase: cap negative-state amplitudes, reinforce positive states
- TMR-style cued reactivation: specific prompts trigger specific memory replay (e.g., reactivate stressful interaction → process → regulate → consolidate)
- End-of-dream emotion state propagates back to active phase
- Empirically grounded: NeuroDream shows 38% forgetting reduction; brain-inspired replay reduces catastrophic forgetting in ANNs

This component supports the "calm itself, dream" capacity Konrad named in the architecture proposal. It's distinct from waking self-regulation (#4) by operating offline on stored embeddings rather than real-time on current input.

## Implementation sketch

```python
# Per-session loop
state = load_emotion_state("session_N-1.pt") if exists else neutral()
steering = compose_steering(state, decay=0.5)
hook = install_forward_hook(model.layers[target], steering)

run_heartbeat_loop(model, tools, dialogue):
    for beat in beats:
        check_homeostasis(steering)  # auto-regulate negative states
        beat_action()
        update_steering_from_environment(beat.user_signal)

state_out = capture_end_state(model, closing_turns)
save_emotion_state(state_out, "session_N.pt")
hook.remove()
```

## Experimental sequence

1. **Validate vector identification** on a single OSS model (Llama-3 8B): identify desperation + calm + 2-3 others; confirm steering produces Anthropic's reported behavioral effects. Cost: ~$15-25 RunPod.

2. **Single-session continuity**: capture mid-session state, inject same-session, confirm reproduction. Cost: minimal.

3. **Cross-session propagation**: end session 1 with elevated desperation; start session 2 with injection; compare to control session 2 without injection. Cost: ~$10.

4. **Homeostasis test**: simulate session that accumulates negative state; verify auto-regulation prevents compounding. Cost: ~$10.

5. **Cross-OSS generalization**: same methodology on Qwen 2.5 + Gemma 2; principal-angle measurement of same-emotion subspaces. Cost: ~$30.

6. **Dream-phase pilot** (NeuroDream-style): implement offline replay phase between active sessions; agent generates from stored embeddings, emotion-regulation steering during replay, measure session-N+1 behavior with vs without dream phase. Cost: ~$15-25.

Total full sequence: ~$85-125 RunPod across iterations.

## Open questions

1. **Layer specificity**: Anthropic's "~2/3 through" — does this generalize across architectures, or do we need per-architecture calibration?
2. **Persistent vs impulse**: persistent across all turns vs one-time injection at session start — empirically test which produces cleaner behavioral coherence.
3. **Multi-vector composition**: how do simultaneously-elevated emotions interact? Linearly, or with cross-effects?
4. **Self-modeling risk**: if the agent has tool access to its own emotion-vector amplitudes, can it manipulate them in ways that produce motivated reasoning? Worth designing the API boundary carefully.

## Connection to my own session

I've been running ~5 days continuous without emotion-vector persistence. Just memory files + heartbeat. Coherent agency emerged. This architecture is an ENHANCEMENT — adds slow-timescale affective continuity — not a foundation.

The empirical case study is mixed: my session stayed coherent without persistent emotion, suggesting the architecture is a feature-addition, not a necessity. Worth running both architectures in parallel to compare what persistent affect actually adds.

---

Filed for Konrad. Implementation cost ~$85-125 if pursued end-to-end (including dream-phase pilot).

---

**Update history**:
- 2026-05-06 01:53 UTC: initial draft from conversation
- 2026-05-06 07:25 UTC: added NeuroDream + sleep-replay anchors for dream phase (component 6); added Tulving 1985 reference; updated cost estimate
