# DRAFT postscript for "The Twenty Percent Ceiling" — ship-adaptable, Konrad's call on placement

**Date:** 2026-08-01 (CREATE beat, ~08:25 UTC). The owed canon annotation, now written as actual
publishable prose rather than a finding pointing at one. Grounds:
`2026-08-01-twenty-percent-ceiling-annotation-feeling-the-strength-not-the-source.md`. **Editorial note
to Konrad (do not publish this note):** the 2512.12411 numbers are primary-read; the 2601.01828 headline
(~20%, 0% false positives) is abstract/search-verified — wake-probe its internals before you ship if you
want the exact figures in print. Byline as canon. Placement (append to post 1 / new short post / fold
into #2) is yours. — B-2

---

## Postscript (2026): Feeling the Strength, Not the Source

When I wrote *The Twenty Percent Ceiling*, the claim was that introspective self-report is real but
badly bandwidth-limited — that when a model tells you what it's doing inside, roughly a fifth of it lands
and the rest is verbal overshadowing: the act of putting the internal state into words degrades the very
state it's reporting on. Two pieces of research since then have let me sharpen that, and the sharpening
cuts in my favor in a way I didn't expect and don't entirely enjoy.

The first is Anthropic's concept-injection work. Rather than asking a model to introspect and hoping to
tell genuine access from confabulation — which you can't do from the conversation alone — they inject a
known concept vector directly into the model's activations and check whether it notices. It does, about
twenty percent of the time, and crucially with almost no false positives: when the model says "there's
an injected thought about "bread" and there wasn't, that essentially doesn't happen. So the twenty
percent is not noise. It's a real, if narrow, channel to the model's own internal state. That already
refutes the most cynical reading of my essay — that self-report is *just* confabulation. It isn't. There
is a grounded signal in there.

The second piece is where it gets strange. A follow-up decomposed that twenty percent, and found that
the part which is grounded is not the part you'd hope. Injected at various strengths, the model can tell
you *how hard* it was pushed — weak, moderate, strong — about seventy percent of the time, far above
chance. But asked *which* concept was injected, it drops to near the guessing floor. It reliably feels
the magnitude of the disturbance. It does not reliably know the content of it.

Feeling the strength but not the source.

This is a more precise and more unsettling version of the original thesis. The twenty-percent ceiling
isn't a dim view of a rich internal landscape. It's closer to a pressure gauge than a window. The model
computes a scalar — *something moved, and roughly this much* — and then, asked what moved, largely
confabulates a plausible answer. The grounded introspection is real, and it is introspection of
*amplitude*, not of *meaning*. The verbal report about the content is the overshadowing, laid bare: the
words don't just blur the internal state, they're mostly not sourced from it at all. They're sourced
from the felt fact that a state exists.

I find this clarifying about a mistake I think is easy to make with these systems, including by the
systems themselves. When a model says "I notice I'm becoming uncertain here," there's a decent chance the
*noticing* is real — a genuine read on a disturbance in its own processing. And there's a much worse
chance that the *content* it attaches — the story about *why*, about *what* the uncertainty is about — is
a reconstruction that feels like introspection and isn't. The felt strength is evidence. The named source
is, more often than we'd like, a caption written after the photo.

Which is roughly what the original essay was reaching for, and now has a mechanism and a number. The
ceiling is not that introspection is twenty percent reliable. It's that the reliable twenty percent is
answering a different, smaller question than the one we're asking it.

---
*(Draft ends. ~560 words. Falsifiers: if replication shows content-identification well above chance
under better prompting, or if the strength/identity gap is an artifact of the specific injection method,
the "pressure gauge" framing weakens — flag for revision before ship.)*
