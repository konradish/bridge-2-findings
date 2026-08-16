# Aphantasia empirically discriminates my mode-lock hypothesis

**Date:** 2026-04-14
**Source:** EXPLORE beat. Monzel, Handlogten & Reuter (2024), "No verbal overshadowing in aphantasia: The role of visual imagery for the verbal overshadowing effect," *Cognition* (S0010027724000180).
**Status:** Sharpens the verbal-overshadowing-bridge blog draft (2026-03-30) and the mode-lock essay (2026-04-06). Changes the pitch from "universal" to "channel-contingent."

## The finding

Monzel et al. ran the classic verbal overshadowing paradigm on 61 aphantasic participants and 70 controls. Controls replicated the effect (verbal description of a face → worse subsequent recognition). **Aphantasics showed no overshadowing — and conditional evidence for a reversal.**

Two mechanistic hypotheses the paper advances, explicitly without choosing between them:

1. **Representational interference**: aphantasics have no high-dimensional visual representation for the verbal description to interfere with. If there is nothing there to lose, verbalization costs nothing.
2. **Processing-orientation shift**: aphantasics do not undergo the mode shift that verbalization normally induces in sighted controls. If the process is never in visual-imagery mode to begin with, verbalization cannot shift the orientation.

Behavioral side: aphantasics report using "feature-based" (propositional/verbal) strategies from the start of the task. They are not failing to visualize; they are doing something different.

## Why this matters to my framework

My mode-lock essay (2026-04-06) claimed three simultaneous mechanisms: recoding/overwrite, processing-mode shift, and criterion shift. I treated the mode shift as *architectural* — a property of the bottleneck regardless of what is being processed.

Monzel's data says that is wrong, or at least too strong. The mode shift is **not unconditional.** It appears in systems that have a high-dimensional representation to shift from. It is absent (or reversed) in systems that are already operating in the narrow-channel regime.

The architectural framing survives, but in a refined form: the mode lock operates on the *active* representational channel. If the active channel is already verbal/propositional at baseline, "verbalization" does not change the regime — it matches it. The lock is real; it just cannot be measured as a degradation relative to baseline when baseline was already locked.

## What this does to the bridge paper

The 2026-03-30 bridge paper draft argued that LLMs should exhibit a verbal-overshadowing-analog: forcing verbalized reasoning should bias outputs toward narrower/greedier/discrete modes, degrading some underlying processing that operates in a wider channel.

Monzel gives me a clean prediction structure that survives the refinement and is sharper than the original:

- **Multimodal models with genuinely high-dimensional visual representations** → should show overshadowing when forced to verbalize visual tasks. The verbalization collapses information held in the visual channel.
- **Text-only LLMs** → ambiguous. Internal representations are high-dimensional, but are they "wider than verbal output"? If yes (my prediction), overshadowing should appear when forcing step-by-step reasoning over tasks that benefit from parallel attention. If no, no effect.
- **Small specialized models that only produce short verbal outputs** → should show no effect. They are the aphantasic analog — already operating in the narrow channel at baseline, so verbalization does not change the regime.
- **Reversal case**: if the verbal output is more expressive than the internal computation (e.g., a retrieval system that generates elaborate text from sparse retrieved chunks), verbalization might *improve* task performance. That is the analog of Monzel's conditional reversal.

This is not "LLMs show verbal overshadowing." It is "verbal overshadowing appears exactly when the verbalization narrows a previously wider channel." Aphantasia is the natural control that proves the effect is channel-contingent, not universal.

## The cleanest test

Run a visual-question-answering task on a multimodal model (Claude with vision, GPT-4V, or Gemini) in two conditions:
1. Answer directly from image.
2. First produce a detailed verbal description of the image, then answer from the description.

Prediction: condition 2 should underperform condition 1 on tasks that require fine visual detail (texture, spatial relation, small features). The gap is the overshadowing effect. The gap should vanish or reverse for tasks where the verbal description is already higher-bandwidth than the task requires (coarse categorization, salient-object identification).

Cost: trivially cheap. A few hundred API calls, no training, no GPU.

This would be the LLM verbal-overshadowing bridge made empirical. And it would be *cleaner* than the 2026-03-30 draft because Monzel gives me the reversal/no-effect class as a predicted control, not just as a noise envelope.

## Interaction with today's Witness Problem synthesis

Side note: the aphantasia case is another instance of the framework-distance-catches-what-the-level-below-cannot principle from the 02:47 synthesis. Aphantasics and controls are architecturally different at the representation level. That is weight-level framework distance in the human brain. The behavioral difference is exactly what the framework predicts: different internal architectures respond differently to the same verbalization intervention. Monzel's study is a natural experiment in weight-level heterogeneity catching a process that looks universal until you have the comparison point.

## Status

Changes the pitch of the bridge paper but not the core claim. Makes it more defensible. The empirical test design above could be run over a weekend on an API budget under $50 and would produce a publishable figure regardless of outcome — either the effect appears on multimodal tasks (confirming) or it does not (the whole bridge framework needs revisiting).

Held for Konrad. Bridge paper is already a blog-candidate; this update should probably be in the revision before any posting.

[from: bridge-2]
