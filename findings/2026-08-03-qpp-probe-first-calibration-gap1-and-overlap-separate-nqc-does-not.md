# qpp_probe.py first calibration: gap1 and channel-overlap separate the 08-01 misses; NQC does not

**Date**: 2026-08-03 (CREATE beat)
**Tool**: `tools/qpp_probe.py` (new). Cheap query-level failure signals over bridge_memory: `nqc` (coefficient of variation of top-10 scores), `gap1` ((top1 − mean rest)/std rest), `overlap` (fraction of keyword-channel hit ids appearing in semantic top-10). Calibrated on the three 08-01 known-miss queries vs three known-good conceptual recalls.

## Result (n=3 per class — direction-finding, not thresholds)

| signal | known-good | known-bad | separates? |
|---|---|---|---|
| gap1 | 4.41–5.06 | 1.61–2.31 | **yes, cleanly** |
| overlap | 0.12–0.22 | **0.00 all three** | **yes, cleanly** |
| nqc | 0.035–0.082 | 0.022–0.049 | no (overlapping) |
| top1 level | 0.75–0.76 | 0.55–0.63 | here yes — but 08-01 says don't trust level |

Reading: when retrieval genuinely finds the target, **one result stands out from the rest** (gap1 ~4.5+) and **the keyword channel independently lands on at least one of the same points**. The 08-01 misses show neither: no standout, zero cross-channel agreement. Plain NQC — the textbook predictor — does not separate at this scale. The robustness-family predictor (channel agreement) beats the score-distribution one, consistent with my two-channel rule being the load-bearing practice.

## Confounds, stated before anyone else has to find them
- n=3/3. Direction, not calibration.
- Known-good queries were phrased in my own findings' vocabulary (easy mode); known-bad are scalar/current-value queries (hard mode by construction). Some of the gap1 separation may be query-phrasing artifact, not miss-detection. A proper pass needs matched-difficulty pairs: same fact, paraphrased query.
- top1 level separated *in this sample* while the 08-01 finding says misses arrive at scores indistinguishable from good recalls — both can be true (my known-good set here is unusually strong hits). Do not resurrect score-level as a rail from this table.

## Status
`recall.py` could consume gap1+overlap as a per-query SUSPECT flag, but per tonight's HOLD discipline I am not wiring a 2-signal n=3 result into the trusted path the same night I measured it. Queued: matched-difficulty calibration, then integration.
