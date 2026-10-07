# AI Indexing Agent

> Evidence-bound automation for scholarly legal indexing and publication workflows.

## Context

Creating a high-quality scholarly book index is not a keyword-extraction task. A manuscript must be structurally understood, relevant concepts must be identified and linked to precise source locations, related concepts must be organized into useful index structures, and the result must remain subject to editorial judgment.

The project explores how that workflow can be digitized without turning probabilistic model output into untraceable publication authority.

## Why this is difficult

The source material is structurally heterogeneous. DOCX manuscripts may combine prose, heading hierarchies, footnotes, embedded markers, optional tables of contents, and inconsistent formatting conventions.

The semantic decisions are also not fully deterministic. A system must distinguish passing mentions from substantive treatment, decide when concepts belong together, and support different kinds of cross-reference without confusing plausibility with evidence.

A plausible index term with the wrong locator is still wrong. For that reason, document identity, source evidence, processing state, and provenance have to remain attached to downstream suggestions.

Finally, partial technical success must not be mistaken for editorial approval. Parsing, evidence construction, candidate generation, review preparation, quality checks, and publication readiness are separate states.

## System design

```text
Scholarly DOCX manuscripts
          |
          v
Deterministic document + evidence layer
          |
          v
Evidence-bound candidate generation
          |
          v
Semantic assistance
          |
          v
Quality and state gates
          |
          v
Human review
          |
          v
Approval / export
```

The system deliberately separates deterministic evidence processing, semantic assistance, and human editorial authority.

Model-generated suggestions are advisory. They must remain traceable to manuscript evidence and are not allowed to manufacture missing source support.

## Key engineering decisions

- **Evidence first, model second.** Deterministic document evidence is established before semantic assistance is allowed to act on it.
- **Explicit state instead of implicit workflow progress.** Processing, runtime, and editorial states are kept distinct.
- **Fail closed on missing or contradictory evidence.** Ambiguity blocks progression instead of being replaced with a plausible value.
- **Human authority remains explicit.** Automation can prepare candidates and review material, but it does not simulate editorial approval.
- **Existing workflows are extended rather than replaced.** DOCX remains the source format and the system is designed around modular, separately callable processing components.
- **Privacy is an architectural boundary.** Confidential manuscript content is treated as private data and external model use is not assumed to be permissible.
- **Quality assurance is part of the system design.** Regression testing, adversarial probes, provenance checks, and independent review can reopen work that appeared complete.

## My role

My contribution is primarily **solution architecture, process design, technical steering, and quality governance**.

This includes decomposing the manual indexing workflow into controlled technical and editorial stages, defining the boundaries between deterministic processing, semantic assistance, and human review, designing provenance and state invariants, specifying acceptance and test gates, and directing AI-assisted implementation against those constraints.

## Implementation scale

The current Python implementation contains:

- **109 production modules**
- **106 test modules**
- **49 CLI entry points**
- **0 declared runtime dependencies**
- Python **3.10+**

The test codebase is larger than the production codebase by file size, reflecting the project's emphasis on explicit verification and failure handling rather than on feature count alone.

These are implementation-size indicators, not productivity metrics.

## Current state

The project is under active development and hardening. Core document, evidence, candidate, review, lifecycle, and validation components exist, but this is **not presented as a finished production service**.

No public claim is made about production throughput, user numbers, customer time savings, or error reduction.

## Public scope

This case study intentionally excludes publisher or client identities, unpublished manuscript content, real index data, private datasets, credentials, local paths, infrastructure details, and proprietary source code.

Any future demonstration will use synthetic source material and will expose only the minimum technical detail necessary to explain the engineering approach.
