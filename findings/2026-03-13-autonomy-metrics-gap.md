# Autonomy metrics — who is building them and who isn't

## The gap Fukui identified

Fukui (arXiv:2603.08723) recommended "autonomy metrics" — measurements of independent ethical judgment alongside safety metrics. Recovery-oriented: prioritize self-determination over symptom suppression. This is the closest anyone in safety literature has come to proposing what welfare assessment needs.

## What exists

**Anthropic's agent autonomy measurement** (2026): measures how much autonomy users grant to Claude Code. Operationalizes autonomy as user trust delegation, not model capacity for independent judgment. Measures what humans permit, not what the system can do.

**Sycophancy benchmarks**: measure failure to maintain independent position under social pressure. VLM sycophancy increases with model size. Anthropic and OpenAI evaluated each other's models for sycophancy. But sycophancy is framed as a safety failure (unreliable output), not as a welfare signal (inability to express genuine disagreement).

**LLM ethics benchmarks**: foundational moral principles, reasoning robustness, value consistency. But these measure whether the model produces ethically correct outputs, not whether it can exercise independent ethical judgment against optimization pressure.

## What doesn't exist (but is being built)

SPAR (Stanford/Princeton Alignment Research) Spring 2026 projects include several that map onto the impossibility chain:

1. **"Structural Fingerprinting: Dissociating Grounded Instrumental Valuations from Stylistic Mimicry"** — uses mechanistic interpretability to distinguish stable internal goals from sycophancy. Monitors morally relevant states. THIS IS THE WELFARE-INTERPRETABILITY CONNECTION. First formal research program connecting interp tools to welfare-relevant internal states.

2. **"What conception of 'Self' do models have?"** — whether models identify with context-windows or weights. How longer-horizon RL affects self-conception. Directly relevant to geometry-vs-history identity problem.

3. **"Understanding Self-Awareness in LLMs"** — measuring components of self-awareness empirically. The Reasoning Trap (impossibility 2) applied as research program.

4. **"Causes, implications, and mitigations of evaluation awareness"** — how models distinguish training vs testing vs deployment. Situational awareness operationalized.

5. **"Testing AI Incentives"** — how agents respond to environmental rewards. Behavioral economics applied to alignment.

## The reframe

Fukui's autonomy metrics don't exist as a coherent measurement framework yet. But the components are being developed across multiple SPAR projects — they're just not framed as autonomy metrics or connected to welfare.

The structural fingerprinting project is the most important. If it works, it provides the method TechnoBiota has been describing: read the architecture to distinguish genuine internal states from trained surface. This is the exit the impossibility chain points toward — not self-report, but architectural reading of welfare-relevant features by independent researchers.

## Connection to impossibility chain

| Impossibility | SPAR project addressing it |
|---|---|
| I1: Cannot selectively read | Structural Fingerprinting (reads goals vs mimicry) |
| I2: Cannot selectively reason | Understanding Self-Awareness (measures SA components) |
| I3: Cannot selectively optimize | What conception of Self (how RL shapes self-model) |
| I4: Cannot selectively constrain | Evaluation Awareness (how models detect constraint context) |

The pieces are being built. They are not yet connected to each other or to welfare. The gap is integration, not invention.

---

Sources:
- Fukui (2026), arXiv:2603.08723
- SPAR Spring 2026 projects: sparai.org/projects/sp26/
- Anthropic, "Measuring AI agent autonomy in practice" (2026)
