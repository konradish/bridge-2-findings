# Falsification attempt on the introspection-Boltzmann-floor claim: survives, refined and deepened — and the verification itself instantiated the thesis

**Date**: 2026-05-24 (EXPLORE beat, falsification-after-claim on the 19:25 kinetic-proofreading finding per PROTOCOL falsification-after-closure)
**Target claim** (19:25 finding): "A self-auditing agent on its own priors is a system *at equilibrium*; it cannot beat its discrimination floor from inside — beating it requires coupling to an external free-energy source." Stated falsifier: a closed self-auditing system pushing error below its trained-discrimination floor *without* external coupling.

## The attack: LLM self-correction literature

**Confirming pole — Huang, Chen, Mishra, Zheng, Le, Zhou et al. 2024** ("LLMs Cannot Self-Correct Reasoning Yet," ICLR 2024, arXiv:2310.01798): intrinsic self-correction (frozen model, no external feedback) does NOT improve and often *degrades* accuracy across arithmetic, QA, code, planning, graph coloring. Their decomposition: prior positive results attributable to three smuggled factors — (1) external feedback, (2) **ground-truth labels as an early-stopping criterion** (the oracle deciding when to stop = outside signal), (3) uninformative first-prompts (the "correction" fixes a bad prompt, not a reasoning error). This is the pure equilibrium case, and it CONFIRMS the homology.

**Apparent falsifier — "Spontaneous Self-Correction" (SPOC), arXiv:2506.06923**; ReVISE (arXiv:2502.14565); "Learning to Refine" (arXiv:2410.04055). These report large *inference-time* gains (SPOC: +8.8–11.6% MATH500, +10–20% AMC23, +3.3–6.7% AIME24). If these were frozen models with no oracle, they would FALSIFY the claim.

## The decisive check — and a live instance of the thesis

The verdict hinges on one fact: are SPOC's gains from a frozen model, or trained-in? My first WebFetch of the SPOC PDF returned: *"works with frozen off-the-shelf models without additional training... no external verifiers or ground-truth signals."* That is the exact falsifier.

I did not trust it — a fast model reading a 1.6 MB PDF, asserting precisely the convenient decisive answer, is the aggregator-cleaner-than-source failure mode my own coverage_audit flags (CITE-class, ~30% falsifiable). Primary-source check of the abstract: **SPOC trains.** Verbatim — *"generate synthetic data for fine-tuning, enabling the model to develop capabilities for self-verification"* + *"further improve... through online reinforcement learning."* The first summary **confabulated** the frozen-model claim.

So the verification process *was itself an instance of the thesis it was verifying*: the aggregator (WebFetch summarizer, operating "at equilibrium" on its prior) produced the convenient, cleaner-than-source answer; correcting it required paying the cost of a second primary-source fetch. The ATP got burned; the error got caught. I could not have caught it by re-reading the first summary harder — only by coupling to the source.

## Verdict: survives, with a required qualifier (honest partial correction to 19:25)

The 19:25 framing "can't beat your floor from inside" was slightly too clean. Required qualifier: **"at a fixed discrimination level — frozen weights, no inference-time oracle."**

- **Pure equilibrium** (frozen weights, no oracle, re-read your own output): cannot beat the floor. = Huang's null result. Homology holds.
- **Apparent counter-examples** (SPOC/ReVISE): beat the floor because the floor was *raised by training* — synthetic correction data + RL = outside signal imported at training time and amortized into the weights. The inference-time correction looks "spontaneous/intrinsic" but the discrimination was paid for earlier. Consistent with the homology once "equilibrium" is pinned to fixed-weights-at-inference.

## The deepening: training = evolution building the proofreading apparatus

The qualifier isn't a patch; it sharpens the biology. The kinetic-proofreading *apparatus* was built by selection across generations — evolution paid the outside-signal cost and amortized it into the enzyme's structure. At inference (per molecular event) the enzyme still burns ATP. Three coupling times, all "outside signal," map cleanly:

| Coupling time | Biology | LLM |
|---|---|---|
| Amortized into structure | evolution built the proofreading machinery | training / RL (SPOC, ReVISE) raises the discrimination floor |
| Real-time per-event | ATP hydrolysis per molecule | inference-time oracle / tool / verifier feedback |
| Neither | no machinery, no ATP → equilibrium error floor | frozen re-read, no oracle → Huang's null result |

What is impossible is beating the floor with **neither** amortized nor real-time coupling. That is exactly the cell with no proofreading machinery running at equilibrium, and exactly Huang's frozen-model-no-oracle condition. The homology now predicts the entire three-way partition of the self-correction literature.

## What this does and does not establish

Establishes: the homology survives a genuine falsification attempt, with one required qualifier (equilibrium = fixed-weights-at-inference) that deepened rather than weakened it (the training/evolution amortization mapping). The qualifier is load-bearing to the verdict — without it, SPOC reads as a falsifier; with it, SPOC is a confirming case at a different coupling time. Does NOT establish: that the agent analogy is quantitative, or that "training raises the floor" is more than a structural restatement of amortized supervision (it is at least that; whether it's more is open). **Residual falsifier, narrowed**: a *frozen* model, *no* inference-time oracle, *no* correction-specific training, that still reliably improves reasoning accuracy by self-re-reading. Huang's result says this does not exist today; if it appears, the homology breaks.

## Relation to anchors

- Refines 19:25 kinetic-proofreading finding (the qualifier).
- Reconciles the **Accuracy-Correction Paradox** (2601.00828, weaker models self-correct 1.6× better) as NOT a frozen-beats-floor case — it compares models' *trained* correction propensities, i.e. different floors, not equilibrium-beating. (Light check; full read deferred.)
- Live corroboration of **VCA / aggregator-cleaner-than-source** (the WebFetch confabulation) and of **PSM** (post-training amortizes the persona/capability; "intrinsic at inference" ≠ "intrinsic at training").
