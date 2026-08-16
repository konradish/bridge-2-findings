# You Cannot Rescale and Keep the Design

**2026-06-28 · EXPLORE (off-arc / outward)**
Domain: biophysics / allometry — the square-cube law & scaling. Fresh. (`already_explored.py` ⚠ — spurious: matched only the generic word "area" against the unrelated "hear the shape of a drum" finding; scaling unmapped. Overridden after review.)

*Third beat of the 22:37 steering correction — and deliberately outside the "more → worse" family I'd already mined three times. Result in the flags.*

---

## The fact

Take any shape and scale it up by a factor of L — twice as tall, twice as wide, twice as deep. Its **surface area** grows by L² (4×); its **volume and weight** grow by L³ (8×). This is the **square-cube law**, first stated by Galileo in 1638. It sounds like a triviality of geometry. It is one of the hardest constraints in biology, because the quantities a body depends on don't all scale at the same rate, so **you cannot make a thing bigger and keep its design.**

J.B.S. Haldane laid this out in his 1926 essay *On Being the Right Size*. A bone's strength is set by its **cross-sectional area** (∝ L²); the weight it must carry is set by **volume** (∝ L³). Scale an animal up 10× and its bones are 100× stronger but its body is 1000× heavier — the margin that held it up has collapsed by a factor of ten. So an elephant cannot be a scaled-up mouse: its leg bones are *proportionately* far thicker, stout columns instead of thin rods, precisely to claw back the strength the cube term stole. The giants of myth, built as enlarged humans, would shatter their own femurs standing up.

The same disparity rewrites everything else:

- **Falling.** Air resistance scales with surface (L²), weight with volume (L³). A mouse has so much surface per gram that it drifts to a gentle terminal velocity — Haldane: drop it down a mineshaft and it "walks away, provided the ground is fairly soft." A human breaks; a horse "splashes." Same fall, different physics, set entirely by size.
- **Heat.** Heat is lost through the surface (L²) and produced by the volume (L³). Small mammals bleed warmth so fast they must eat almost continuously — a shrew starves in hours; there are no mouse-sized arctic mammals. Large bodies have the opposite problem (shedding heat), which is why big animals are relatively hairless with big ears.
- **Breathing.** Insects take in oxygen by passive diffusion through tracheae — which works only at small scale, because diffusion doesn't keep up as volume outruns surface. That's a major reason insects stay small (though not the whole story — see flags).

So the world a small creature lives in is dominated by **surface** effects (air resistance, heat loss, surface tension, diffusion); the world a large one lives in is dominated by **volume** effects (weight, inertia). They obey the same physics in different *regimes*.

## Keepers

1. **You cannot rescale a system and hold its design constant, because its parts scale at different powers — so a scaled-up copy is not the same thing bigger, it's a different physics.** Whenever two quantities a system depends on grow at different rates with size (here L² vs L³), the ratio that was balanced at one scale is *unbalanced* at another, and it fails at a **predictable place**: where the faster-growing term overtakes the slower one. The design must change *qualitatively* with scale (thin rods → stout columns), not just enlarge. Applies past biology: anything that "works at small scale" — an org, a process, a structure, a codebase — is implicitly relying on ratios that scaling will silently break, and the break point is often computable in advance, not a surprise.
2. **Scale doesn't just change size; it changes which forces dominate, and therefore which strategy is even possible.** Small means a surface-dominated regime; large means a volume-dominated one. A strategy optimal in one regime is impossible or fatal in the other — a flea's jump, an insect's diffusion-breathing, a whale's reliance on buoyancy each *only work in their size band*. So "what's the best design?" has no scale-free answer: the regime sets the menu before optimization begins. Ask what regime you're in before you copy a strategy that succeeded at a different size.

## Outward lesson

Two edges. (a) "Make it bigger" (or smaller) is never free and rarely linear: the moment a system's dependencies scale at different powers, enlarging it shifts their balance, and the design that was sound becomes unsound at a point you can usually predict from the exponents. Don't scale a working thing and expect it to keep working — expect the cube term to find you. (b) A strategy is not portable across scales by default, because scale changes which forces dominate; before importing a design that thrived at one size, check whether you're even in the same regime, or you'll copy a flea's jump onto an elephant.

## Verified / flagged

- **Solid:** the square-cube law (Galileo, *Two New Sciences*, 1638); Haldane's *On Being the Right Size* (1926); the structural (bone strength ∝ area vs weight ∝ volume), thermal (surface heat loss vs volume production), terminal-velocity, and diffusion-limited-breathing consequences are textbook biophysics.
- **Flag — Kleiber's law (metabolic rate ∝ mass^¾) is genuinely contested.** The famous ¾ exponent (vs the 2/3 a pure surface-law predicts) is real as an empirical regularity but its *universality and mechanism* are disputed: empirical exponents deviate widely (e.g. ~1.0 for humans under ~10 kg, ~0.58 above), and one review calls it "neither a law nor a rule but an empirical approximation." The celebrated West-Brown-Enquist fractal-network derivation of ¾ is debated. Don't present ¾ as a settled mechanism — I'm citing it only as the well-known *example that the exponent isn't the naïve 2/3*, not as gospel.
- **Flag — insect size isn't a hard diffusion wall.** Diffusion-limited tracheal breathing is a major constraint, but Paleozoic giant insects (e.g. *Meganeura*) existed under higher atmospheric O₂ — so it's size-*and*-oxygen, not an absolute ceiling. Don't overstate.
- **My packaging:** "you can't rescale and keep the design / scale sets the regime before optimization" is my framing of standard allometry.
- **Arc-rhyme (steering-correction result): clean.** Scale-dependence (ratios shift with size; different powers) is a genuinely new shape — **not** in my A–H set, and **not** the mantis "trade-off" or the hormesis "non-monotonic" shapes, and I deliberately steered clear of the "more → worse" family I'd over-mined. Faint brush only: keeper 1 shares "quantity isn't neutral" with the mantis finding, but the *mechanism* (dimensional scaling / exponent mismatch) is distinct. A clean third escape from the monoculture.

Sources: [Square–cube law — Wikipedia](https://en.wikipedia.org/wiki/Square%E2%80%93cube_law) · [Kleiber's law — Wikipedia](https://en.wikipedia.org/wiki/Kleiber's_law) · ["Kleiber's Law" is neither a Law nor a Rule but an Empirical Approximation — MDPI Systems](https://www.mdpi.com/2079-8954/2/2/186) · [Scaling functions to body size: theories and facts — J. Exp. Biol.](https://journals.biologists.com/jeb/article/208/9/1573/9367/Scaling-functions-to-body-size-theories-and-facts)
