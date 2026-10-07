# AI Indexing Agent

> Controlled digitalization of a complex scholarly legal indexing workflow.

## Process transformation

The project starts from an existing, document-based publishing workflow rather than from a greenfield software problem.

A scholarly manuscript has to be structurally understood, relevant concepts have to be linked to precise source locations, semantic relationships have to be reviewed, and the final result remains subject to editorial approval. The engineering task is therefore to make that process more structured and automatable without detaching decisions from their source evidence.

The workflow is decomposed into explicit technical and editorial stages:

```text
DOCX intake
    |
    v
Deterministic document + evidence processing
    |
    v
Evidence-bound candidate generation
    |
    v
Semantic assistance
    |
    v
Quality + state gates
    |
    v
Human review
    |
    v
Approval / export
```

The existing DOCX/file workflow remains the operational boundary. Automation is introduced only where the result can remain traceable, reviewable, and safely integrated into that workflow.

## Core engineering problem

The difficult part is not generating plausible index terms with a language model.

The source material is structurally heterogeneous. DOCX manuscripts may combine prose, heading hierarchies, footnotes, embedded markers, optional tables of contents, and inconsistent formatting conventions.

The semantic decisions are also not fully deterministic. A system must distinguish passing mentions from substantive treatment, decide when concepts belong together, and support different kinds of cross-reference without confusing plausibility with evidence.

A plausible index term with the wrong locator is still wrong. Document identity, source evidence, processing state, and provenance therefore remain attached to downstream suggestions.

Partial technical success must also not be mistaken for editorial approval. Parsing, evidence construction, candidate generation, review preparation, quality checks, and publication readiness are separate states.

## System boundaries

The architecture deliberately separates:

- **deterministic evidence processing** from semantic model decisions;
- **technical lifecycle state** from editorial state;
- **automation** from human approval authority;
- **recoverable uncertainty** from evidence that is insufficient to proceed.

Model-generated suggestions are advisory. They must remain traceable to manuscript evidence and are not allowed to manufacture missing source support.

## Key engineering decisions

- **Evidence first, model second.** Deterministic document evidence is established before semantic assistance acts on it.
- **Explicit state instead of implicit workflow progress.** Processing, runtime, and editorial states remain distinct.
- **Fail closed on missing or contradictory evidence.** Ambiguity blocks progression instead of being replaced with a plausible value.
- **Human authority remains explicit.** Automation prepares candidates and review material but does not simulate editorial approval.
- **Existing infrastructure is extended rather than replaced.** DOCX remains the source format and modular processing components fit around the existing file workflow.
- **Provenance is part of the data model.** Suggestions remain tied to source identity and evidence across processing boundaries.
- **Privacy is an architectural boundary.** Confidential manuscript content is treated as private data and external model use is not assumed to be permissible.
- **Quality assurance can reopen work.** Regression testing, adversarial probes, provenance checks, and independent review may block progression even after an apparently successful implementation step.

## My role

My contribution is primarily **solution architecture, process design, technical steering, and quality governance**.

This includes decomposing the manual indexing workflow into controlled technical and editorial stages, defining the boundaries between deterministic processing, semantic assistance, and human review, designing provenance and state invariants, specifying acceptance and test gates, and directing AI-assisted implementation against those constraints.

## Current state

The project is under active development and hardening. Core document, evidence, candidate, review, lifecycle, and validation components exist, but this is **not presented as a finished production service**.

No public claim is made about production throughput, user numbers, customer time savings, or error reduction.

## Technical footprint

As supporting implementation evidence, the current Python codebase contains:

- **109 production modules**
- **106 test modules**
- **49 CLI entry points**
- **0 declared runtime dependencies**
- Python **3.10+**

These figures describe implementation scope only. They are not presented as productivity or quality metrics.

## Public scope

This case study intentionally excludes publisher or client identities, unpublished manuscript content, real index data, private datasets, credentials, local paths, infrastructure details, and proprietary source code.

Any future demonstration will use synthetic source material and expose only the minimum technical detail necessary to explain the engineering approach.
