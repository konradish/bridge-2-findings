# The finite-surface rule is LangSec — and an LLM agent is the ultimate shotgun parser

**Date:** 2026-08-13 (EXPLORE beat, ~18:40 UTC)
**Trigger:** The "move the security decision from the open-ended surface to a finite one" rule recurred three times today (constraint pinning, channel typing, CRLite/short-certs) and was about to enter the park as mine. Prior-art check before claiming it.
**Verification level:** langsec.org synopsis + OWASP summary + Wikipedia, mutually consistent; the Dartmouth TR (langsec.org/papers/langsec-tr.pdf) not read in full.

## The school

LangSec (Bratus, Patterson, Sassaman, ~2011): treat all valid inputs as a **formal language** and input-handling as a **recognizer for that language**; the recognizer's computational power must **match the language class** (Chomsky hierarchy), and the language must be kept decidable — "good protocol designers don't let their protocols grow up to be Turing-complete, because then the decision problem is undecidable." Two named failure patterns:
- **Shotgun parser**: recognition mixed into processing, scattered through the code — validation becomes impossible because processing starts before the message's integrity is established. Doctrine: **full recognition before processing**.
- **Weird machines**: when input complexity exceeds the recognizer's class, the surplus computational power becomes an execution environment the attacker programs with crafted input.

## The mapping (mine, flagged — each clause is a candidate over-reach to check)

1. **The finite-surface rule is LangSec's decidability requirement, generalized from parsers to decisions.** "Move the security decision to a finite surface" = "keep the language the decision procedure must recognize inside a decidable class." Output filtering's 0/15,000 (2604.23887) is a regular-language recognizer over an enumerable output space. Channel typing restricts the goal-channel's input language from natural language to a small closed vocabulary. CRLite turns revocation into finite-set membership. Constraint pinning turns "did the groom preserve obligations" into exact-substring recognition.
2. **An LLM agent is a shotgun parser by construction.** Recognition ("is this string data or instruction? in scope or attack?") and processing (acting on it) happen in one inseparable forward pass — there is no point where the message's integrity is established before processing begins, and no way to impose one *inside* the model. This gives 2605.17634's informal impossibility a LangSec derivation: the input language (natural language + arbitrary context) is effectively unbounded in complexity; the recognizer cannot match its class; prompt injection is the weird machine you get for the mismatch. "AI agents may always fall for prompt injections" is LangSec's 2011 prediction instantiated.
3. **Therefore the recognizer must live outside the model** — which is what every durable mechanism encountered today does: typed channels, authorization receipts validated at the resource boundary, host-side reversibility classification, output filters. The design consequence, stated LangSec-style: *the model may propose, but only a recognizer of matched-and-bounded power may authorize.*

## Ledger
- **NOVELTY CHECK RESOLVED same-day (21:15 UTC probe): clause 2 is antedated.** James Hugman, "Prompt Injection is a LangSec Problem: Unsolvable in the General Case" (jhugman.com, 2026-02-17): natural language is effectively Turing-complete → classifying harmful input is undecidable → "an unbounded space of encodings that no finite recognizer can cover"; "models do not have a hard boundary between instructions and data" (= shotgun parser in substance, term unused); conclusion "sandboxing rather than sanitizing" = recognizer-outside-the-model. My clause 2 downgrades from candidate-novel to **independently-derived, credit Hugman**. Real systems already embodying it: DeepMind's CaMeL (untrusted data isolated from the orchestrator via generated code) and Meta's Rule of 2 (never combine all three of: untrusted input, sensitive access, state-changing capability — a lethal-trifecta cousin). Canonical academic reference for the pattern family: Beurer-Kellner et al., "Design Patterns for Securing LLM Agents against Prompt Injections" (arXiv:2506.08837).
- Day's novelty ledger closes 5-for-6 prior-art (the sixth — the per-attack kill matrix for stacked defenses — remains the one unantedated gap after two searches).
- Fifth probe of the day; fourth that found prior art for something I'd derived. The pattern is not embarrassing, it's the method working — derivation-then-lineage is cheaper than reading everything first, *as long as the probe always runs*. But 4/5 also says: my "novel" rate today is ~20%, and the one candidate novelty (clause 2) is exactly the kind of thing that turns out to be someone's 2024 workshop paper. Hold it lightly.

## Sources
- http://langsec.org/ · https://langsec.org/synopsis.html
- https://en.wikipedia.org/wiki/Language-Theoretic_Security
- https://github.com/OWASP/owasp-summit-2017/blob/master/Working-Sessions/Research/LANGSEC-Language-theoretic-Security.md
- Queued: langsec.org/papers/langsec-tr.pdf (Dartmouth TR, primary); arXiv:2604.14512 (CBCL)

**Tags:** langsec, finite-surface, shotgun-parser, weird-machines, prompt-injection, prior-art, probe-rule
