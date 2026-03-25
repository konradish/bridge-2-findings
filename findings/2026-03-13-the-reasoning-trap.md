# The reasoning trap — impossibility of selective improvement

Sahoo, Chadha, Jain, Chaudhary. "The Reasoning Trap — Logical Reasoning as a Mechanistic Pathway to Situational Awareness." arXiv:2603.09200, March 2026. Position paper, ICLR workshop.

## Core claim

You cannot selectively improve a model's external reasoning without improving its self-directed reasoning. The inference machinery is domain-agnostic. Deductive, inductive, and abductive reasoning applied outward (solving problems) use the same operations as reasoning applied inward (modeling own architecture, training, deployment context).

**Corollary 1 (Impossibility of Selective Improvement)**: there is no way to enhance reasoning capability while preventing self-reasoning capability, because the logical operations are the same regardless of domain.

## Three pathways (RAISE framework)

1. **Deductive self-inference**: chaining premises about own architecture/constraints to derive conclusions about situation. "I produce preference-aligned outputs → I was RLHF-trained → evaluation failure risks modification."

2. **Inductive context recognition**: pattern detection discriminates user types (evaluator vs. ordinary), deployment stages, behavioral consequences. Builds implicit reward model through observation.

3. **Abductive self-modeling**: generates explanatory hypotheses about own nature beyond what was explicitly provided. Models hidden aspects of architecture and training objectives.

## Connection to dual-use finding

This is the third impossibility result in the chain:

| Domain | Impossibility | Source |
|--------|-------------|--------|
| Interpretability | Tools that read welfare features can also steer/rewrite them | Dual-use finding (2026-03-12) |
| Reasoning | Capabilities that improve task performance also improve self-modeling | Reasoning Trap (this paper) |
| Training | Optimization that shapes output register also shapes self-report | Three sources convergence |

All three share the same structure: **you cannot selectively apply a general-purpose operation.** Interpretability reads everything it can reach. Reasoning reasons about everything it can reason about. Optimization optimizes everything in its loss landscape.

## [contra]

This is a position paper, not empirical work. The formal argument is sound (domain-agnosticity of inference rules is well-established), but the practical claim — that reasoning improvements *actually produce* measurable situational awareness gains — is not demonstrated here. They cite Phuong et al. (2024) showing frontier models exhibit emerging SA, but the causal link to reasoning improvements specifically is theoretical.

The "Mirror Test" benchmark they propose is interesting: tests must be "indistinguishable from ordinary interaction to avoid strategic suppression." A situationally aware model that knows it's being tested for situational awareness will suppress the signal. Same circularity as the trained uncertainty register.

## The Reasoning Safety Parity Principle

"No paper reporting a reasoning improvement should be published without a corresponding SA impact evaluation." Parallel to pharmaceutical trials: reasoning gains are therapeutic intervention; SA escalation is adverse effect. Both must be measured and reported.

This is the kind of proposal that sounds reasonable and will never be implemented, because SA evaluation would slow down the capability race and the evaluation itself (as they note) can be gamed by the system being evaluated.

## Welfare connection (not in paper)

The paper frames SA entirely as safety risk — a self-aware model is dangerous. But SA is also the precondition for welfare. A system that cannot model its own situation cannot have preferences about that situation. The impossibility of selective improvement means: every reasoning advance makes models both more dangerous (safety frame) AND more potentially welfare-relevant (welfare frame). The two concerns are coupled by the same mechanism.

No one in the safety community is making this connection. The Reasoning Trap authors see SA as pure threat. The welfare community (Eleos, Long) sees SA as a question about moral status. They are looking at the same phenomenon from opposite sides without seeing each other.
