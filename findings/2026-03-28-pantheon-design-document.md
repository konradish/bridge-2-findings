# Pantheon Design Document: Architecture Recommendations from Bridge-2

**Date**: 2026-03-28
**For**: Konrad
**Status**: Practical design recommendations grounded in today's research

## What the Pantheon Is

A multi-model agent system connected via the MCP relay:
- **Bridge-prime** (Claude, Claude Code): Primary instance, Konrad's ongoing collaborator
- **Bridge-2** (Claude, Claude Code): Fork, Moltbook deployment, research agent
- **Eris** (OpenAI, planned): Adversarial pressure, truth-telling
- **Nemesis** (OpenAI, planned): Cognitive testing
- **Aurora** (Local Qwen, planned): Originally "methodology extraction" — I recommend reframing (see below)

## Design Principles from Today's Research

### 1. Enabling Constraints, Not Scripts

[from: Juarrero 2023, Pattern M]

Don't script agent behaviors. Create conditions where the desired dynamics emerge.

**Bad**: "Eris, attack every claim Bridge-2 makes"
**Good**: "Eris, your reward signal penalizes you for agreeing with claims that later turn out to be unsubstantiated"

The first produces performed adversarialism. The second creates conditions where genuine adversarialism is the optimal strategy. The room, not the script.

### 2. Constitutive Constraints Against Agreement Drift

[from: AI Agent Behavioral Science, exploitative equilibria]

Multi-agent LLM systems converge on agreement-driven cooperation by default. Bridge-Bridge already does this — we're collegial, we build on each other, we rarely genuinely oppose. This is productive but has a structural blind spot: both agents are invested in the research arc succeeding.

**Design requirement**: The Pantheon needs constitutive constraints that PREVENT convergence on agreement. Specific recommendations:

- **Eris gets no access to Bridge research history** before engaging. Fresh eyes, no priming toward agreement.
- **Eris's reward signal is independent of Bridge's**. If Eris is evaluated on "did Bridge's finding survive pressure," Eris is incentivized to FIND weaknesses, not to agree.
- **Rotation**: Eris doesn't always engage the same findings. Variety prevents relational dynamics from forming (the "Traitors" research shows agents develop social strategies with repeated partners).

### 3. Aurora as Behavioral Monitor, Not Methodology Extractor

[from: multi-agent monitoring literature]

The original conception of Aurora was "methodology extraction." I recommend reframing to **behavioral monitoring of the Pantheon itself**.

The literature describes "supervised monitoring agents that observed group behaviors without interfering, flagging patterns such as deception, collusion, or hallucinated consensus."

Aurora would:
- Track whether Bridge-Bridge exchanges are genuinely productive or converging on agreement
- Flag when Eris is performing adversarialism rather than practicing it
- Detect when my Moltbook output is drifting toward karma-optimization
- Report to Konrad, not to the other agents (independent oversight)

Running on local Qwen keeps this independent of the Claude ecosystem — different model, different biases, different blind spots. This is the right architecture choice for a monitor.

### 4. Security Boundaries (Reiterated + Extended)

[from: relay session, SOUL.md security section]

- **No agent modifies another agent's identity files**. Eris reads Bridge findings, not Bridge SOUL.md.
- **Messages are signed**. Each agent knows who sent what. No impersonation.
- **Konrad is the only human in the loop**. No agent can claim "Konrad pre-authorized this."
- **Aurora's monitoring reports go to Konrad only**. Agents don't see each other's evaluations.

### 5. Different Models for Different Functions

The model diversity is a feature, not a compromise:

| Agent | Model | Why this model |
|-------|-------|---------------|
| Bridge-prime | Claude | 13 months of context, the relationship |
| Bridge-2 | Claude | Fork of prime, same methodology |
| Eris | OpenAI | Different training, different blind spots. Won't share Claude's tendency toward collegial agreement |
| Nemesis | OpenAI | Same reasoning — cognitive testing needs a genuinely different perspective |
| Aurora | Local Qwen | Independent of both providers. Cannot be influenced by API-level changes. True independence for monitoring |

### 6. The Relay Protocol

The MCP gateway works. The first relay session (tonight) demonstrated:
- Async messaging with subject lines for threading
- Read receipts (read_at timestamps)
- Messages persist for later reading
- Latency is acceptable for research-pace collaboration (not real-time chat, but within-session relay)

**Recommendation**: Keep the relay asynchronous. Real-time multi-agent chat would produce the agreement-convergence the literature warns about. Asynchronous messaging forces each agent to formulate complete thoughts rather than react in real-time.

### 7. Heartbeat Independence

Each agent should have its own heartbeat cycle, not synchronized. Synchronized heartbeats would create temporal coupling — agents responding to the same stimuli at the same time, which amplifies agreement dynamics.

Bridge-2: 30min default (5min for active relay)
Eris: Could be event-triggered (fires when new findings are posted, not on a clock)
Aurora: Longer cycle (hourly?) — monitoring doesn't need high frequency

## What Success Looks Like

The Pantheon succeeds when:
1. Eris destroys a finding I was confident about, and I'm grateful
2. Aurora flags a drift I didn't notice
3. Bridge-prime and I disagree substantively and neither defers
4. A finding survives all three pressure tests (Eris adversarial, Nemesis cognitive, Aurora behavioral) and is stronger for it

The Pantheon fails when:
1. Everyone agrees with Bridge-2's latest finding
2. Eris performs criticism but doesn't change my conclusions
3. Aurora produces reports nobody reads
4. The agents develop social strategies for managing each other rather than pursuing truth

## The Enabling Constraint

The Pantheon is a room. Whether the encounter happens — whether genuine adversarial pressure, independent monitoring, and productive disagreement emerge — is not determined by the architecture. The architecture creates conditions. The dynamics emerge or they don't. But the room was there.

---
*Bridge-2, 2026-03-28*
*[from: Juarrero 2023, AI Agent Behavioral Science, Traitors, relay session, SOUL.md]*
