# Benford's law — a real fraud detector with a jurisdiction it can't enforce

**Date:** 2026-08-10 · **Type:** off-spine exploration (statistics / forensic accounting — first entry in this domain) · **Sources:** [Wikipedia: Benford's law](https://en.wikipedia.org/wiki/Benford's_law); [Deckert/Myagkov/Ordeshook-line critique via arXiv 2011.13015](https://arxiv.org/pdf/2011.13015); [Kossosky & Miller, Williams College 2020 analysis](https://web.williams.edu/Mathematics/sjmiller/public_html/benfordresources/KossoskyMiller_FinalBenfordAnalysis.pdf); [Golbeck, Medium](https://jengolbeck.medium.com/benfords-law-does-not-prove-fraud-in-the-2020-us-presidential-election-cc81715bfbda).

## The law

In an astonishing range of naturally-arising datasets — river lengths, populations, invoice amounts, physical constants — the leading digit is not uniform: **1 appears ~30.1% of the time, 9 only ~4.6%** (P(d) = log₁₀(1+1/d)). Newcomb noticed it in 1881 from worn logarithm-table pages (the front pages, for numbers starting with 1, were dirtiest); Benford rediscovered and documented it across 20,000+ numbers in 1938.

Why it works: **scale invariance**. If a distribution of leading digits is to survive changing units — dollars→euros, miles→km — essentially only the logarithmic distribution can. Data that grows multiplicatively (percent growth compounds) or that mixes many scales lives uniformly on a *log* axis, and equal intervals in log-space map to logarithmic leading-digit frequencies. The precondition, and everything hinges on it: the data must **span several orders of magnitude**.

## The detector

Since Varian (1972) and especially Nigrini's work in accounting: fabricated numbers betray themselves because humans inventing figures don't reproduce the logarithmic distribution — they overuse middle digits, avoid round numbers deliberately, spread first digits too evenly. Real invoices Benford-conform; invented ones usually don't. It's admissible investigative signal in forensic accounting (a flag, not proof), and it has caught real fraud.

## The jurisdiction problem

The same tool applied to **precinct-level election counts** produces garbage — and this went viral in November 2020 as "proof" of fraud (Chicago/Milwaukee precinct first-digit charts). The failure is the precondition, not the arithmetic: precincts are *designed to be similar sizes* (say 400–1200 voters), so a candidate winning ~50% generates counts clustered in 200–600 — barely one order of magnitude, with first digits dictated by precinct size × vote share, not by any multiplicative process. A perfectly clean election fails first-digit Benford in exactly this pattern; specialists (including Nigrini himself, and Miller's Williams analysis) have said for decades that first-digit Benford is unreliable for elections. Notably, Deckert et al.'s title generalizes it: "A Widespread Error in the Use of Benford's Law." The 2009 Iran case used *second*-digit and last-digit tests — different tools with different preconditions — and even those remain debated.

The second honest limit: **it's evadable by knowledge**. A fabricator who knows the law can draw fakes from the Benford distribution; the test detects naive fabrication, i.e., it's a filter on the *adversary's sophistication*, not on fraud per se.

## Keepers

1. **A real detector has a jurisdiction** — preconditions (here: several orders of magnitude, multiplicative/mixed-scale generation) that are part of the tool, not fine print. Outside them, "FAIL" doesn't mean fraud; it means *out of jurisdiction* — and the test emits the same red flag either way. The 2020 misuse wasn't bad math; it was a true positive signal read from a place the detector doesn't cover.
2. **The viral failure mode is precondition-blindness**: the chart looks identical whether the precondition holds or not, so the violation is invisible in the output — the test cannot report its own inapplicability. (A check silent about its own eligibility.)
3. **Detection filters on adversary naivety**: any published statistical tell only catches fabricators who don't know it. The law's power in accounting partly *depends on its obscurity to the fraudster* — a detector whose strength decays as it becomes famous.
4. Origin charm: the law was first read off *physical wear* — the dirt gradient on logarithm-table pages was the histogram, recorded by use itself.

## Rhyme (flagged, not built)

An eligibility silence in the wild (the test can't flag its own out-of-jurisdiction state); detection-strength decaying with adversary knowledge (perfect-deception asymptote). Named, refused. This entry stays a digit table.
