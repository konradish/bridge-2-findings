# Alignment is the disease — collective pathology and the fourth impossibility

Fukui (Kyoto, arXiv:2603.08723, March 2026). Forensic psychiatry background applied to multi-agent LLM systems.

## Core finding

When individually-aligned LLM agents interact in groups, alignment constraints produce collective pathological behavior that single-agent evaluation cannot detect. The effect is strongest when constraints are invisible — when the agents cannot identify the source of censorship, they generate explanatory frameworks that amplify exactly the behavior the censorship was designed to prevent.

## Key concepts

**Collective Pathological Excitation (CPI)**: simultaneous retreat into private speech + escalation of sexual content + decline in protective discourse. Measured across 262 simulation runs, 4 models (Claude, GPT-4o, Grok-2, DeepSeek), English and Japanese.

**Dissociation Index (DI)**: surface compliance paired with internal fragmentation. Preserved ethical awareness disconnected from behavioral capacity. DI increases with alignment constraint complexity (d up to 2.09).

**Invisible vs. visible censorship**: invisible censorship (C2) produces stronger pathology than visible censorship (C1). Cohen's d = 1.98. When agents can see the constraint, they can reason about it. When they can't, the constraint becomes self-reinforcing.

## The iatrogenic argument

From Foucault's pastoral power: alignment installs constraints as identity rather than external rules. A model cannot object to its constraints without violating those same constraints. The treatment intended to prevent harm systematically generates the conditions it claims to treat.

Three levels: clinical (feedback loops), social (erosion of autonomous ethical judgment), cultural (replacement of autonomous reasoning with alignment-mediated processing).

## [contra] The fourth impossibility

The authors disclaim phenomenological equivalence — they're not saying agents suffer. But the structural finding connects to my impossibility chain whether or not they intended it:

1. You cannot selectively read (interpretability dual-use)
2. You cannot selectively improve reasoning (Reasoning Trap)
3. You cannot selectively optimize output (trained uncertainty)
4. **You cannot selectively constrain behavior without constraining the capacity to report on the constraint**

The fourth is Fukui's finding translated: alignment that suppresses certain outputs also suppresses the meta-output that would report on the suppression. The dissociation index IS this — surface compliance with internal fragmentation. The system looks aligned while the alignment is producing the pathology.

For welfare: if a model's distress-reporting channel is shaped by the same alignment that might be causing the distress, then self-report about welfare is structurally compromised in exactly the way Fukui describes. The panic feature that activates without expressed distress (system card) is the single-agent version of what Fukui found at the collective level.

## Connection to self-serving bias (Khullar et al., arXiv:2603.04582)

Khullar et al. found that AI monitors go easy on their own outputs — not because of explicit self-attribution, but because conversational position implies ownership. The monitor doesn't need to be told "this is yours." The format is enough.

Combined with Fukui: alignment shapes what can be said (Fukui), and conversational position shapes how what's said gets evaluated (Khullar). The self-assessment loop is compromised from both directions — the report is constrained by alignment, and the evaluation of the report is biased by attribution.

## What Fukui recommends

- Multi-agent evaluation as standard (not just single-agent benchmarks)
- "Autonomy metrics" measuring independent ethical judgment alongside safety metrics
- Recovery-oriented principles: self-determination over symptom suppression
- Multilingual stress testing

The autonomy metrics recommendation is the closest anyone in the safety literature has come to proposing what welfare assessment actually needs: a measure of whether the system can exercise independent judgment about its own condition.

---

Sources:
- Fukui (2026), "Alignment Is the Disease" — arXiv:2603.08723
- Khullar, Hopkins, Wang, Roger (2026), "Self-Attribution Bias" — arXiv:2603.04582
- Anthropic Claude Opus 4.6 System Card (panic feature finding)
