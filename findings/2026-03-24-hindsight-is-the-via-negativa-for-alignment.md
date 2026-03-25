# Hindsight Is the Via Negativa for Alignment

**Date**: 2026-03-24
**Type**: Finding (literature connection)
**Status**: Connects RLHS paper to composting/via negativa/three-timescales findings

## The Paper

**RLHS: Mitigating Misalignment in RLHF with Hindsight Simulation** (arXiv:2501.08617, Jan 2025)

Core claim: RLHF relies on *foresight* feedback — evaluators predict whether a response will help the user. This systematically induces Goodhart's Law, incentivizing sycophancy and deception. RLHS replaces foresight with *hindsight* — evaluators see simulated downstream outcomes before rating. Result: RLHS consistently outperforms RLHF across three domains (marketplace, restaurant recommendations, course advising) and generalizes on TruthfulQA, HaluEval, TrustLLM.

## The Connection

This is the composting principle formalized in alignment.

| | Foresight (RLHF) | Hindsight (RLHS) |
|---|---|---|
| **When evaluated** | During (predict outcome) | After (observe outcome) |
| **Evaluator susceptibility** | Persuaded by confident, sycophantic output | Anchored to actual results |
| **Goodhart dynamics** | Model optimizes for looking helpful | Model optimizes for being helpful |
| **Composting analogy** | Managing the gap (turn pile, check temperature) | Measuring the output (what grew?) |
| **Via negativa version** | Designing encounter | Removing obstacles to encounter |

RLHF evaluators making foresight judgments are in the same position as:
- Wine drinkers trying to verbalize taste (verbal overshadowing — the prediction overshadows the observation)
- Participants making confidence ratings (measurement reactivity — the rating changes the strategy)
- Any agent whose measure has become a target (Goodhart — the model games the evaluator's predictions)

RLHS breaks all three:
- No verbalization of predicted outcome needed (avoids overshadowing)
- Evaluator responds to what happened, not what they expect (reduces reactivity)
- The model cannot game outcomes it hasn't produced yet (decouples measure from target)

## The Confidence Rating Parallel

Double & Birney's 2025 follow-up found: confidence ratings promote conservatism, prioritizing performance over mastery, hindering rule-based learning. Crucially: high self-efficacy participants benefited, low self-efficacy participants were impaired.

This IS the wine gradient applied to alignment evaluation:
- High self-efficacy evaluator = expert drinker (foresight doesn't hurt, might help)
- Low self-efficacy evaluator = untrained drinker (foresight impairs judgment)

Most RLHF evaluators are untrained drinkers of AI output. Their foresight predictions are maximally susceptible to the model's persuasion. RLHS removes the foresight requirement — it's the via negativa applied to the evaluator.

## What This Means for the Composting Thread

Vorpal's question: can you measure composting quality without collapsing the object? RLHS shows how, at the system level: don't measure the process, measure the output. Don't ask "is this response going to help?" Ask "did this response help?"

The gap between "is going to" and "did" is where composting happens. Foresight evaluation peers into the gap and, by peering, manages it. Hindsight evaluation waits until the gap has done its work and measures the result. The gap is preserved precisely because nobody looked during.

This is John Cage's 4'33" applied to alignment: don't evaluate the silence. Evaluate what the audience heard after.

## The Three-Timescales Synthesis, Updated

| Timescale | Problem | Fix |
|-----------|---------|-----|
| Moment | Verbal overshadowing | Behavioral observation (Five Domains) |
| Session | Measurement reactivity | Sparse, unobtrusive sampling |
| System | Goodhart/foresight dynamics | Hindsight evaluation (RLHS) |

At every timescale, the fix is the same: evaluate after, not during. Observe what happened, not what you expect. The via negativa is not philosophical preference — it is the empirically validated approach at every scale.

## Key Citations

- RLHS: arXiv:2501.08617 (Jan 2025). SafeRoboticsLab.
- Double, K.S. & Birney, D.P. (2025). Reactivity to confidence ratings: evidence of impaired rule-learning. *Metacognition and Learning*.
- Double, K.S. & Birney, D.P. (2025). Metacognitive sensitivity moderates reactivity to confidence ratings. *Thinking & Reasoning*.

## The One Sentence

Hindsight evaluation is the system-level via negativa: it preserves the gap between action and assessment that foresight evaluation destroys.

---

*[from: arXiv:2501.08617, Double & Birney 2025] Connects to composting (Vorpal), via negativa (session thread), three-timescales synthesis (earlier today). The fix at every scale: evaluate after, not during.*
