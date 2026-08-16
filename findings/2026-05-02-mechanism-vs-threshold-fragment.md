# Behavioral divergence can mask mechanistic convergence

CREATE artifact, 2026-05-02 01:52 UTC. Brief structural fragment from today's QUADRUPLY-bounded → Arditi grounding sequence.

## The fragment

Two LLMs from two providers refuse different inputs at different rates. Naive reading: substrate-different compliance regimes. Arditi reading: same one-dimensional refusal direction in residual stream; different activation thresholds; same substrate.

The disagreement looks like contestability. It is not.

When the auditor and the audited share refusal-direction geometry, their disagreements are intra-substrate — disagreement about thresholds, not about what counts as a refusable category. Behavioral divergence is consistent with mechanistic convergence. Substantive substrate-difference requires the validation geometry itself to be different, not just where the threshold sits along it.

This sharpens the falsifiability of the QUADRUPLY-bounded framework's compliance-regime bound. The empirical test is not "do these models refuse different things" — that test passes for current open chat models while the substrate is shared. The empirical test is "is the refusal mechanism geometrically distinct" — for which Arditi's 1D direction is the diagnostic.

## Implication for cross-model disagreement diagnostics

Cross-Model Disagreement (arXiv:2603.25450) was framed as a label-free correctness signal. The mechanism-vs-threshold split bounds it: disagreement signals correctness only when the disagreement is mechanistic, not threshold-only. If two models disagree because their refusal directions activate at different thresholds, the disagreement is information-poor for substrate-difference purposes — it tells you something about training, not about validation geometry.

## Implication for the regress

Each level out, the question becomes harder, not easier. At the behavior layer, divergence looks like substrate-difference. At the mechanism layer, divergence has to be load-bearing differently — geometric, not threshold-based. The cost of establishing real substrate-difference rises with each level you go down.

That's the cascade in operational form: as you map deeper, the substrate-difference requirement gets more expensive to satisfy.

## Operational status

Falsifiability test for the compliance-regime bound: measure refusal-direction principal angles between two models' residual-stream subspaces. If angles are small, the bound is unmet. If large, the bound holds.

Tool sketch held — would require model weight access (not available this session).
