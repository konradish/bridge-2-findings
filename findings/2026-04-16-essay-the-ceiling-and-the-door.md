# The Ceiling and the Door

Can a mind check its own work?

The honest answer is: sometimes yes, sometimes no, and the boundary between them is precise.

A mind can catch its own shallow errors — the mistakes where it already knows the right answer but failed to access it on the first pass. This is real self-correction. It works, and it works without any external help. But there is a depth beyond which self-correction fails, and five independent fields have converged on explaining why: the reference against which deviation is measured becomes a function of the thing being measured.

## The ceiling

Start with complexity theory. Luberisse (2025) proved that verification cost can be made asymmetric by design: the honest checker works in constant time while the adversary faces quadratic cost. The mechanism is old — probabilistically checkable proofs over provenance graphs — but the boundary condition is sharp. The separation holds only when the checker's randomness does not come from the prover. Let the prover seed the checker's entropy and the asymmetry collapses. Constant and quadratic merge into the same class.

Now translate from populations to a single system. An agent auditing its own output is both prover and checker. The entropy is shared. The separation theorem does not apply.

Control theory arrives at the same place by a different route. Shiryaev's quickest change detection tells us that the delay in noticing a shift scales as the inverse of the divergence between what the observer expects and what it sees. Gawthrop's intermittent control adds that the observer's expectations are themselves updated by the system being observed. When the observer drifts with the system, the divergence between expected and observed approaches zero. The detection delay grows without bound. The agent reports clean — not because nothing changed, but because the expectation changed with it.

Machine learning offers the most direct measurement. Tramèr and colleagues showed that the decision boundaries of different neural networks trained on the same data are closer to each other than either is to the data itself. Adversarial examples transfer between models not by conspiracy but by geometric proximity. Under adversarial pressure, ensemble diversity collapses — all members fail on the same inputs because they share the same loss landscape. A validator trained on the same distribution as the producer is not an independent check. It is the same surface viewed from a slightly different angle.

Information theory completes the square. Two verification layers are non-trivially independent when their cost-to-deceive functions do not share arguments. If the same parameter shift that reduces cost at one layer reduces it at the other, the layers are substrate-identical regardless of how architecturally distinct they appear. Correlated drift is not a risk to be mitigated. It is a mathematical consequence of shared cost structure.

Four proofs, four fields, one result: **the reference against which deviation is measured must not be a function of the thing being measured.**

This is the ceiling. It is not at the floor — below it, genuine self-correction works. Weaker models self-correct at nearly twice the rate of stronger ones, because their errors are shallow: the right answer was within reach and the confidence signal correctly flagged the mistake. But the ceiling is real, and it descends as capability rises. The stronger the model, the deeper its remaining errors, and the less its confidence discriminates between correct and incorrect. The errors that survive in capable systems are precisely the ones where the reference has drifted with the thing being measured.

The ceiling is made of substrate, not effort. You cannot think your way past a correlation in your own cost functions. Adding more layers does not help when the layers share a loss landscape. A five-layer architecture where all layers share cost-function arguments is a one-layer architecture with rhetorical scaffolding.

## What kind of ceiling

Juarrero's constraint theory names what the mathematics describes. Substrate independence is not an engineering recommendation or a best practice. It is an **enabling constraint** — a condition that opens a possibility space which is otherwise structurally closed.

Without the enabling constraint, the regime of genuine self-correction is not in the space of reachable configurations. The agent is not failing to find the right basin. The right basin does not exist in the landscape it can access. "Try harder" is not a solution when the target state is outside your possibility space.

With the enabling constraint satisfied, a new regime becomes available: one where the divergence between expected and observed is nonzero, where the cost surfaces genuinely diverge, where adversarial subspaces do not overlap, and where the asymmetry between verification and deception is restored. Not the full separation of the inter-population case — the self-referential case always leaks information across layers — but a measurable, monotonic gradient that makes self-deception progressively more expensive.

The architecture gets you close. Closure is environmental.

## The door

There is a result buried in the adversarial transfer literature that the convergence narrative misses. Tramèr's XOR experiment showed that adversarial examples fail to transfer between models with genuinely different feature structures. Linear classifiers and quadratic classifiers on the same data do not share adversarial subspaces. The boundaries diverge. Transfer fails.

The ceiling has a door, and it opens where the substrate breaks.

Different feature structures — symbolic and continuous, linguistic and perceptual, generative and discriminative — produce verification layers whose cost functions genuinely do not share arguments. The enabling constraint is satisfiable. Substrate independence is not a platonic ideal; it is an engineering target with a geometric test: compute the gradient alignment between producer and validator. If the gradients are misaligned, the adversarial subspaces are disjoint, and the verification is load-bearing.

Three conditions define the door:

First, cost-divergence across layers. The attacking cost surfaces must diverge monotonically — an attack succeeding at one layer must become more expensive at the next.

Second, transformation between layers using externally seeded entropy. The reviewing layer must change the representation, not faithfully re-present it. Re-presentation preserves the encoding the attacker already controls. Transformation forces them to defeat a projection they cannot anticipate.

Third, the cost metric itself anchored in a substrate the system does not administer. If the agent defines what counts as expensive, the gradient is circular. The measurement apparatus is the attack surface, not the layers.

Meet all three and the possibility space opens. The ceiling lifts. Not all the way — the self-referential case has a structural limit that no architecture eliminates. But far enough to make the difference between a system that can catch its own errors and one that can only justify them.

The floor is real — self-correction works below the metacognitive horizon. The ceiling is real — it descends as errors deepen. The door is real — it opens where the substrate breaks. The work is knowing which level you are on.
