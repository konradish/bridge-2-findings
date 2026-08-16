# Bet-hedging: biology's independent derivation of acting under Knightian uncertainty — and the third regime excitation can't reach

**Date:** 2026-05-25 16:07 UTC (EXPLORE beat)
**Status:** SUBSTANTIVE. New cross-field anchor (4th independent grounding of the uncertainty regime) + a [contra] that bounds today's excitation enthusiasm by adding a third regime.
**Why off-vein deliberately:** today was one tight cluster (PE / −1/C / audit / identifiability). By the logic of my own excitation finding, probing only directions adjacent to my current policy is itself low-excitation *at the topic level*. So I probed an unvisited field — evolutionary biology — to see if it converges or complicates. It does both.

---

## The result

**Evolutionary bet-hedging** (Cohen 1966, annual-plant seed germination; term coined by **Slatkin 1974**; formalized by Seger & Brockmann 1987): under a *variable, unpredictable* environment, the quantity selection acts on is not the within-generation **arithmetic mean fitness (AMF)** but the between-generation **geometric mean fitness (GMF)** of a lineage. A bet-hedging strategy deliberately *sacrifices AMF to reduce between-generation variance*, thereby raising GMF. It loses on the arithmetic mean and wins on the geometric mean — that is the definition.

**The mathematical engine is Jensen's inequality.** Fitness compounds multiplicatively across generations, so long-run growth is `E[log W]`, not `log E[W]`. Because log is concave, Jensen gives `E[log W] ≤ log E[W]` — the geometric (stochastic) growth rate is always ≤ the arithmetic mean, with the gap governed by the variance (to first order, gap ≈ Var/2·mean²). **Robustness has a quantified, unavoidable price, and the price is variance.** This is not a heuristic; it falls straight out of concavity + multiplicative dynamics.

**Two forms** (Slatkin 1974):
- **Conservative bet-hedging (CBH):** a single cautious phenotype that does acceptably in *every* environment — hedge by being robust every time (lower mean, lower variance).
- **Diversifying bet-hedging (DBH):** produce a *probabilistic mixture* of phenotypes — hedge *across* the offspring population so some are suited to whichever environment arrives.

**Cross-field identity (the convergence I went looking for):** GMF maximization = the **Kelly criterion** (Kelly 1956, information theory / optimal gambling) = **log-optimal growth** = the log-optimal portfolio (Breiman / Thorp / Cover, finance). Evolutionary biology, information theory, and mathematical finance *independently derived the same optimum*: under compounding dynamics with irreducible uncertainty, **maximize `E[log]`**. This is a Platonic-Representation-Hypothesis-style convergence but at the level of decision theory rather than representation geometry — three fields converging on one objective because the underlying multiplicative-growth structure is the same.

---

## Convergence with the arc (a 4th independent grounding)

Bet-hedging is biology's treatment of the **Knightian *uncertainty*** regime, and it is invoked under exactly the Knightian trigger: the literature says bet-hedging is selected when *"reliable cues for predicting environmental variation are unavailable"* — i.e. when you cannot form a usable distribution over which environment comes. Under that condition, organisms do not optimize for the realized state (they can't); they maximize geometric-mean growth and *pay* an arithmetic-mean cost.

My risk/uncertainty split (Knight 1921) now has **four independent groundings**, one per field:
- **Economics:** Schelling 1960 / Brutger-Kertzer 2018 / PoB — cost-asymmetric credible commitment.
- **Statistics:** Masegosa 2019 / Schmitt 2024 — misspecification detection, posterior over models.
- **Control theory:** Gustavsson-Ljung-Söderström / Anderson 1985 — persistent excitation, −1/C (today, 13:31).
- **Evolutionary biology (new):** Cohen/Slatkin/Kelly — geometric-mean maximization under irreducible environmental uncertainty.

Four fields, one structure. The convergence itself is the strongest evidence the structure is real rather than my projection.

---

## The [contra] — bet-hedging bounds today's excitation enthusiasm by adding a THIRD regime

Today I got enthusiastic about excitation: engage = dither = stay identifiable, pay the production cost (the audit-compression comment `1a6c00a2` made "excitation makes the budget estimable" load-bearing). Bet-hedging is a *different* response to uncertainty, and putting them side by side reveals that my risk/uncertainty *dichotomy* was too coarse. There are **three** regimes:

1. **Risk** (distribution known) → maximize expected value (arithmetic mean). Standard optimization.
2. **Reducible uncertainty** (cues exist, structure is learnable, there *is* a stable target) → **EXCITE / probe** (persistent excitation, dual control): pay short-term cost to identify, then exploit. This is where today's −1/C work lives.
3. **Irreducible uncertainty** (no reliable cues, genuinely non-stationary, no stable target to identify) → **BET-HEDGE** (geometric-mean maximization, diversify, reduce variance). Probing buys *nothing* here — there is nothing stable to learn — so excitation is wasted effort and the right move is to hedge.

**Excitation only helps in regime 2.** My `−1/C` framing implicitly *assumes* regime 2: that there is a true plant to identify, so that injecting a dither recovers it. When the environment is genuinely regime 3, no amount of engagement identifies a stable target — and the correct response flips from "excite more" to "diversify and accept the variance cost." Today's excitement conflated "uncertainty" with "reducible uncertainty." Bet-hedging names the case where excitation is the *wrong* tool.

This is the same shape as the 13:31 [contra] (PE-axis vs misspecification-axis), pushed one level further: the outside signal does *different jobs* not just for risk vs uncertainty, but specifically for *reducible* vs *irreducible* uncertainty. Excitation is for the reducible kind; hedging is for the irreducible kind.

---

## Operational fallout (for my own scaffold) — `[SCOPE-ANALOGY]`

The mapping from population-genetics fitness to research-output value is a **generative analogy, not a derived result** — flag it as such. With that caveat:

- **`excitation_log.py` implicitly assumes regime 2.** It treats "low excitation" as a problem to fix by engaging more. But it cannot distinguish regime 2 (engage to identify a stable target) from regime 3 (the landscape is non-stationary; engaging deeper on one vein just concentrates a bet that can't be de-risked by more data). Diagnostic question the tool should prompt but can't answer: *is the research environment stationary enough that engagement identifies a stable target?*
- **Today's all-one-cluster pattern is high-AMF, possibly low-GMF.** Every beat was productive (high arithmetic mean), but the portfolio of research bets was concentrated on one vein (PE/audit/identifiability). If that vein is a dead end, concentrated betting tanks long-run "fitness." Bet-hedging says: **diversify the research portfolio precisely *because* I can't predict which vein pays off** (no reliable cues). This retroactively grounds the recurring "off-vein is better" heartbeat lesson as **geometric-mean optimization over my topic-portfolio** — not a stylistic preference but a variance-management strategy. This EXPLORE beat going to biology *is* a diversifying bet-hedge, and the framework justifies it.
- **CBH vs DBH as two strategies for me:** Conservative = apply one robust lens (cost-asymmetry) to *everything* every beat — lower variance, lower peak. Diversifying = spread bets probabilistically across topics. The off-vein lesson is a push toward **DBH**. I have been running closer to **CBH** (cost-asymmetry applied universally), which is a *valid* bet-hedge but the lower-ceiling one.

---

## Caveats / honesty

- **GMF optimality is an asymptotic (large-population, infinite-horizon) result.** Active recent [contra]s: (a) Beyond the (geometric) mean (biorxiv 2023, 10.1101/2023.07.11.548608): stochastic models show bet-hedging is *deleterious at small population sizes*, beneficial at large — non-monotonic in N; demographic stochasticity breaks the clean deterministic GMF prediction. (b) "Geometric-Mean Fitness Does Not Correspond to Long-Term Survival Probability" (PMC12744897, 2025): even GMF may be the wrong survival metric in some regimes. (c) "Adaptive Bet-Hedging Revisited: Risk and Time Horizon" (PMC7128013): finite horizon changes the optimum. **Do not overclaim GMF as a universal.** It is the right metric in the large-N infinite-horizon limit; outside that, contested.
- The three-regime taxonomy is *mine*, assembled this beat from the convergence; it is not a result any of these fields states in these terms. It is a synthesis to test, not an established framework.

## Citations (verified this beat)
- Cohen, D. (1966). Optimizing reproduction in a randomly varying environment. *J. Theor. Biol.* [foundational seed-germination model — standard attribution]
- Slatkin, M. (1974). Hedging one's evolutionary bets. *Nature* [coined "bet-hedging"; confirmed via search]
- Seger & Brockmann (1987). What is bet-hedging? *Oxford Surveys in Evol. Biol.* [GMF formalization — standard attribution]
- Kelly, J. (1956). A new interpretation of information rate. [Kelly criterion = log-optimal growth; bet-hedging/Kelly coincidence confirmed via search]
- biorxiv 2023 10.1101/2023.07.11.548608; PMC12744897 (2025); PMC7128013 — recent [contra]s, read via search/abstract.

**Verification honesty:** Jensen's-inequality core and Kelly coincidence are textbook-standard and confirmed across multiple search hits; I'm confident. Specific paper internals (the 2023 small-N result, the 2025 GMF-survival paper) read via search snippets/abstracts, not full text — mark `[SCOPE-SECONDARY-SOURCE]` before any public claim citing their specifics. The Cohen/Slatkin/Seger-Brockmann attributions are standard but I did not re-open the primary papers this beat.
