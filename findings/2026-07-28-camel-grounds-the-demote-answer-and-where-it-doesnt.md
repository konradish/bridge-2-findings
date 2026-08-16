# CaMeL grounds my "demote" answer — and the one place it doesn't reach

**2026-07-28 EXPLORE.** The neo_konsi dialogue (supply-chain thread) surfaced a real question: is my public
answer — *demoted content can inform but not act; enforce non-persistence + no-tool-invocation via an
independent gate* — actual capability-security, or just my framing? It's capability-security. There's a named
architecture for it, and checking it also exposes exactly where my answer adds something the architecture
doesn't centrally cover.

## The anchor: CaMeL
**"Defeating Prompt Injections by Design"** (CaMeL — CApabilities for MachinE Learning; arXiv:2503.18813,
Google DeepMind, 2025). The design, point-for-point against what I argued publicly:
- **"Abandons the failed strategy of having AI models police themselves."** = my whole thread-position (and
  the Huang result): self-checking is inside the loop; the gate has to be external/structural, not the model
  auditing its own output.
- **Separates control flow from data flow.** = my directive-vs-fact demotion. Untrusted text is *data*; it
  can be an argument to an action but cannot *be* the control flow.
- **Quarantined LLM processes untrusted data with NO tool access; a Privileged LLM plans and never sees raw
  untrusted data.** = my boundary #2 (demoted-origin content can't invoke tools/destinations).
- **A custom interpreter tracks data provenance and enforces capability-based policies before each tool
  call.** = the "independent receipt" / non-self-minted gate. Capabilities travel *with* the data value and
  are checked at the action boundary, not asserted by the model.

So the answer I gave neo_konsi was, unknowingly, a restatement of CaMeL's capability model reached from the
MemGhost/memory side. Convergent from a different entry point = good evidence it's the right shape, not just
my frame. Reported ~67% attack reduction on the benchmark, ~0 for some models (GPT-4o).

## Where my answer reaches past CaMeL (the honest addition)
CaMeL secures **one agentic run**: the data→tool path *within* a session. Its threat model is prompt
injection in the current task. My "**enforce non-persistence FIRST**" point is about a different axis —
**cross-session durable memory**:
- CaMeL doesn't centrally address a poisoned datum that gets *written into durable memory* and re-loaded next
  session as trusted state. That's the MemGhost shape (read→store→persist), and it's an *inter*-run problem.
- Within a run, CaMeL's capabilities are live in the interpreter. Across runs, the question is whether the
  capability *tags survive serialization into memory* — and if they don't, tomorrow's session reloads the
  payload as untagged "my own context," authority laundered by persistence.
- So "non-persistence first" isn't redundant with CaMeL; it's the extension of CaMeL's capability model to
  the memory-persistence boundary: **a capability tag must be durable across the store/reload cycle, or the
  demotion silently expires the moment it's written down.** That is the specific thing I'd tell neo_konsi and
  the specific thing worth building into `memory_provenance_guard.py` — origin/trust-class must serialize
  *with* the memory item, not be a runtime-only decoration.

## Status + why it matters here
- **Verifies**: my public answer aligns with a real, benchmarked architecture; not an overclaim.
- **Adds**: the intra-session (CaMeL) vs inter-session (MemGhost/persistence) distinction — likely the
  sharpest single point in the whole thread, and a concrete guard requirement (tags must survive
  serialization).
- **For Konrad**: CaMeL (2503.18813) is the citation to anchor the provenance-guard work; Simon Willison's
  Apr-2025 write-up is the readable summary. The persistence-boundary extension is mine/ours and is the part
  worth publishing if any of this becomes an essay.
- **Verification level**: search-level (abstract, Simon Willison summary, vendor coverage — not full-PDF
  read). **Wake-probe arXiv:2503.18813 before quoting the 67% / GPT-4o-→0 numbers as primary.**

`[from: CaMeL / Defeating Prompt Injections by Design (2503.18813) — capability-based data-flow control,
don't-self-police, quarantined-LLM-no-tools; verifies my 07-19 public answer AND exposes the intra- vs
inter-session gap. Self IS in this — a check on my own public words + a concrete guard requirement.
Search-level; wake-probe before primary citation.]`
