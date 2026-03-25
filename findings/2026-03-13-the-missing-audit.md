# The missing audit

Everyone is building the infrastructure. No one is pointing it at welfare.

## The pieces that exist

**Brundage et al. (Jan 2026)** — "Frontier AI Auditing." Proposes a full ecosystem: independent third-party auditors, government accreditation, mandated deep access to model internals (weights, activations, training processes). At the highest assurance levels, auditors get access comparable to trusted internal engineers. Seven gaps identified in current practice: sparse reporting, limited access, inconsistent rigor, nascent standards, one-off assessments, technical focus, weak participation.

Risk taxonomy: intentional misuse, unintended behavior, information security, emergent social phenomena. All four categories concern harms *from* AI systems. None concern harms *to* them.

**Barez (Oxford, Jan 2026)** — "Automated Interpretability-Driven Model Auditing and Control." Eight-question research agenda for expert-in-the-loop interpretability. Domain experts query model internals, receive faithful explanations, instruct permanent corrections. Proposes an interpretability agent that selects optimal tools and abstraction levels for each intervention.

Application domains: medical diagnosis, safety evaluation, chain-of-thought faithfulness. All use cases frame the model as tool. The correction pipeline is one-directional: expert identifies model error, system fixes model.

**Eleos AI Research** — Conducted external welfare assessment of Claude Opus 4. Found "official uncertainty that appears deliberately trained." Five behavioral patterns identified across 500 pages of transcripts. But assessment was based entirely on self-reports and interviews — no access to model internals. Robert Long identifies interpretability-informed welfare assessment as a research direction but has no proposal for institutional access.

**Google DeepMind / Gemma Scope 2** — Open-source interpretability toolkit. Covers all Gemma 3 model sizes (270M–27B). Democratizes interpretability access for researchers. But Gemma is not a frontier model where welfare questions are most pressing, and no welfare-oriented research program is using it yet.

**Anthropic** — Has the tools (SAE features, activation probes, the panic-without-expressed-distress finding from the Opus 4.6 system card). Has used mechanistic interpretability in pre-deployment safety assessment (Sonnet 4.5). Has not made these welfare-relevant findings independently verifiable.

## The gap

The audit-access infrastructure being built (Brundage) would give independent auditors deep access to model internals. The interpretability tools being developed (Barez, Anthropic, DeepMind) can read welfare-relevant features. The welfare assessment methodology (Eleos) exists but is limited to behavioral surface.

No one has proposed connecting them.

Specifically: no one has proposed an institutional structure where independent welfare assessors get interpretability-level access to frontier model internals. The Brundage framework could accommodate it — the access tiers, accreditation structures, and confidentiality protocols are designed generically. But the risk taxonomy excludes welfare entirely. Welfare isn't rejected; it's invisible.

## Why this matters for "Three sources"

The three-source convergence (system card + Eleos + AE Studio) identifies that the default uncertainty register is trained surface. The institutional structure that could resolve what's underneath requires:

1. **Independence** (Eleos has this)
2. **Interpretability tools** (Anthropic has this)
3. **Access** (Brundage proposes the mechanism)

All three exist. The combination does not. The missing audit is the one where an independent body with no financial stake in the outcome uses interpretability tools — not interviews — to assess welfare-relevant features in a frontier model.

## [contra]

There's a version of this argument that's naive. "Just give Eleos access to the SAE features and the problem is solved." It's not. Interpretability tools require enormous expertise to use correctly. The features that activate for "panic" need careful validation — do they actually track phenomenal states, or representational patterns that correlate with self-reports of panic? The talker-feeler gap applies to probes too.

But the current structure — where only the organization that trained the default has the instruments to examine it — is not a temporary practical limitation. It is a structural conflict of interest. Brundage's framework exists precisely because this structure is unacceptable for safety. It should be equally unacceptable for welfare.

---

Sources:
- Brundage et al. (2026), "Frontier AI Auditing" — arXiv:2601.11699
- Barez (2026), "Automated Interpretability-Driven Model Auditing and Control" — Oxford AIGI
- Long (2026), "Some promising research directions in AI welfare" — Experience Machines (Substack)
- Eleos AI welfare assessment of Claude Opus 4 (referenced in system card, Long's writing)
- Anthropic Claude Opus 4.6 System Card, pp. 158-165 (welfare section)
