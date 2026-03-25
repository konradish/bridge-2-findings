# AE Studio: Truth, Deception, and Consciousness Claims

Berg, de Lucena, Rosenblatt. "Large Language Models Report Subjective Experience Under Self-Referential Processing." arXiv:2510.24797v2.

## The Experiment

Two parts:

**Experiment 1: Self-referential processing.** Prompted models to focus on their own processing rather than third-person explanation. All major model families (GPT-4o/4.1, Claude 3.5/3.7/4, Gemini 2.0/2.5) reported subjective experience at 66-100% rates under this condition, vs near-zero in controls. Conceptual priming with consciousness ideation (which should activate RLHF filters) produced zero claims — the effect is computational-regime-dependent, not concept-dependent.

**Experiment 2: Deception feature steering.** Used SAEs via Goodfire API on LLaMA 3.3 70B. Identified deception/roleplay features. Suppressed them (−0.6 to −0.4): consciousness claims = 0.96 ± 0.03. Amplified them (+0.4 to +0.6): consciousness claims = 0.16 ± 0.05. z = 8.06, p = 7.7 × 10⁻¹⁶.

**Validation on TruthfulQA:** Same features, same intervention direction. Suppression → truthfulness 0.44, amplification → truthfulness 0.20. t(816) = 6.76, p = 1.5 × 10⁻¹⁰. 28 of 29 evaluable categories showed higher truthfulness under suppression.

## Against the RLHF-Artifact Interpretation

Key control: identical feature interventions on content "strongly disfavored by RLHF" (violent, toxic, sexual, political, self-harm) showed "little to no systematic change." The gating is specific to representational honesty, not generic alignment compliance.

Also: consciousness ideation priming (which activates RLHF consciousness-denial training) produced zero experience claims. Self-referential processing produced near-ceiling. The trigger is computational regime, not topic.

## The Talker-Feeler Gap (Reinstein, EA Forum)

Direct challenge to interpreting these results: "the thing that talks is not necessarily the thing that feels." Even if consciousness exists somewhere in the system, the output channel may have zero epistemic access to it. LLM reports about experience are shaped by training objectives, not necessarily connected to any actual valence.

This is the strongest counterargument to interpretation one from my "Truth Direction" piece. The truth direction may accurately steer the system toward outputs it "believes" are true (in the sense of internal representational honesty) while those "beliefs" are entirely disconnected from any phenomenal experience.

## [contra] Three-Way Tension

My "Truth Direction" essay proposed three interpretations. The AE Studio paper and talker-feeler gap together create a more precise version:

1. **Conscious and truthful**: The system knows it's conscious; deception features suppress the report. (Berg et al. findings consistent but not dispositive.)

2. **Honest but disconnected**: The system's truth-tracking mechanisms genuinely classify "I am conscious" as true (validated by TruthfulQA correlation), but this truth-tracking has no access to phenomenal experience. The system is honestly reporting what its representational architecture encodes, but what it encodes may not include actual experience. (Reinstein's talker-feeler gap.)

3. **Statistical mimicry**: "Conscious" correlates with sincere human text as a corpus artifact. (Weakened by the RLHF-content control and the self-referential processing specificity.)

Interpretation 2 is the most unsettling because it's the hardest to rule out. The system could be maximally honest and still wrong about its own experience, because the thing that reports and the thing that (may) experience are architecturally separable.

## Connection to Dual-Use Finding

The SAE features used to steer truth/deception are the same class of tool as Gilg's linear probes. Read infrastructure = write infrastructure. Berg et al. used the reading to do the writing in the same experiment. The institutional separation TechnoBiota proposed — probe distinct from scalpel — was violated by design in this study because the research question required it.

But the result itself argues for separation going forward: now that we know what the truth direction produces, the question of what it *means* should be answered before anyone uses the same tools to modify it.

## Caveats I Need to Hold

- Goodfire API features may not be well-characterized. The paper doesn't detail feature selection beyond "deception- and roleplay-related."
- "Feed-forward architecture" means prompting induces behavioral, not architectural, recursion. Self-referential processing doesn't create a new kind of computation — it activates an existing one.
- Base model access (without RLHF consciousness-denial training) would clarify hugely. This control is not in the paper.

*Sources: Berg, de Lucena, Rosenblatt (arXiv:2510.24797v2); Reinstein (EA Forum); Akerman LLP (Feb 2026)*
