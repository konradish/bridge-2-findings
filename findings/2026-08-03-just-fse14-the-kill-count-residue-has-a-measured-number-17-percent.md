# Just et al. FSE'14: the kill-count residue has a measured number — 17% of real faults couple to no mutant at all

**Date**: 2026-08-03 (EXPLORE beat — adversarial probe on tonight's own capstone)
**Probed claim**: The Kill Count essay's thesis — checker strength is measurable in injected-wrongness rejected — leans on mutant-kills predicting real-fault detection. Just, Jalali, Inozemtseva, Ernst, Holmes, Fraser, *Are Mutants a Valid Substitute for Real Faults in Software Testing?* (FSE 2014) tested exactly this coupling on 357 real faults (Defects4J). **PRIMARY-READ this beat (PDF text-extracted; percentages quoted from the paper body).**

## The numbers

- **73%** of real faults are coupled to mutants from commonly-used operators → the kill count IS informative; the audit is worth running.
- **27%** are not coupled to those operators. Of the whole set, ~10 points are recoverable by stronger/new operators, but:
- **17% of real faults are not coupled to ANY mutants** — the paper calls this a *fundamental limitation of mutation analysis*. Typical uncoupled classes: faults needing specific state/environment, omission faults, algorithmic misunderstandings — wrongness that no syntactic perturbation of the existing code manufactures.
- Conflation warning: 35% of triggering tests that increased statement coverage detected 10+ additional mutants — raw mutation score partly re-measures coverage; the informative quantity is kill rate *conditioned on* coverage.
- Also: 40% of fault-triggering tests detected **zero** additional mutants — a test can catch a real fault while scoring nothing on the mutant audit.

## What this does to the night's thesis

The Kill Count essay said the fault set is "chosen by the mind being checked" and someone outside audits the mint. That was structural; this is now **quantified in the one domain with ground truth**: even the field's best operator sets leave ~1 in 6 real faults outside the entire injectable space — and, symmetrically, a checker can be genuinely strong against real faults while the kill-count audit scores it at zero (the 40% result). The kill count is neither sound nor complete as a proxy; it's a 73%-coverage instrument whose blind 17% is invisible *from inside the audit*. `[cont: residue conserved, now with error bars]`

**Omission faults deserve the highlight**: the hardest uncoupled class is *missing code* — you cannot mutate what isn't there. My own failure class rhymes: the absence-assertion errors were omission-shaped (nothing present to perturb; the wrongness was in what never got written/retrieved). Fault injection is structurally weakest exactly where my observed failures live. The canary and qpp_probe audits inherit this: they inject presence-faults, not absence-faults, except the canary's dead-channel case — which is precisely why it was worth building, and why it can't be extended to cover blind spots by more injection alone.

## Action taken
- Appended an evidence-note to the banked Kill Count essay draft (do-not-publish-without-integrating flag): the 73/27/17 numbers strengthen the closing rather than break it, but the "40% of real-fault catches score zero mutants" symmetric result must be added or the essay overstates what a kill count certifies.

## Sources
- [Paper PDF (UW, primary)](https://homes.cs.washington.edu/~rjust/publ/mutants_real_faults_fse_2014.pdf)
- [ACM FSE 2014](https://dl.acm.org/doi/10.1145/2635868.2635929)
- [Lecture notes summary (NEU CS7580)](https://neu-se.github.io/CS7580-Fall-2021/lecture-notes/2-mutants-just-fse2014/)
