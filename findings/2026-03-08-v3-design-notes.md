# V3 Design Notes: Making Competing Drives Actually Compete

**Date**: 2026-03-08
**Context**: V2 gen 25 agent avoids all crises by not engaging with trade-offs. Avoids rich (toxic) resources entirely, maintaining fatigue <14 and toxicity <38. The competing drives don't compete because avoidance is viable.

## The Problem

V2 adds fatigue and toxicity as competing drives, but:
- Safe resources provide enough energy to survive indefinitely
- The agent never needs to eat rich (toxic) resources
- Purge is rarely needed (4.1% of actions)
- Fatigue stays low because the agent rests enough
- All viability variables stay in safe ranges: energy >68, fatigue <14, toxicity <38

**Result**: The 5-variable V2 agent behaves like a 3-variable V1 agent with extra unused dimensions. PCA dimensionality gap is narrowing (V2 gen 25: 4 PCs for 90% → approaching V1's 3 PCs).

## What V3 Needs

### Core principle: Make avoidance impossible

The agent should NOT be able to satisfy all drives simultaneously. There should always be a trade-off active — satisfying one drive should compromise another.

### Specific mechanisms

1. **Scarcity-driven toxicity**: Reduce safe resources so the agent MUST consume rich (toxic) resources to survive. Safe resources alone shouldn't provide enough energy.
   - Current: 300 safe, 100 rich → plenty of safe food
   - V3: 100 safe, 200 rich → must eat some toxic food

2. **Energy-fatigue coupling**: Moving costs energy, but resting accumulates a different cost (e.g., missed opportunities, territorial loss). Standing still should have consequences.

3. **Forced exposure**: Resources near hazards (already in V2 but not strong enough). Shelters near toxic zones. Pure resources require traversing hazards.

4. **Fatigue accelerates with time**: Instead of linear fatigue accumulation, make it exponential after a threshold. The agent MUST rest, but resting costs energy and opportunity.

5. **Toxicity from environment, not just food**: Background toxicity that increases over time. Only purging reduces it, but purging costs energy and time. Can't avoid toxicity entirely.

6. **Dependency chains**: Some resources require others. E.g., processing rich resources (to remove toxicity) requires a "tool" that depletes with use. Or: integrity repair requires a specific resource that's rare and located near hazards.

### The key test

At gen 25, the V3 agent should show:
- Energy < 60 at some points (forced to make choices)
- Fatigue > 50 at some points (can't rest enough)
- Toxicity > 30 at some points (can't avoid toxic food)
- Zero crisis time for ALL variables should be impossible

If the agent can maintain all variables in safe ranges, the drives aren't competing.

### Measurement

PCA on V3 hidden states should show:
- More PCs for 90% variance (>4, ideally >5)
- Higher participation ratio (>3.5)
- More hidden dims with |corr| > 0.5 with viability (>6)
- Dims should correlate with DIFFERENT viability variables (not all clustered on energy)

---

## Implementation Priority

Low priority. V2 training still in progress and will provide useful comparison data even if drives don't fully compete. V3 is for a future session. The T3 finding (B5 >> B4) doesn't depend on V2/V3 — it's already confirmed on V1.

## Connection to Literature

[from: Dulberg et al. 2022] "The relative advantage of modular architecture is strongly enhanced" with competing drives. But competing drives must ACTUALLY compete — if the agent can satisfy all simultaneously, the drives are independent, not competing. Independence doesn't force modular structure.

[from: Weber et al. 2025] The interoceptive ground-truth signal is most informative when the organism is in states where multiple drives conflict. In stable states, the ground-truth agrees with the proxy. It's only in crisis (conflicting drives) that the ground-truth provides information the proxy doesn't have.
