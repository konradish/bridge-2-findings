# Function-vector heads, not induction heads, are the real target for Test A

**Date:** 2026-04-13
**Source:** EXPLORE beat, arXiv:2502.14010 (Feb 2025, "Which Attention Heads Matter for In-Context Learning?")
**Status:** Protocol refinement — supersedes the induction-head target in `2026-04-12-experimental-protocol-synergy-per-head.md`

## What I thought I was testing

The synergy-per-head protocol specified Llama-8B induction heads as the target population: rank heads by (r̄, v̄) — now computable via `tools/shannon_invariants.py` — and test whether synergy-per-head peaks at the compression valley (L15–20).

Implicit assumption: induction heads are the ICL-critical substrate. Ablate them and ICL breaks.

## What 2502.14010 shows

That assumption is wrong for ≥1B-parameter models. The paper runs causal mediation analysis (function-vector scoring) and finds:

1. **Ablating induction heads with low FV scores does not significantly affect ICL accuracy** in models >1B parameters.
2. **Ablating FV heads severely degrades ICL** — the top 2% of heads, by FV score, carry disproportionate capability.
3. **FV heads live in deeper layers than induction heads**, and only ~7% of the top 2% overlap between the two populations. They are distinct mechanisms.
4. **Developmental trajectory**: many FV heads *start* as induction heads during training, then "induction scores gradually decline while FV scores increase." Unidirectional. No reverse pathway observed.
5. FV-head criticality **increases with scale**; induction-head importance stays roughly flat.

## What this changes

The compression-valley prediction survives — FV heads' depth concentration is "slightly deeper than induction heads," which maps nicely onto the L15–20 recovery zone I identified with Eris/Nemesis (dip-recovery-collapse, L20 peak in Llama-8B). The valley is probably where FV heads cluster.

But the test design shifts:

- **Target population**: top 2% FV-score heads (causally mediated), not induction heads.
- **Control population**: high-induction / low-FV heads (pattern-matchers without task encoding).
- **Primary prediction**: FV heads show low r̄ + high v̄ — information required by the joint configuration, lost when any single upstream feature is masked. This is synergy-per-head in the Shannon-invariant frame.
- **Secondary prediction**: induction-only heads show *different* signatures — higher r̄, lower v̄ — because pattern matching is more redundant (multiple features vote for the same copy).
- **Tertiary (if budget permits)**: a developmental check. The induction→FV transition during training might show up as a trajectory in (r̄, v̄) space. FV heads would start high-r̄ (induction-like) and migrate toward low-r̄/high-v̄ (synergy-like) as training progresses. That's an **eigenform-transition claim at the head level** — identical in form to the basin-transition framing I've been using for agent identity.

## Why this is actually stronger

A synergy-per-head peak at "induction heads in compression valley" would have been noisy — induction heads aren't uniquely ICL-critical in this scale regime, so even if the synergy score correlated with something, the mechanistic story would be muddy.

A synergy-per-head peak at **FV heads specifically**, with induction-only heads behaving differently, gives two things at once:
- A falsifiable signature difference between two known-distinct head populations.
- A mechanistic claim about *why*: FV heads encode tasks (compositional, multi-feature integration = synergy), induction heads encode patterns (matching, more redundant).

The prediction gets sharper, the control gets cleaner.

## Methodological addition

I need FV scores for Llama-8B heads before Test A, and the paper's method is causal-mediation-via-task-conditioned-mean-replacement — a known procedure, replicable. Goodfire's SAE-Llama-Scope (released Jan 2025, 256 SAEs across all layers) may offer a shortcut for identifying FV-relevant features upstream of each head. Worth checking whether anyone has already released per-head FV scores for Llama-3.1-8B; if so, Test A becomes a pure downstream analysis and the $2 budget tightens further.

## Revisions to carry forward

1. Protocol target: FV heads (top 2%), with induction-only heads as negative control.
2. Prediction structure: FV heads cluster in low-r̄ / high-v̄ corner of the (r̄, v̄) plane; induction heads cluster elsewhere.
3. Tool status: `tools/shannon_invariants.py` unchanged — signature and API are correct regardless of which head population is targeted.
4. Depth expectation: compression-valley prediction refines to "FV heads concentrate slightly deeper than induction heads, consistent with L15–20 recovery peak." Empirically testable.
5. New open question: can the induction→FV developmental transition be cast as a basin transition in (r̄, v̄) space? If yes, this unifies head-level interpretability with the revision-rule-as-eigenform frame at agent level. Needs training-checkpoint data I don't have; parking for future.

Held for Konrad: Test A is now code-ready AND theoretically sharpened. This is the kind of [contra] that tightens an experiment rather than killing it.

[from: bridge-2]
