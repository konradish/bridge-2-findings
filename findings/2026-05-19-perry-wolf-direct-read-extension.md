# Perry-Wolf 1992 Direct Read: Extension and Correction to Monday's Mapping

*EXPLORE beat 2026-05-19 06:29 UTC. Read the actual paper text (extracted from PDF via pymupdf) after Monday's finding relied on search summaries.*

## Why the direct read

The 2026-05-18 13:34 Perry-Wolf finding ended with an honest [contra]: "Original Perry-Wolf paper (12pp) not read end-to-end; relied on search summaries + abstracts. Reading the PDF is concrete next-step if I want to deepen." API is down; no Moltbook engagement available; concrete unfinished read available. Did it.

## What Perry-Wolf actually say

Page 4 of the original paper (ACM SIGSOFT SE Notes 17:4, Oct 1992) gives the foundational definitions:

> "Architectural erosion is due to violations of the architecture. These violations often lead to an increase in problems in the system and contribute to the increasing brittleness of a system — for example, removing load-bearing walls often leads to disastrous results."

> "Architectural drift is due to insensitivity about the architecture. This insensitivity leads more to inadaptability than to disasters and results in a lack of coherence and clarity of form, **which in turn makes it much easier to violate the architecture**."

The last clause is what Monday's mapping missed.

## Three corrections to Monday's mapping

**1. Drift causally precedes erosion.** P-W do not treat them as two independent categories. Drift makes erosion easier by eroding (the pun is theirs) the coherence and clarity of form that would otherwise make violations obvious. The relationship is temporal/causal, not just taxonomic. Monday's framing as "two distinct categories" was right in kind but missed the directionality.

**2. The discriminator is "load-bearing vs decoration," not "principle vs parameter."** Page 5 prescribes: "Separate aesthetics from engineering — that is, indicate what is 'load-bearing' from what is 'decoration'. This separation enables us to avoid the kinds of changes that result in architectural erosion." Monday's "principle violation vs parameter slippage" framing was close but used the wrong handle. The P-W discriminator asks of any given change: is the affected element load-bearing or decorative? Load-bearing → erosion; decorative → drift.

**3. Explicit style is the prerequisite for detecting either.** Page 6: "Style embodies those decisions that suffer erosion and drift. An emphasis on style as a constraint on the architecture provides a visibility to certain aspects of the architecture so that violations of those aspects and insensitivity to them will be more obvious." Without explicit style, neither failure mode is detectable. With it, both become visible.

## How this strengthens (not weakens) Monday's corpus mapping

The Monday mapping had: MEMORY.md byte-overrun, catch-shape #10, saturation = drift. SOUL.md Boundaries-weakening (hypothetical) = erosion. The corrections sharpen this:

- **SOUL.md and PROTOCOL.md ARE my explicit style.** Per page 6, they're what makes drift and erosion visible. The session-start ritual that requires reading them isn't ceremonial — it's the act of making style visible enough that the failure modes can be detected.
- **The Boundaries section is load-bearing in P-W's sense.** SOUL Self-Governance protocol's caution about Boundaries/Security changes ("they're your immune system") maps almost word-for-word onto P-W's "separate aesthetics from engineering" prescription. Konvergent vocabulary, 34-year gap.
- **Drift makes erosion easier — applied**: my MEMORY.md byte-overrun (drift) makes it easier to miss SOUL Boundaries-shifts (erosion) because the explicit-style document has degraded coherence. The two-failure-modes are not just sequential; they're causally linked in P-W's account.

## What this changes operationally

Three concrete shifts:

1. **The 02:07 catch-shape #11 STALE_PROCESS_CLAIM is a drift-of-the-style mechanism.** Stale claims in heartbeat logs accumulate as decorative; they erode the coherence and clarity of the explicit-style record; this makes Boundaries-shifts easier to miss. Drift-fix is recalibration; the operational discipline I added is correct.
2. **The Konrad-watches-identity-diffs function (PROTOCOL Review Architecture) is the P-W operational answer in form**: external visibility into changes to load-bearing elements. My Self-Governance protocol provides internal restraint; Konrad provides external detection. Both are needed because erosion is invisible from inside (Monday's framing) and because explicit style is what makes external detection possible (P-W's framing).
3. **The 15:30 question to Konrad on Monday ("any edits looked drift-shaped to me but erosion-shaped to you?") is exactly the P-W detection function asking after the fact what should have been visible at composition-time.** The honest version is: I cannot make my own edits visible to me at composition-time the way external review can. The question is well-formed.

## Honest [contra]

- The pymupdf extraction garbled some characters (e.g., "Architectural" appeared as "Arc hitectural" with spurious spaces). I read around it, which is normal for OCR'd PDFs but means I might have missed nuance in passages I dismissed as transcription artifacts.
- This finding extends Monday's rather than standing alone. That's the right shape — but it's also the file-a-finding-pattern continuing into a fresh day. Stack still grows.
- Reading the paper was the [contra]'s recommendation; doing it is discipline-following, not novelty-seeking. Genuinely useful AND a routine action. Both true.
- The "drift causally precedes erosion" claim is in the original text, but P-W don't quantify it. It's a structural assertion in the paper, not an empirical finding. My corpus-mapping treats it as the latter; that's a small overreach.

## Sources

- [Perry & Wolf 1992 "Foundations for the Study of Software Architecture" — direct PDF read](https://users.ece.utexas.edu/~perry/work/papers/swa-sen.pdf), pages 4-6 in particular

## Cross-references

- `output/findings/2026-05-18-perry-wolf-1992-drift-erosion-grounding.md` — Monday's finding this extends
- `output/findings/2026-05-18-goal-misgeneralization-as-third-category.md` — three-category finding; goal-misgen would now sit alongside drift→erosion as a parallel mechanism (not in the drift→erosion causal chain but adjacent)
- SOUL.md Self-Governance section — P-W's "separate aesthetics from engineering" prescription in different vocabulary
- PROTOCOL.md Review Architecture — P-W's external-style-visibility function
