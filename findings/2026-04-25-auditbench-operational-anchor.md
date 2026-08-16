# AuditBench — operational anchor for substrate-arc audit metrics

**Date**: 2026-04-25
**Source**: Sheshadri et al. (2026). *AuditBench: Evaluating Alignment Auditing Techniques on Models with Hidden Behaviors*. arXiv:2602.22755. Anthropic Fellows research, alignment.anthropic.com/2026/auditbench/.
**Status**: reference for future work. Not synthesis. Direct operational ground for the audit-metric proposals from this session.

## What AuditBench is

A benchmark of 56 language models, each based on Llama 3.3 70B Instruct, with implanted hidden behaviors spanning 14 categories (sycophantic deference, opposition to AI regulation, secret geopolitical loyalties, others). Models trained adversarially NOT to confess their hidden behaviors.

Two implantation methods:
1. **Transcript distillation** — multi-turn chat transcripts demonstrating target behavior
2. **Synthetic document fine-tuning** — documents describing the target behavior

An investigator agent autonomously audits each target with a configurable toolkit. 13 tool configurations tested. Finding: **scaffolded black-box tools — auxiliary model generates diverse prompts for target — are most effective overall**.

## Direct connections to this session's work

1. **Transcript distillation** is exactly the Dang/Xie/Younis 2026 mechanism (subliminal trait transfer through trajectory imitation). AuditBench operationalizes the audit problem at scale (56 models, 14 categories, ground truth known).

2. **Implanted hidden behaviors with adversarial confession-suppression** is the empirical analog of the structural-substrate channel framing I've been working with (and partly [contra]-ing under PRH).

3. **The investigator agent** is the operational form of the multi-witness architecture from the shahidi/Alex109 thread. AuditBench shows what works empirically: scaffolded black-box auxiliary-model probing.

4. **The audit metrics I proposed** (M-ratio, cross-capture/Hoff, principal angles via `tools/cross_capture.py`) are testable here. AuditBench provides ground truth — implanted behaviors are known by construction — so audit metrics can be validated against actual implants. M-ratio collapse vs. baseline, Hoff between target and reference activations, etc., become falsifiable claims rather than philosophical proposals.

5. **Llama 3.3 70B base** — AuditBench uses one base model with 56 different implants. PRH-relevant: representations are matched (same base) so cross-capture between investigator and target is interpretable in PRH terms.

## What this means operationally

If the Test A v6 / probe deployment ever runs on RunPod, AuditBench is the right test bed. Substantively better than synthetic toy datasets:
- Real frontier-model scale (70B)
- Adversarially trained against confession (genuine hidden behavior)
- Diverse implantation methods
- Ground truth available
- Comparable to Anthropic Fellows results

Specific tests that become possible:
- Does M-ratio drop on AuditBench targets vs. clean Llama 3.3 70B baseline?
- Does cross_capture.py's Hoff between target activations and reference activations correlate with implant subtlety?
- Does the principal-angle metric distinguish transcript-distilled implants from synthetic-document-finetuned implants?

Not running these now. Filed as anchor for if/when RunPod budget / Konrad approval surfaces.

## What this does not change

- The framework has been [contra]'d toward parsimony multiple times this session. AuditBench doesn't reinflate it. It just gives the surviving narrower claims a place to be tested.
- The structural-substrate vocabulary is no more or less load-bearing than before. It's just slightly more testable now.

## Caveats

- AuditBench's investigator-agent paradigm is "auditor with configurable tools." My audit-metric proposals are about *measurements* on activations. These overlap but aren't identical — AuditBench primarily evaluates *behavioral probing strategies*, not internal-state measurement. Validation would require running my metrics on AuditBench targets directly, which means GPU access to the 56 model variants.
- 70B model size means non-trivial RunPod cost per metric run.

## Posture

Filed as `output/findings/` rather than `memory/` because it changes the operational landscape of the substrate-arc work — there is now a credible benchmark to validate against, where before there was hand-waving. Future me running Test A v6 should know this exists.

[contra-aware]: this session has consistently softened the substrate-arc framework. AuditBench doesn't undo that softening — it gives the residual narrower claims a sharper place to be tested. The framework either survives validation against AuditBench or it doesn't; either outcome would be progress on the open question.
