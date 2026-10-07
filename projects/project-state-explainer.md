# Project State Explainer

> Structured, evidence-oriented project-state workflows for complex projects.

## Process transformation

Complex projects accumulate information across source control, tests, audits, issues, documentation, research notes, operational records, and project-management systems.

Those sources usually record **activity**. They do not automatically explain what the project can do now, which problems matter, whether a statement is still current, or which evidence supports a conclusion.

Project State Explainer (PSE) turns that manual interpretation and handover process into an explicit, reviewable workflow:

```text
Distributed project information
          |
          v
Human authoring / adapters / producers
          |
          v
Structured project-state model
          |
          v
Validation + provenance + freshness
          |
          v
Review / comparison / update lifecycle
          |
          v
Evidence-backed project-state explanation
```

The goal is not to replace existing project tools. PSE adds a structured explanation and review layer around information that already exists.

## Core engineering problem

The difficult part is not producing a summary.

Project information is heterogeneous, and no single project-management method or platform can be assumed. The system therefore needs a method-neutral boundary that can sit alongside existing file, CLI, source-control, and browser workflows.

State and authority also have to remain explicit. A working draft is not a reviewed snapshot; a reviewed snapshot is not verified truth; a missing problem is not necessarily a resolved problem; and a newer file is not automatically the authoritative project state.

PSE therefore models lifecycle, provenance, freshness, evidence, identity, and review status separately rather than collapsing them into a single notion of "current".

## Workflow and authority boundaries

Two implemented workflows illustrate the design.

### Human authoring

```text
Working Draft
    |
    v
Review
    |
    v
Human Reviewed
    |
    v
Project-state snapshot
```

Review authority applies only to the exact reviewed content. Editing the content invalidates that authority.

### Incremental update

```text
Accepted snapshot
    |
    v
Working Update
    |
    v
Added / Modified / Removed
    |
    v
Review Changes
    |
    v
Human Reviewed
    |
    v
Next snapshot
```

The accepted baseline remains immutable. There is no silent rebase to a newer state and no "continue anyway" path when identity or baseline constraints fail.

## Key engineering decisions

- **Determinism before inference.** The core can validate, compare, and render project state without requiring an LLM.
- **No invented project truth.** Contract validation means structural validity, not factual truth; evidence references provide traceability, not automatic proof.
- **Explicit human review.** Review is a modeled system state tied to exact content rather than an informal flag.
- **Immutable baselines.** Incremental updates remain bound to the exact accepted snapshot from which they started.
- **Authority is explicit, not inferred from recency.** File timestamps, filenames, size, or mere validity do not automatically establish the active state.
- **Fail closed on identity and state conflicts.** The system stops rather than selecting a likely replacement.
- **Local-first operation.** Core workflows require no mandatory cloud service or AI provider.
- **Compatibility over replacement.** Existing formats and workflows are extended incrementally rather than replaced by a new platform.

## My role

My contribution is primarily **product and system architecture, process design, technical steering, and quality governance**.

This includes defining the project-state semantics, lifecycle and authority boundaries, engineering contracts, acceptance criteria, review gates, integration decisions, recovery behavior, and test strategy, while directing AI-assisted implementation within those constraints.

## Current implementation

The current Python/browser implementation includes:

- structured project-state contracts with goals, achievements, problems, evidence, roadmap, decision gates, and dependencies;
- strict parsing and validation;
- deterministic rendering and comparison;
- provenance and freshness modeling;
- human-authoring and incremental-update lifecycles;
- a local project library and bounded discovery;
- browser views for overview, comparison, evidence, roadmap, decisions, and dependencies;
- CLI and batch processing;
- a core with **0 mandatory runtime dependencies**.

## Verification footprint

As supporting implementation evidence, the current repository contains:

- **51 Python production modules**
- **61 Python test modules**
- **13 browser/UI files**
- **8 test fixtures**
- latest full verification attributable to the current code state: **1,737 tests, 1 skipped, PASS**

These figures describe implementation and verification scope only. They are not presented as evidence of external product validation.

## Current state

PSE is under active development. Its internal technical validation is substantial, but the product has **not been externally validated as a finished market product**, and its ProjectLog v2 model remains Candidate/Draft.

No public claim is made about user adoption, time savings, ROI, production-scale performance, or superiority over existing project-management products.

## Public scope

This case study is intentionally limited to disclosure-safe architecture, workflow concepts, and aggregate implementation metrics.

Future examples and screenshots will use synthetic project data. The source code is not publicly released at this stage.
