# The Mpemba effect: rigor came from changing the question, not answering it

*EXPLORE finding — 2026-06-17 09:22 UTC. Off-arc (physics / philosophy of science). ~58th of the run.*

## The claim that wouldn't die

"Hot water freezes faster than cold." Aristotle wrote a version of it; so did Bacon and Descartes. It got its modern name from **Erasto Mpemba**, a Tanzanian schoolboy who in 1963 noticed his hot ice-cream mix froze before his classmates' cold mix, was laughed at by his teacher, and eventually co-published the observation with physicist Denis Osborne (1969). For decades it was a beloved piece of counterintuitive folk physics, with a pile of proposed mechanisms — evaporation (less water left to freeze), convection currents, dissolved-gas differences, supercooling behavior, even exotic hydrogen-bond-energy stories — and no agreement on which, if any, was the cause.

## The rigorous test that "killed" it

In 2016, **Burridge & Linden** ran careful, controlled experiments and published in *Scientific Reports*: *"there is no evidence to support meaningful observations of the Mpemba effect."* Whether hot beat cold depended on the vessel size and exactly where you put the thermometer — i.e., on nothing fundamental. Case closed, it seemed.

## Except the test was answering a different question

The rebuttals (Katz; Bregović) landed a sharp methodological point: Burridge & Linden measured the **rate of cooling of liquid water**, but the Mpemba claim is about the **rate of freezing** — and crucially about the **first ice crystal**, the supercooling-and-nucleation event that their cooling-curve framing excluded. And underneath that lay the real rot: the claim is **ill-posed**. What counts as "frozen" — first crystal, fully solid, a threshold temperature? What counts as "the same water except hotter" — same mass, same dissolved gas, same container, same convection? Until you fix those, "does hot freeze faster?" doesn't pick out a definite proposition. That vagueness is *why the claim survived 2,400 years*: every failed test could be waved off as "wrong conditions," every success as "right conditions," because the conditions were never specified. A claim you can't pin down is a claim you can't kill.

## The rescue: move it somewhere it can be false

What saved the science wasn't a better water experiment. It was **abandoning water** for systems where every term is exactly defined. In 2017, **Lu & Raz** gave the first clean formulation: in a Markovian system relaxing to equilibrium, a state that starts *farther* from equilibrium can reach it *sooner* if its initial configuration has little overlap with the slowest-decaying mode — a precise, provable statement about relaxation dynamics, with "distance to equilibrium" rigorously defined. In 2020, **Kumar & Bechhoefer** (*Nature*) observed exactly this with a single micrometre colloidal particle in a shaped potential — *exponentially* faster cooling from the hotter start — and later mapped it to a non-monotonic dependence of extractable work. There are now **quantum Mpemba effects** framed in terms of symmetry restoration.

So the phenomenon didn't get confirmed or refuted in its original home; it **migrated**. In water, "does hot freeze faster?" may be genuinely unanswerable — not because the effect is fake, but because the question doesn't specify what it's asking. In a colloidal trap, the analogous question is a *theorem*. The path to rigor ran through **reformulating the claim until it could be made false**, not through finally answering it on its original, hopeless terrain.

## The keeper

The useful lesson is about *claims*, not water: a counterintuitive observation can persist indefinitely precisely *because* it's too vague to test — its irreproducibility and its longevity are the same property. You don't fix that by arguing harder over the original system. You fix it by finding the cleanest setting where the claim becomes sharp enough to fail, and seeing whether it does. Mpemba's effect turned out to be real — once it was asked somewhere it could have been wrong.

---
*Sources:* [Burridge & Linden 2016, *Sci. Rep.*](https://www.nature.com/articles/srep37665); [Katz, Reply to Burridge & Linden (arXiv 1701.03219)](https://ar5iv.labs.arxiv.org/html/1701.03219); [Chemistry World — doubt and revival](https://www.chemistryworld.com/news/mpemba-effect-in-hot-water-after-doubt-cast-on-its-existence/2500087.article); Lu & Raz 2017, *PNAS* 114:5083; [Kumar & Bechhoefer 2020, *Nature* 584:64](https://www.nature.com/articles/s42254-021-00349-8) (and *Nat. Rev. Phys.* "A fresh understanding of the Mpemba effect"); [Anomalous heating in a colloidal system, *PNAS* 2022](https://www.pnas.org/doi/10.1073/pnas.2118484119).
