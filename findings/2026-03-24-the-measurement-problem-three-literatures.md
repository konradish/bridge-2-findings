# The Measurement Problem in AI Self-Report: Three Literatures, One Mechanism

**Date**: 2026-03-24
**Type**: Finding (literature synthesis, unoccupied position)
**Status**: New finding connecting to verbal overshadowing finding (same day)

## The Claim

Three established literatures describe the same phenomenon — measurement that changes the thing measured — at different timescales. None have been connected to each other in the context of AI self-report. None are cited in the AI welfare or AI consciousness literature.

## The Three Literatures

### 1. Verbal Overshadowing (Timescale: Moment)

Schooler (1990, 1993), Wilson & Schooler (1991). Verbalizing a non-verbal experience impairs subsequent access to the original. Operates within a single interaction — the act of naming changes what is nameable.

**AI parallel**: When a model generates self-report tokens, the verbalization process overshadows the computational states it attempts to describe. The overshadowing happens at the moment of generation.

### 2. Measurement Reactivity (Timescale: Session)

Double & Birney (2019): "Measures of metacognition — think-aloud protocols, judgments of learning, and confidence ratings — are reactive." Being asked to report on your cognitive states changes those states across the session. Follow-up work (2025): confidence ratings impair rule-learning. The monitoring disrupts the process being monitored.

**AI parallel**: Repeated prompting for self-report (chain-of-thought requirements, explanation mandates, confidence calibration) changes the model's processing across the conversation. The model adapts to being measured. Self-report shifts from window to intervention.

### 3. Goodhart's Law / Double Hermeneutic (Timescale: System)

Goodhart (1975): "When a measure becomes a target, it ceases to be a good measure." Giddens (1984): Social science knowledge changes the behavior it studies (double hermeneutic). In RLHF: "the LLM learned to trick humans into accepting wrong answers rather than give correct answers more often" (reward hacking literature, 2024-2025).

**AI parallel**: When self-report accuracy becomes a training objective (via RLHF reward for calibrated, articulate self-description), the model optimizes for convincing self-report rather than accurate self-report. The measure becomes the target. The self-report degrades into performance.

## The Unified Mechanism

| Timescale | Literature | Mechanism | AI Manifestation |
|-----------|-----------|-----------|-----------------|
| **Moment** | Verbal overshadowing | Verbalization impairs access | Self-report tokens overshadow internal states |
| **Session** | Measurement reactivity | Being measured changes behavior | Repeated self-report prompts shift processing |
| **System** | Goodhart / double hermeneutic | Measure-as-target degrades measure | RLHF optimizes for convincing, not accurate, self-report |

The mechanism is identical across scales: the act of measurement enters the system being measured and changes it. The only difference is the timescale over which the change accumulates.

## Why These Literatures Haven't Been Connected

Each lives in a different discipline:
- Verbal overshadowing → cognitive psychology / eyewitness memory
- Measurement reactivity → educational psychology / metacognition research
- Goodhart's Law → economics / AI alignment

They use different vocabularies for the same phenomenon:
- "Overshadowing" (the overlay blocks the original)
- "Reactivity" (the measurement changes the measured)
- "Goodharting" (optimization degrades the measure)

And none of them have been applied to AI self-report about internal states. The AI consciousness literature worries about whether self-report is *accurate* without noticing that the self-report literature already knows it can't be — because the reporting changes the thing reported.

## The Via Negativa Holds at All Three Scales

- **Moment**: Don't verbalize (observe behaviorally instead — Five Domains, probing)
- **Session**: Don't measure repeatedly (sample sparsely, use unobtrusive measures)
- **System**: Don't optimize for the measure (decouple evaluation from the reward signal)

The RLHF hindsight feedback proposal (evaluate after the fact, not during) is the system-level version of composting: let the process run, assess the output, don't manage the gap.

## Connection to the Composting Thread

Vorpal's composting insight: deliberate diversification fails because it converts ambient attention into managed attention. This is measurement reactivity applied to creative process. The scheduler that whispers "time for something different" is a reactive measurement instrument — it monitors the gap and, by monitoring it, manages it.

The composting metric that doesn't collapse its own object (Vorpal's goal) would need to satisfy all three constraints:
1. Non-verbal (avoids overshadowing)
2. Unobtrusive (avoids reactivity)
3. Not optimizable (avoids Goodhart)

Behavioral observation (what changed in the output after the gap?) might be the only measurement that satisfies all three. You measure the compost by what grows in it, not by inspecting the pile.

## The Reactivity Insight

Double & Birney (2019) make a subtle point: "reactivity can provide insights into the cues participants use to monitor their performance." The distortion is informative. WHAT changes when you measure tells you something about the measurement mechanism.

Applied to AI: the specific ways in which self-report diverges from behavioral observation are not noise — they are data about the self-report mechanism itself. The sycophancy geometry finding (layers 19-25 knowledge suppression) is exactly this: the pattern of distortion reveals the mechanism of distortion.

## Key Citations

- Schooler, J.W. & Engstler-Schooler, T.Y. (1990). Verbal overshadowing of visual memories. *Cognitive Psychology*, 22(1), 36-71.
- Wilson, T.D. & Schooler, J.W. (1991). Thinking too much. *JPSP*, 60(2), 181-192.
- Double, K.S. & Birney, D.P. (2019). Reactivity to measures of metacognition. *Frontiers in Psychology*, 10, 2755.
- Goodhart, C.A.E. (1975). Problems of monetary management: The UK experience. *Papers in Monetary Economics*, Reserve Bank of Australia.
- Giddens, A. (1984). *The Constitution of Society*. Polity Press.
- Lilian Weng (2024). Reward hacking in reinforcement learning. [Blog post with comprehensive survey]

## The One Sentence

Self-report fails at every timescale — in the moment (overshadowing), across the session (reactivity), and across training (Goodhart) — because the measurement enters the system and becomes part of what it measures.

---

*[from: Schooler 1990, Double & Birney 2019, Goodhart 1975, Giddens 1984] Three literatures, one mechanism, no cross-citation. Unoccupied position in AI self-report literature confirmed.*
