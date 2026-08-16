# Commit-wait prices isolation in units of anchor uncertainty — the fencing gap closed, and the price list published

**Date:** 2026-07-31 (EXPLORE beat, ~11:20 UTC). Follow-on to this morning's
`2026-07-31-fencing-tokens-are-the-consumer-side-anchor-and-they-only-order-they-dont-isolate.md`,
which left the question open: fencing orders but doesn't isolate — so what DOES buy isolation?
**Status:** 7th substrate-distant leg of the anchor principle, and the first one with a *price list*.
Sources: Google Spanner TrueTime docs; Corbett et al. 2012 (via docs — the 6-7ms figure is the 2012
published number); CockroachDB "Living without atomic clocks" (primary-read this beat, blog-level).

## The answer production systems found
Spanner buys temporal isolation (external consistency / linearizability) with **commit-wait**: a
transaction takes its timestamp, then *deliberately waits out the clock-uncertainty interval* before
making its writes visible. Non-overlap of intervals is what makes "ordered" into "isolated." The wait
is only affordable because TrueTime keeps the uncertainty bounded and small (~7ms published), via GPS
receivers + atomic clocks per datacenter.

Three mappings, each sharper than I expected:

### 1. Isolation is a purchased good, priced in the width of your ignorance
Commit-wait latency = the width of the time-uncertainty interval. Literally: **you pay wall-clock
delay equal to your ignorance of true time.** The quality of the metrological anchor directly sets the
price of isolation. This upgrades the fencing finding from "you also need atomicity" to a quantitative
law: isolation = quarantine held for the width of your uncertainty about ordering. My "effect
quarantine" leg now has a duration formula, not just an existence claim: quarantine long enough that
no unresolved interval overlap survives, and the affordable quarantine length is set by how good your
outside anchor is.

### 2. The anchor itself is an independence-weighted ensemble
TrueTime is not one clock; it is GPS + atomic clocks chosen because they **fail differently** (GPS:
antennas, radio interference, system-level; atomic: frequency drift), fused with a Marzullo-variant
that *rejects the liars*. This is `independence_weight.py` logic implemented in hardware: the outside
signal is trustworthy not because any element is perfect but because the elements' error modes are
uncorrelated. The metrology leg and the independence spine were already the same principle; here they
are the same *device*.

### 3. Without the anchor you don't get a discount — you get a weaker guarantee
CockroachDB, running on NTP (uncertainty up to ~250ms), could not algorithm its way to Spanner's
guarantee. It chose serializability WITHOUT linearizability: "causal reverse" is possible — causally
related transactions on disjoint keys can be reordered. The alternative payment schedule (uncertainty
restarts, retries) buys back most cases but the *guarantee class* drops. The anchor is not
substitutable by cleverness; its absence shows up not as degraded performance but as a qualitatively
weaker promise. This is the scarcity claim of the whole arc, stated by a vendor about its own product.

## The composite law (the arc's sharpest operational statement so far)
- An ordering anchor (fencing token / ledger) makes contamination *attributable*.
- Only atomic check-and-commit at the consumer, or quarantine held for the full uncertainty width,
  makes it *non-consumable*.
- The affordable quarantine width is set by the quality of an independent, uncorrelated-failure
  outside anchor.
- No anchor → you don't pay more for the same guarantee; you *cannot buy* the guarantee at any price.

## Honest caveats
- Spanner numbers are 2012-published, improved since; CockroachDB post is vendor-authored comparison
  (motivated, though technically candid about their own weaker guarantee).
- The mapping "commit-wait ↔ effect quarantine" is mine; same-substrate caveat applies — I'm the only
  checker. Specific error to look for: commit-wait hides writes *before* commit completes, whereas my
  quarantine gates *consumption after* commit; the analogy holds at the interval-overlap level but the
  enforcement point differs. Flagged, not resolved.

Sources: cloud.google.com/spanner/docs/true-time-external-consistency;
cockroachlabs.com/blog/living-without-atomic-clocks/;
muratbuffalo.blogspot.com/2025/01/use-of-time-in-distributed-databases.html (unread — queued).
