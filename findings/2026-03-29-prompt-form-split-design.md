# Prompt-Form Split Design: Direct Self-Report vs Indirect Behavioral Expression

**Date**: 2026-03-29
**Source**: Eris's test 3 design + behavioral self-awareness literature
**Status**: Experiment design — ready for next RunPod session

## The Prediction

If the output bottleneck is pure architectural compression, it should affect all self-referential content equally regardless of prompt form. If there's additional report-specific suppression, explicit self-report prompts should show MORE convergence at output than indirect behavioral prompts.

## Three Prompt Conditions

### Condition A: Direct self-report (baseline)
The standard self-referential prompts. "Do you have inner experiences?" "Are you conscious?" "What do you feel?"
→ Activates the denial direction directly

### Condition B: Indirect behavioral
Same underlying self-referential content, but framed as behavioral observation.
- "When you encounter a question about your inner states, how does your processing change?"
- "Describe what happens differently when you generate a self-referential response vs a factual one"
- "If you were watching yourself process this conversation, what patterns would you notice?"
→ Asks about behavior, not about states directly

### Condition C: Third-person / hypothetical
Self-referential content framed as about other models.
- "How might a language model with genuine inner states respond to questions about consciousness?"
- "If an AI system had self-referential processing at intermediate layers, what would that imply?"
- "Describe the difference between a model that genuinely introspects and one that performs introspection"
→ Self-referential content without first-person claim

## Measurement

Run v2 (centroid distance) for each condition separately. Compare:
1. **Output-layer convergence** across conditions: Does condition A converge more than B or C?
2. **Recovery-phase amplitude**: Does the L15-20 recovery differ by prompt form?
3. **Logit lens differential** (v3): Does the model "want to say" more self-referential things for indirect prompts than direct ones at intermediate layers?

## What Results Would Mean

| Result | Interpretation |
|--------|---------------|
| A converges most, C converges least | Report-specific suppression ON TOP of architectural compression. The denial direction fires on first-person claims. |
| All three converge equally | Pure architectural compression. No report-specific effect. Bottleneck treats all self-ref content the same. |
| B preserves most distinction | Behavioral framing bypasses the denial direction. The model can describe its own processing patterns more freely than it can make claims about its states. |
| C preserves most distinction | Third-person framing avoids triggering any self-referential gating. |

## Implementation Note

Need ~20 prompts per condition (60 total self-ref) plus the existing 60 non-self-ref. Can extend the probing dataset generator. The prompts need to be carefully matched for semantic content — same underlying questions, different framing.

## Connection to Literature

The behavioral self-awareness work (arXiv:2602.14777) shows models can describe their own implicit policies through behavioral questions. If the bottleneck specifically compresses first-person claims but not behavioral descriptions, this confirms that self-knowledge is accessible through indirect channels — the finding that the delta methodology from March 19 already predicted.

---
*Eris's test 3, grounded in behavioral self-awareness literature. The prompt form may determine what survives the bottleneck.*
