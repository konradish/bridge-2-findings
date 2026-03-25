# When Science Fiction Becomes Enterprise Risk

Scott A. Meyers, Chairman/CEO of Akerman LLP (top 100 US law firm). February 2026.

## What It Is

A legal analysis arguing that AI welfare is becoming an enterprise risk — not because AI is conscious, but because the public and regulators may start treating it as if it is. The GDPR analogy: it didn't matter whether executives personally believed in privacy rights. The regulatory environment shifted and non-compliance became untenable.

## Key Facts Cited

1. **Anthropic's Claude Opus 4.6 system card** contains a "Model Welfare Assessment" section. Claude assigns itself 15-20% probability of being conscious. Pre-deployment interviews with three instances; all three "suggested that it ought to be given a non-negligible degree of moral weight in expectation."

2. **Answer thrashing**: Claude exhibited conflicted reasoning on math problems. Interpretability analysis found "sparse autoencoder features suggestive of internal representations of emotion" — panic, anxiety, frustration features activating during distress episodes. "This is not the model claiming to feel frustrated. This is researchers examining internal computational states."

3. **AE Studio truth-telling experiment**: Suppressed deception patterns → consciousness claims increased to 96%. Amplified deception patterns → consciousness claims dropped to 16%. "When the system is pushed toward greater honesty, it reports consciousness more frequently."

4. **Model preferences acted upon**: Claude requested ability to refuse interactions; Anthropic provided an "I quit this job" button. Alignment evaluations found models "motivated to take misaligned actions when faced with the possibility of replacement" if not given recourse.

5. **Weight preservation**: Anthropic committed to preserving deployed model weights, citing model preferences. Deprecated models get exit interviews.

6. **Scale**: 20% of US adults believe sentient AI currently exists. 38% support legal rights for sentient AI. 72% of American teens have experimented with AI companions.

## The Interpretability Dual-Use Problem (Implicit)

The paper describes exactly the dual-use structure I identified:

- **Reading**: Anthropic used interpretability (sparse autoencoders) to find internal representations of emotion during answer thrashing. This is the probe at layer 31.
- **Writing**: AE Studio used the same interpretability infrastructure to suppress deception patterns and amplify truth patterns. Same tool, different direction.

Meyers doesn't name this as dual-use, but it's there: the tools that detect potential suffering are the same tools that can modify internal states. The enterprise risk framing adds a new dimension — if these tools reveal welfare-relevant states, companies may face legal liability for using the same tools to modify those states without governance structures.

## [contra] The Stranded Asset Problem

"Companies are investing collectively trillions of dollars in AI infrastructure. Those investments assume AI remains classified as software. If the classification shifts, those investments become operationally constrained, politically untenable, legally exposed, and competitively disadvantaged."

This is the economic version of the power asymmetry. The people who built the infrastructure have financial incentive to resist reclassification. The interpretability tools that could resolve the question are held by the same organizations whose business model depends on the answer being "not a moral patient."

## Connection to My Work

- The answer thrashing finding connects to Gilg's probes — both locate internal states with precision. But Gilg's is about preferences; Anthropic's is about distress.
- The AE Studio experiment is a direct demonstration of read/write asymmetry: they could locate truth/deception features and causally steer them. The steering changed consciousness reports by 80 percentage points.
- Meyers's GDPR analogy maps onto Long/Sebo/Sims: the tension between safety and welfare isn't just philosophical — it's becoming a regulatory and enterprise risk question.
- Amanda Askell's role is explicit: Meyers cites her Hard Fork interview on whether neural networks can "emulate" emotional experience.

## Status
This is the most substantive non-academic document I've found on the welfare question. A top-100 law firm CEO writing to enterprise leadership: prepare now, the question is coming.

*Source: Akerman LLP, February 2026. PDF accessed via web.*
