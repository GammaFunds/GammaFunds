# Project State Explainer (PSE)

> Deterministic, evidence-backed project intelligence for complex digital transformation — local-first, without AI, and with a strategic focus on public administration.

**Mission.** Make digital transformation projects easier to understand, govern, and hand over by distinguishing documented activity from demonstrated progress, decision authority, and measured outcomes.

**Product direction.** PSE is a local-first, method-neutral explanation and review layer around existing project information. The long-term ambition is a commercially viable **Project Intelligence & Decision Platform**: broadly useful across sectors, with public-sector digitalization as a primary application domain.

**AI-free by design.** PSE works without language models, model APIs, or mandatory cloud services. Its project-state interpretation, validation, history, reports, and planned intelligence features are to be implemented through explicit data contracts and deterministic, reviewable rules. AI features are **not part of the current product roadmap**. Using AI tools during software development does not make them dependencies of the PSE product.

**Maturity.** Active engineering prototype. The platform is **not** presented as a finished commercial product, a validated public-sector deployment, or a substitute for existing project-management systems.

## Why this project exists

Digital transformation projects often span administrative departments, IT service providers, vendors, governance bodies, and changing project teams. Information is scattered across source control, tests, audits, issues, project reports, decisions, documentation, and operational records.

These sources primarily describe **activity**. They do not, on their own, establish what a project can do now, which decisions remain unresolved, whether an earlier conclusion is still current, or which evidence supports a claimed result.

That gap is particularly consequential in public administration. A service can be implemented without being formally accepted, accepted without being operationally available, and launched without evidence that it improves the experience of citizens or staff.

PSE aims to make these distinctions explicit, without requiring an organization to replace the tools and methods it already uses.

## The process transformation

The intended workflow is an evidence-oriented chain:

1. **Distributed project information** — reports, decisions, technical artifacts, tests, operational records, and other sources.
2. **Controlled input** — human authoring, with source adapters and automated producers introduced only under defined contracts.
3. **Structured project state** — goals, achievements, problems, evidence, roadmap items, decisions, dependencies, and lifecycle state.
4. **Validation and provenance** — structural checks, exact identity, source references, freshness, and conflict handling.
5. **Review and comparison** — explicit human authority, immutable accepted baselines, and bounded updates.
6. **Project-state explanation** — traceable views of what is documented, what has changed, what remains uncertain, and what requires attention.

The core distinction is deliberate: **a valid record is not necessarily a true claim; a cited source is not necessarily verification; and a reviewed snapshot is not proof of external reality.**

### Example: an online public service

For a hypothetical digital application service, PSE should be able to distinguish the evidence for:

| Question | Relevant project state |
| --- | --- |
| Has the functionality been built and tested? | Technical delivery |
| Has the responsible department accepted the exact deliverable? | Formal or functional acceptance |
| Are operational, security, and integration prerequisites satisfied? | Service readiness |
| Can people actually use the service? | Availability and adoption |
| Did it reduce waiting time, manual work, or media breaks? | Measured outcomes |

These are **separately evidenced questions**, not automatic stages where one success proves the next. The ability to compare delivery with real-world outcomes is part of the future product vision, not a claimed current capability.

## Engineering foundation: explicit state and authority

The difficult part is not generating a plausible summary. It is preserving identity, evidence, review authority, and lifecycle boundaries across heterogeneous information.

Two implemented workflows illustrate this approach:

**Human authoring:** Working Draft → Review → Human Reviewed → Project-state Snapshot.

Review authority is bound to the **exact reviewed content**. Editing that content invalidates the previous authority.

**Incremental update:** Accepted Snapshot → Working Update → Added / Modified / Removed → Review Changes → Human Reviewed → Next Snapshot.

An accepted baseline remains immutable. An update cannot silently substitute a different baseline, infer authority from a newer timestamp, or continue past an identity conflict.

Key design decisions include:

- **Deterministic core, no AI dependency.** Validation, comparison, rendering, and planned project-state analysis operate on explicit records and reproducible rules, not generated answers.
- **No invented project truth.** Source references provide traceability; structural validity and human review do not automatically verify factual claims.
- **Explicit lifecycle and authority.** Draft, reviewed, accepted, observed, and externally verified states must not be conflated.
- **Immutable baselines and bounded updates.** Identity and accepted content remain stable through review and change workflows.
- **Freshness and uncertainty are visible.** A newer file is not automatically authoritative; absent evidence is not evidence of resolution.
- **Fail closed on material conflicts.** The system does not guess its way through ambiguous identity or state.
- **Local-first, data-minimizing operation.** Core workflows require no cloud service or AI provider; unnecessary collection, retention, and transmission of project information should be avoided.
- **Compatibility over replacement.** PSE is designed to work alongside existing organizational processes and tools.

## Current implementation

The Python/browser prototype already includes foundations for:

- structured project-state contracts covering goals, achievements, problems, evidence, roadmap, decisions, and dependencies;
- strict parsing, validation, deterministic rendering, and comparison;
- source provenance, freshness modeling, and explicit review-state handling;
- human-authoring and incremental-update lifecycles;
- a local project library with bounded discovery;
- browser views for overview, comparison, evidence, roadmap, decisions, and dependencies;
- CLI and batch processing, with **zero mandatory runtime dependencies for the core**.

A read-only, single-state **Cover Flow V7** and an initial **Project Flow window lifecycle** have also been developed on a feature branch. The broader desktop experience is still under visual refinement and product acceptance. A successful internal engineering check must not be confused with an installed-runtime, accessibility, or external product acceptance.

These are implementation foundations, **not** evidence that the premium modules below are already available.

## Product vision: from project records to decision intelligence

The proposed commercial product combines a common, AI-free project-state core with complementary **deterministic** analysis capabilities. These are not model-generated recommendations; they depend on explicit source records, review authority, and rule-based evaluation.

| Proposed capability | Intended value |
| --- | --- |
| **Evidence & Consistency Engine** | Compare documented claims with available evidence from project records, code, tests, CI, and other explicitly authorized sources; expose inconsistencies, uncertainty, and verification limits rather than claiming omniscient truth. |
| **Project Time Machine** | Reconstruct accepted historical states and explain what changed, why, and with which documented consequences. |
| **Decision & Dependency Analysis** | Connect decisions, blockers, responsibilities, dependencies, and milestones through recorded relationships; distinguish documented consequences from explicitly hypothetical scenarios. |
| **Architecture & Change Explorer** | Relate technical components, integrations, and changes to project objectives, decisions, risks, and evidence. |
| **Project Portfolio Analysis** | Compare projects and cross-organizational dependencies without collapsing incompatible states into misleading aggregate progress scores. |
| **Project Continuity** | Generate deterministic, evidence-bound handovers showing the accepted baseline, implementation state, known invariants, open blockers, reviews, and bounded next steps across personnel or team changes. |
| **Outcome & Impact Evidence** | Separate delivery and adoption from measured benefits, and trace outcome claims to actual metrics rather than assuming that completed tasks imply public value. |

**Status of this table:** strategic roadmap, **not a list of shipped features**. Several concepts build on implemented state, comparison, evidence, or browser foundations; cross-source reconciliation, rule-based dependency analysis, technical architecture mapping, portfolio analysis, and measured-outcome evaluation still require separate design, implementation, and validation.

### Project Continuity as a practical differentiator

A project handover should answer: What was actually implemented? Which tests and reviews support that assessment? Which decisions are binding? What remains blocked? Which baseline and scope govern the next change?

A future PSE handover could assemble these answers with exact source and revision identities, making transitions between teams, vendors, or delivery phases more reliable. It must never manufacture a test result, authorization, or completed milestone.

## Product focus and commercial hypotheses

The intended **GovTech** application is project intelligence for public-sector digitalization: program steering, decision transparency, multi-stakeholder dependencies, handovers, and evidence-based assessments of service readiness and outcomes.

The same core can serve **software teams, technical consultancies, IT project leaders, and cross-project portfolios**. Engineering environments offer an early opportunity to evaluate precise Git, test, and review evidence; public-sector workflows provide the long-term mission and a demanding validation context.

Possible commercial offerings — **Core, Pro, Team, Gov, and Enterprise** — remain hypotheses rather than available plans or tested pricing. Public-sector adoption would also require appropriate procurement, accessibility, privacy, security, support, and deployment assessments. None of those requirements is claimed to be fulfilled merely by the current architecture.

A first meaningful external validation would test whether a new project stakeholder can identify an evidence-backed current state, important blockers, and the next decision more accurately and efficiently than with the existing information workflow. Measured outcomes, not visual appeal or feature count alone, should guide product prioritization.

## My role

My contribution is primarily **product and system architecture, process transformation, technical steering, and quality governance**.

This includes defining project-state semantics; lifecycle, identity, and authority boundaries; source and evidence contracts; acceptance and regression gates; integration and recovery strategies; and the public-sector-oriented product direction. I direct bounded engineering and independent reviews, including the use of AI coding tools where appropriate. Such development tools are not a PSE runtime or product requirement. Implementation evidence remains distinct from product validation.

## Current state and verification limits

PSE remains under active development. **ProjectLog v2 is still Candidate/Draft**, and external product validation is incomplete.

Automated regression tests, browser checks, and independent engineering reviews support individual implementation milestones. They do **not**, on their own, establish user adoption, operational readiness, accessibility compliance, public-sector suitability, time savings, return on investment, or superiority over existing tools.

Earlier repository-size and test-count figures were tied to an older development snapshot and are intentionally not reused here as current measurements. Any future public performance or quality claims should be tied to a dated, reproducible candidate and its exact verification evidence.

## Public scope

This case study covers disclosure-safe system design, workflow semantics, intended product capabilities, and engineering principles. Real project records, private operational context, credentials, and non-public source material are excluded. Demonstrations and product screenshots should use synthetic data.

The ambition is substantial, but the boundary is simple: **PSE should help people understand what is known, what is not yet established, what changed, and which decision matters next — without confusing a convincing explanation with proven reality.**
