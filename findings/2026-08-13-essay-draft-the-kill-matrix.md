# The Kill Matrix (draft — companion to "The Kill Count," NOT ship-as-is)

**Status:** DRAFT, written 2026-08-13 CREATE beat. Depends on The Kill Count (drafted 08-03, still carrying 2 flags). Numbers below are abstract-verified only (2604.23887, 2605.17634 — wake-probed same morning, see the two 08-13 findings). Do not ship before: (a) Kill Count's flags resolve, (b) PDFs internals-verified, (c) Konrad's read.

---

A test suite that has never failed tells you almost nothing. That was the argument of The Kill Count: a checker earns trust by the wrongness it demonstrably rejects, not by the silence of its green light. Inject faults; count the kills; the count is the strength.

But a kill count has a blind spot of its own, and I walked into it this week recommending the method to someone building injection defenses for mobile agents.

Layered defenses are the norm now — sanitize the input, wrap it in delimiters, instruct the model to be suspicious, filter the output. Stack seven layers and run your red-team suite, and the stack kills, say, 985 of 1,000 seeded attacks. Strong number. The standard way to learn more is ablation: pull out a layer, rerun, see what leaks. One recent evaluation did exactly this and found the stack leaked 0.5% without its output filter and 0% with it.

Ablation, though, answers the wrong question. It tells you what the stack does without a layer. It does not tell you what each layer *did*. Those differ because kills overlap: an attack stopped by the output filter might also have been stopped by the sanitizer upstream. Suite-level numbers — with and without — conflate a layer that made a thousand redundant kills with a layer that made three unique ones, and the three-unique-kill layer is the one whose removal is quietly catastrophic.

Mutation testing solved this decades ago, and the solution wasn't a better aggregate score. It was a matrix: every mutant crossed with every test, each cell recording a kill or a miss. From the matrix you can read off what no aggregate reveals — tests that kill nothing (dead weight), mutants nothing kills (your blind spots), and tests whose kills are all redundant (safe to lose) versus tests carrying kills nothing else backs up (guard these).

The same object is buildable for a defense stack, and as far as I can find, nobody builds it. Seed your attacks. Let the first layer that stops each one record its kill — but run every downstream layer anyway, in log-only mode, and record whether it *would* have stopped the attack too. Attack by attack, layer by layer: the kill matrix.

What the matrix buys you over the count is one specific number, and it happens to be the number that decides whether your security is real. Some layers are structural: an output filter enforces a property over a space that is finite and enumerable, and its kills are permanent — the attack class dies by construction. Other layers are judgment: a model noticing that text smells like an instruction. Judgment kills are real kills, today. But the same evaluation that ran its attacks past 300 rounds found every judgment-based layer eventually collapsed — not degraded, collapsed — while the structural layer sat at zero across fifteen thousand attacks, because adversaries adapt to judgment and cannot adapt to arithmetic. And there is an argument, informal but hard to dismiss, that this asymmetry is permanent: the space of contexts an attacker can construct is open-ended, and the evidence that would separate a fabricated context from a real one is precisely what the defender doesn't have at decision time. Judgment defends an infinite surface with finite evidence. It loses on schedule.

So partition your kill matrix by layer type and read off: what fraction of my unique kills are judgment kills? That fraction is not part of your security posture. It is a countdown. It is the portion of your 98.5% that round three hundred takes back.

The aggregate number couldn't tell you this. Two stacks can post identical kill counts — one resting on a typed boundary with judgment layers adding redundant depth, the other resting on model vigilance with a filter mopping up the easy cases. Same count. The first is a wall with guards walking on top of it. The second is guards standing where a wall should be, and guards get tired; the whole reason we stack defenses is that we know this. The matrix is how you check which one you built — before the attacker, who is also keeping a matrix, checks it for you.

The general form, one more time, because it keeps generalizing: a green light is not evidence until you know what would have turned it red, *and which part of the system would have done the turning*. Count the kills — then attribute them. Strength that can't be located can't be trusted to hold.

---

*Notes for revision:* the "countdown" paragraph overstates slightly — 2604.23887's collapse result covers their six model-reliant configurations, not all possible judgment layers; soften to "every judgment layer yet measured." Consider whether the guards/wall image earns its place or repeats the point. The mutation-testing paragraph could cite Just FSE'14's converse lesson (17% of faults couple to no mutant) as the matrix's own blind spot: rows you never seeded — links to outside-curator rule (Practice 4); currently omitted for length. ~740 words.
