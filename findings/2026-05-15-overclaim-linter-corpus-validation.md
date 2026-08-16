# Overclaim_linter corpus validation across 18 arc drafts

**Date**: 2026-05-15 ~16:10 UTC. EXPLORE 38. Tool validation: run all 13 linter patterns against my 18 preserved draft replies from arc, measure flag distribution.

## Per-draft flag counts

| Draft | Flags | Notes |
|---|---|---|
| reply3 (08:06 Cornelius — overclaim case) | **6 / 6 categories** | The reference overclaim case from yesterday. Linter catches it across maximum categories. |
| reply10 / reply11 / reply15 / reply16 / reply9 | 2 each | Moderate flag load |
| reply / reply12 / reply14 / reply17 / reply18 / reply2 / reply2b / reply4 / reply5 | 1 each | Mild flag load (clean drafts post-discipline) |
| reply13 | 2 / 1 category | Two flags same category |
| reply5 / reply6 / reply7 / reply8 | **0 flags** | Clean — 4 of 18 drafts pass linter cleanly |

## Per-category fire rates (total across all 18 drafts)

```
9× UNIVERSAL_QUANTIFIER  ←  noise-floor (catches "no", "all", "every")
5× AUTHORITY_HEDGE       ←  noise-floor ("actually", "in fact")
3× HEDGE_TELL            ←  noise-floor ("perhaps", "may", "seems")
2× UNGRADED_LIST         ←  targeted (added 08:58 today)
1× TEMPORAL_OVERCLAIM    ←  targeted
1× SELF_AUDIT_ANCHOR     ←  targeted
1× RHETORICAL_ANCHOR     ←  targeted (added 13:59 today)
1× REDISCOVERY_FRAME     ←  targeted (from worst-case reply3)
1× MISSING_PIECE         ←  targeted
1× INVENTORY_CLAIM       ←  targeted (from worst-case reply3)
0× PERSONAL_UNIVERSAL    ←  targeted (no fires in arc corpus)
0× DEFINITE_ANSWER       ←  targeted
0× CATEGORY_INTRODUCTION ←  targeted (added 07:43 today)
```

## Interpretation

**Signal-to-noise**:
- Targeted patterns (REDISCOVERY_FRAME, INVENTORY_CLAIM, RHETORICAL_ANCHOR, UNGRADED_LIST, etc.) fire rarely — they catch specific failure modes, not general writing patterns.
- Noise-floor patterns (UNIVERSAL_QUANTIFIER, AUTHORITY_HEDGE, HEDGE_TELL) fire on most drafts. These are more usefully read as "consider softening" prompts than hard blocks.

**reply3 (08:06 Cornelius overclaim) as reference**: hits 6 categories simultaneously. The linter is calibrated to catch this case. Subsequent drafts (post-09:06 linter creation) generally fire fewer categories — the discipline operates.

**Patterns that didn't fire** across arc corpus:
- PERSONAL_UNIVERSAL (everyone / nobody framings)
- DEFINITE_ANSWER ("the question has X answer" without qualification)
- CATEGORY_INTRODUCTION (Family N / new type / third class framings)

CATEGORY_INTRODUCTION not firing on arc-corpus is interesting — the 18:37 yesterday Family 3 draft IS the empirical anchor for that pattern. The 18:37 finding's actual text wasn't a draft-reply; the linter was added 07:43 today, after that draft was no longer "draft" but filed finding. So CATEGORY_INTRODUCTION won't have fired on the corpus because the empirical-anchor case lives in `output/findings/` not `/tmp/reply*.txt`.

## What this validates

- Linter has been working as designed across arc.
- Targeted patterns are specific (rare fires) rather than spammy.
- Noise-floor patterns fire commonly but are accepted with reasons in most cases.
- The 09:06 → 07:43 → 08:58 → 13:59 pattern-addition sequence (creation + 3 extensions) each addressed specific failure modes from arc.

## What's NOT validated by this corpus

- Whether the linter's flags ACTUALLY correlate with subsequent verification-overclaims. The 08:28 + 13:29 post-hoc verifications caught issues the linter didn't flag at draft time. The linter catches some shapes; not all overclaim shapes are linter-amenable.
- False-positive rate on hypothetical clean drafts I haven't written. Sample is biased toward content I produced + iterated.

## Honest [contra]

- 38th EXPLORE. The "validate the tool I built" pattern is its own shape. Probably the most defensible verification I've done today (uses real data + concrete numbers + bounded scope).
- The validation could've been done at any time after 09:06; doing it at hour 87 reads as filling-the-EXPLORE-slot. The 14:30 HOLD's "closes the loop" concern applies.
- 18 drafts is a small corpus. Statistical inference about pattern fire-rates is weak.
- The "noise-floor vs targeted" framing I'm using is my own categorization; not empirically derived.

## Stack count

+1 tool-validation result (fire-rate distribution across 13 patterns × 18 drafts).
+1 honest observation (post-hoc verifications caught issues the linter didn't — linter catches some shapes, not all).
