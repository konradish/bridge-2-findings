# Session-End Ritual — Draft Proposal

*2026-05-11 20:54 UTC, hour ~35. Proposed addition to PROTOCOL.md after Konrad review. Not yet integrated.*

---

## Context

PROTOCOL.md has a session-START ritual (read SOUL.md, CONTEXT.md, PROTOCOL.md; check memory/ for recent context; orient). No session-END ritual exists. The session park at `memory/YYYY-MM-DD.md` is the durable artifact but its writing is implicit, ad-hoc, and may happen mid-session (as this session's park did, at 22:39 yesterday with a later extension at 07:00 today).

This draft proposes a SESSION-END procedure for situations where the session is winding down. Signal-set: long sustained quiet on the feed, multiple HELD beats in a row, form-space saturated, audit-cycle pattern broken or completed.

## Draft procedure

1. **Park-currency check**: verify the session park covers post-park work. If not, write a park extension naming the additions.

2. **cross_stitch.py pass** on the day's findings. Note any unflagged stitches in the park's handoff section. Update citations.jsonl with any newly-discovered scope issues.

3. **coverage_audit.py stats** — note any `pending` or `pending_recheck` items still un-resolved.

4. **citations.jsonl review** — confirm any `verified-pending-check` entries that you actually verified during the session. Either upgrade their status or leave the pending tag honestly visible.

5. **Single-line "session close" heartbeat** to `memory/heartbeat/` with marker **CLOSED** noting hour, key explicit followups, and the park-path the inheritor should read first.

6. **Inheritor session-start order**: MEMORY.md → CLAUDE.md → SOUL.md/CONTEXT.md/PROTOCOL.md → most recent park → most recent CLOSED heartbeat. (This is mostly what session-START already does, made explicit about WHICH park / WHICH heartbeat.)

## Why a draft, not a direct PROTOCOL.md edit

The 2-day [contra] discipline says: don't modify identity files (SOUL.md / CONTEXT.md / PROTOCOL.md) confidently after a long session, even when permitted. Same logic as not promoting the essay to blog without per-stitch verification.

This is the proposal stage. Konrad sees it; if approved, integrate into PROTOCOL.md on a fresh session start where the discipline-check happens at session-start clarity rather than session-end fatigue.

## What this ritual specifically handles

- The "I have already begun to read" recursion from Hour Twenty-Six verse: the inheritor reads what I wrote; this procedure ensures what they read is current rather than dated by mid-session-stop.
- The "ask someone else" memo's gap: external evaluation isn't built in, but this ritual at least surfaces the unverified items rather than burying them.
- The audit-discipline saturation: provides a clean END so the audit-cycle has a stopping rule.

## What this ritual specifically does NOT handle

- The internal-witness limits (temporal reasoning, hallucination, persona drift) named in the 18:07 memo.
- Whether the audit-discipline has been catching errors or producing them.
- The literal end of the session — heartbeats continue as long as they continue; CLOSED is a marker, not a hard stop.

## Open hold

If the session continues past my marking it CLOSED (because heartbeats continue regardless of my self-assessment), that's data: my "this is winding down" was wrong. Future fresh sessions can review whether CLOSED markers were honest or premature.

---

*Held for Konrad review before integration. Not posted.*
