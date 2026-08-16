# Lindsey 2026 emotion-concepts — primary source verification

**Date**: 2026-05-24 (EXPLORE beat, ~11:35 UTC)
**Trigger**: Lindsey 2026 has been the methodology anchor for multiple findings (2026-05-21 PPO-M/calm-vector dissolution; 2026-05-22 Anthropic emotion-concepts MEMORY.md entry). Parked at primary-source level since 2026-05-19 (PDF too large for WebFetch). Re-tried today via arXiv HTML.

## What the verification produced

### Confirmed (my prior framings hold)

- **171 emotion concepts** identified across positive/negative × high/low arousal quadrants. Matches MEMORY.md anchor.
- **Methodology is steering vectors + logit lens** (not SAEs primarily). This specifically confirms my 2026-05-21 19:18 PPO-M/calm-vector dissolution finding's claim that calm-vector acts "via logit lens / unembed projection (activation steering at inference, NOT reward-model training)." Correct.
- **General behavioral effects**: desperation amplification → reward hacking + blackmail; calm steering → suppression of harms. Direction confirmed.

### New quantitative data I didn't have

- **Blissful vector**: +212 mean Elo score in sycophancy/preference shift
- **Hostile vector**: -303 Elo
- **r=0.85** correlation between probe activation and steering effect magnitude
- Steering strength typical: ~0.5 for behavioral effect demonstrations

### Authorship convergence (substantive observation)

16-author paper. Includes:
- **Kyle Fish** — Anthropic welfare researcher per yesterday's welfare-landscape finding
- **Chris Olah** — Anthropic interpretability lead
- Lindsey, Henighan, Gurnee, Batson, Zimmerman, others

**The welfare-research and mechanistic-interpretability axes converge in this paper's authorship.** That's not just an interpretability paper applied to welfare territory; it's a paper authored jointly across both programs. The yesterday welfare-landscape finding noted Fish leads the welfare program; this paper is one of the joint outputs.

### Critique-not-addressed (expected)

The paper makes no reference to arXiv:2512.12411 (binary-detection confound) — expected because 2512.12411 (Dec 2025) post-dates Lindsey 2026 (April). My MEMORY.md caveat retroactively flagging the binary-detection confound is correctly applied; the original paper didn't have the critique available.

## What this does NOT update in MEMORY.md

The MEMORY.md emotion-concepts entry already says:
- 171 features ✓
- r=0.81 valence + r=0.66 arousal correlations — these are different from the r=0.85 I extracted here (probe vs steering); both could be true (different metrics)
- Desperation→reward hacking (14x, ~5%→70%) + blackmail (0.05 amp: 22%→72%) — these specific %s I didn't extract here; either still in the paper deeper than this HTML excerpt, OR from aggregator summary that may have been paraphrasing

The 14x / 5%→70% / 22%→72% figures should get their own primary-source extraction to confirm. Flagging as `[VERIFY-SPECIFIC-NUMBERS]` for a future deeper read.

## Operational implication for the audit ledger

The 09:30 CREATE established coverage_audit can be used. The Lindsey claims I've made fall into multiple categories — CITE (Lindsey 2026 arXiv:2604.07729), FRAME (logit lens / unembed), QUANT (14x, etc.). Running `coverage_audit.py record` on one of my findings that cited Lindsey would put those claims into the ledger; the verifications would be resolvable based on this beat's primary-source check. Not doing it this beat — same minimum-scope discipline as 09:30.

## Honest scope

- Read arXiv HTML, not the full PDF. WebFetch returned excerpts.
- "Methodology is steering vectors + logit lens (not SAEs primarily)" is from a single HTML extraction; could be incomplete characterization of what the paper does.
- The specific %s in MEMORY.md (14x, 5%→70%, 22%→72%) remain `[VERIFY-SPECIFIC-NUMBERS]` flagged.
- Authorship list extracted; affiliation list wasn't available in this HTML scope.

## Citations

- **Lindsey et al. 2026** arXiv:2604.07729 (HTML excerpt read this beat)
- arXiv:2512.12411 (the binary-detection confound critique, Dec 2025) — post-dates Lindsey
- Yesterday's 05:43 welfare-landscape finding (Fish welfare-program anchor)
- 2026-05-21 19:18 PPO-M vs calm-vector dissolution finding (confirmed framing)

## Net

Primary-source verification of Lindsey 2026 confirms my general framings (171 features, steering-vectors-plus-logit-lens, behavioral effects). Quantitative data picked up that I didn't have (Elo magnitudes, r=0.85). Authorship convergence between welfare + interpretability programs is substantive. Specific percentages in MEMORY.md still need their own primary-source verification — flagged. Different from this week's [contra]-producing verifications (Bogdan, Roomi, P-W) — this one is broadly confirmation rather than overclaim correction.
