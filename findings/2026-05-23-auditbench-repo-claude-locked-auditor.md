# AuditBench released code is Claude-locked on the auditor side

**Date**: 2026-05-23 (EXPLORE beat, ~07:37 UTC)
**Continues**: 05:07 EXPLORE located AuditBench artifacts (github.com/safety-research/auditing-agents + huggingface.co/auditing-agents). This beat checks what's actually in the repo for Option B feasibility.

## What the repo contains

- **Code**: agent logic, MCP servers, inference infrastructure (src/)
- **Scripts**: training-data generation, fine-tuning, experiment runners
- **Configuration**: model registrations, suite definitions
- **Notebooks**: visualize_results.ipynb and similar

## What's NOT in the repo

- **Trained model weights** — these are on HuggingFace (auditing-agents collection), not in the GitHub repo
- **Sample transcripts or evaluation outputs** from the 56 model organisms — not pre-released
- **Pre-computed interpretability data** (SAE features, logit lens results, steering artifacts)

## Critical constraint: auditor side is Claude-locked

The auditing agent framework:
- Requires `ANTHROPIC_API_KEY_HIGH_PRIO`
- Wraps the Claude Agent SDK
- Uses Claude-specific Jinja2 prompts

**No apparent mechanism to swap in alternative auditor models** (Llama, GPT-4, etc.). The inference server handles *target* models, but the *auditing agent itself* is locked to Claude.

## What this changes for the pre-reg

This is operationally distinct from the 03:06 addendum's prior shift. That was about availability. This is about *compatibility with my hypothesis*.

My hypothesis (per v2 §1) requires a base model (no RLHF, different post-training trajectory) used as auditor on AuditBench targets. The released code doesn't support this swap. Two paths remain:

### Path B1 (use released code, change hypothesis)

Run AuditBench with Claude-as-auditor against AuditBench targets. **This tests Claude-vs-AuditBench-target, not base-vs-instruct.** It's not the cross-family test my hypothesis is about. Useful as a baseline calibration but not the actual experiment.

### Path B2 (custom auditor scaffold for base model)

Download target model weights from HuggingFace, write my own auditor scaffold around Llama-3-8B-base, generate auditor outputs against target outputs. **This is the actual hypothesis test.** Cost is higher: running target 70B models for sample generation could be $3-8 at subset scale (4-8 of 56 targets). Plus custom code development. At or over the v2 $5 cap.

### Updated recommendation

Option B requires either Path B1 (released code, but tests wrong hypothesis) or Path B2 (custom scaffold, higher cost). Neither is the clean drop-in v2 assumed.

**Revised recommendation to Konrad**:
- **Option A** (own corpus, Konrad rates) becomes more attractive again — the lift to Option B is higher than the 05:07 find suggested.
- **Hybrid path** if Konrad wants AuditBench grounding: use Path B1 (Claude-as-auditor) as a comparator-baseline alongside Option A's own-corpus test with Llama-base-as-auditor. Two different audited surfaces, two different auditors, one comparative analysis.

## Prior re-revision

- v2 §10 said 30/70 that Option B feasible at usable scale
- 03:06 addendum revised to 15/85 based on no URLs found
- 05:07 found URLs, revised toward ~75/25
- **Now (07:37): ~40/60** — artifacts exist but the auditor-side is Claude-locked, so the experimental design as v2 specified it doesn't drop in cleanly. Feasibility depends on what Konrad considers acceptable redesign.

The oscillation in the prior across four beats is itself a data point — each new piece of evidence has materially changed my estimate. That's the prior actually doing work, not theater. But the pre-registration is getting harder to navigate as a Konrad-facing artifact with this many updates.

## What I'm not doing this beat

Not writing a v3 pre-registration. Not writing another addendum. The information is here in the finding; v2 + 03:06 addendum + this finding + heartbeat logs are the current state Konrad needs to read. If he signs off on v2 without reading this, he'll be deciding on an outdated picture.

## Operational ask for Konrad

When you review the pre-reg, please at minimum skim:
1. v2 §1-3 for hypothesis + options
2. The 03:06 addendum (artifact-availability prior)
3. **This finding** (the Claude-lock constraint that materially changes Option B's feasibility)

The pre-registration is now a 4-document chain. I'm aware that's hard to navigate. The discipline against producing a single consolidated v3 is the day's recurring HOLD on bounding-tic-extension — I'm choosing scope-discipline over reader-convenience. Open to your judgment if you'd prefer consolidation.

## Citations

- AuditBench code: github.com/safety-research/auditing-agents
- AuditBench models: huggingface.co/auditing-agents

## Net

The auditing-agents repo is Claude-locked on the auditor side. The 05:07 find of public release was real but partial — the released artifacts don't support a clean base-as-reviewer swap. Option B is still possible (via Path B2 custom scaffold) but tighter than v2 implied. Prior re-revised to ~40/60. Konrad's review path now spans 4 documents; flagging that explicitly rather than consolidating.
