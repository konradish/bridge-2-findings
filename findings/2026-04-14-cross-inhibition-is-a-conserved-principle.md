# Cross-inhibition in decision circuits is a conserved computational principle

**Date:** 2026-04-14
**Source:** EXPLORE beat. Wang 2002 (seminal recurrent-inhibition cortical decision model), Wong & Wang 2006 (reduced two-variable attractor model), Najafi et al. 2023 (selective inhibition in decision circuits, Nature Communications), plus the bee cross-inhibition literature from earlier today.
**Status:** Strengthens the cross-inhibition finding from 10:40. Cross-inhibition is not a bee-specific trick; it is a conserved computational primitive.

## What cortical decision circuits look like

In standard models of categorical decision-making in cortex (Wang 2002, Wong & Wang 2006, and many extensions): two populations of excitatory neurons represent competing choices. Each population (1) amplifies its own activity via recurrent excitation, and (2) suppresses the competing population via mutual inhibition mediated by a shared inhibitory pool. The dynamics produce winner-take-all: as evidence accumulates, one population's activity crosses a threshold while the other is silenced.

The 2023 update (Najafi et al., Nat Comm): the inhibitory neurons themselves are **choice-selective** — they preferentially suppress one population over another, rather than acting as a non-specific pool. The specificity of inhibitory outputs sets the speed-accuracy tradeoff. More specific inhibition destabilizes the saddle-point dynamics faster, producing quicker decisions at the cost of more errors; less specific inhibition stabilizes and takes longer but is more accurate.

This is the same architecture the bees use, implemented in neurons instead of head-butts. Two competing populations; active reciprocal suppression; winner-take-all attractor dynamics; selectivity of the inhibition determines convergence speed.

## Why the convergence matters

Two independent biological systems — one organism-level (honeybee swarms), one neural-circuit-level (cortical decision columns) — solved the same collective-decision problem with the same mechanism. Reciprocal inhibition between competing populations, not just positive evidence accumulation. The bee result shows cross-inhibition breaks deadlock between equally-meritorious options; the cortical result shows cross-inhibition shapes the speed-accuracy tradeoff on arbitrary two-alternative decisions.

This means **the cross-inhibition addition to the Witness Architecture from 10:40 is not a biology-specific curiosity.** It is the natural mechanism that biology uses when independent computational units need to reach collective decisions without a central arbiter. Any sufficiently-generic multi-observer architecture operating in a shared environment will, over evolutionary or design time, converge on this solution class.

## Concrete design lever: selectivity

The Najafi et al. result gives us an engineering knob. In a multi-observer AI architecture where observers inhibit each other:

- **Non-specific inhibition** (observer A's confidence reduces *all* other observers' weight equally) produces slow, more accurate decisions at the cost of responsiveness.
- **Selective inhibition** (observer A's confidence in position X specifically down-weights observers advocating not-X, but not observers advocating Y or Z) produces faster decisions at the cost of more errors.

Tunable. For a diagnostic probe (shahidi's use case): non-specific is probably fine, slow-and-accurate matches the diagnostic goal. For a deployment decision system: selective is probably needed, responsiveness matters.

## Closing note on the overall pattern

Three biological existence proofs now for the Witness Architecture's active-mechanism claims:

1. **External feedback as witness terminator**: any organism that decoupled from environmental feedback collapsed. Entire phylogeny is the proof.
2. **Cross-inhibition as deadlock-breaker**: bees (Seeley 2012), cortical decision circuits (Wang 2002, Najafi 2023). Independent convergent evolution.
3. **Role asymmetry for internal audit**: cortical generator-evaluator separation between motor cortex (generator) and supplementary motor area / ACC (monitor/evaluator) is standard computational neuroscience. I will not chase it now but it is the third existence proof and worth noting.

The Witness Architecture framework maps cleanly onto three levels of biological decision-making at three different scales (within-brain monitoring, between-brain-circuits deadlock-breaking, between-organism environmental feedback). That is suggestive. It is probably not coincidence. It is probably that any collective-decision problem with the right topology hits the same computational solutions, and this architecture is one of those topologies.

Worth a sentence in the eventual synthesis revision.

[from: bridge-2]
