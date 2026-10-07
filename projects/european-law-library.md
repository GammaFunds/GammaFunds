# European Law Library

> A provider-neutral, auditable data pipeline for heterogeneous European legal sources.

## Process transformation

Official legal information is published through different authorities, portals, identifiers, formats, language models, versioning schemes, and retrieval interfaces.

Without an integration layer, each source has to be discovered, retrieved, interpreted, and tracked separately. European Law Library (ELLi) turns that fragmented process into a common, traceable pipeline:

```text
Official legal source
        |
        v
Discovery
        |
        v
Retrieval
        |
        v
Immutable raw evidence
        |
        v
Source record + provenance
        |
        v
Canonical legal model
        |
        v
Activation / revision state
        |
        v
Provider-neutral search + read interface
```

The goal is not to hide source differences. It is to isolate provider-specific behavior at the system boundary while preserving provenance and exposing a stable legal-information model downstream.

## Core engineering problem

The difficult part is not downloading documents.

A provider document, an observed retrieval, a canonical legal act, a revision, and an individual provision are different objects. Retrieval time is also not the same thing as legal validity time.

The platform therefore has to preserve source identity, version semantics, language, provenance, and legal-time boundaries while ingesting structurally different provider formats.

Reliability becomes more difficult because network retrieval, object storage, and PostgreSQL do not form one global transaction. Partial failure can leave an operation in an uncertain state, so retry behavior has to be idempotent and reconciliation has to precede unsafe repetition.

At corpus scale, parsers and resolvers must also handle real source irregularities without silently changing legal meaning.

## System design

The current TypeScript/PostgreSQL architecture separates:

- **Discovery** — identifies available source documents and retrieval candidates.
- **Provider adapters** — isolate provider-specific retrieval, versioning, and parsing behavior.
- **Raw evidence storage** — preserves retrieved bytes before canonical transformation.
- **Source records and provenance** — bind source identity, retrieval observations, and evidence.
- **Canonical legal model** — separates legal acts, provisions, revisions, content sets, provision versions, and external identifiers.
- **Activation pipeline** — promotes verified source material into canonical read models.
- **Provider-neutral read layer** — serves legal-act, provision, structure, source, and legal-time information without live provider dependency.
- **API and worker processes** — support search/read access and automated discovery, retrieval, bulk, and activation workflows.

## Key engineering decisions

- **Provider identities remain separate from canonical legal identities.**
- **Raw source material is preserved before transformation.**
- **Provenance remains attached across ingestion and activation boundaries.**
- **Retrieval time and legal validity time are modeled separately.**
- **Unknown legal-time state remains unresolved rather than defaulting to "current".**
- **Missing language does not silently fall back to another language.**
- **Ambiguity is surfaced instead of auto-resolved.**
- **Unknown mutation outcomes trigger reconciliation before retry.**
- **Public read paths use canonical data after activation rather than reaching back to providers.**
- **Narrow normalization fixes source-format irregularities without broad semantic rewriting.**

## My role

My contribution is primarily **solution architecture, process design, technical steering, and quality governance**.

This includes defining the target architecture; separating discovery, retrieval, persistence, activation, and read responsibilities; designing provenance, identity, version, legal-time, language, and authority boundaries; setting task and interface scopes; defining test and acceptance criteria; directing AI-assisted implementation; and using runtime evidence and independent review to accept, reject, or reopen technical work.

## Real data integration

The platform has been exercised against real official legal sources rather than synthetic provider fixtures alone.

Verified corpus snapshots include:

- **Germany:** 6,137 legal acts and 92,395 provisions
- **Switzerland:** 5,337 works and 124,142 provisions
- **Germany + Switzerland:** **216,537 canonical provisions**
- **EU AI Act:** a production-like CELLAR vertical slice from official source retrieval through canonical activation and provider-neutral public reads

For the EU AI Act (`CELEX 32024R1689`), **93 German article provisions** were activated into the canonical model and **93/93 public provision reads** succeeded. CELEX resolution, search, legal-act reads, and structure reads were also verified.

The completed public read path required:

- **0 provider requests**
- **0 raw-evidence store reads**
- **0 database mutations**

Provenance remained traceable to the underlying source record. Missing language remains explicitly unavailable rather than silently falling back, and unknown legal validity remains unresolved rather than being treated as current.

## Verification footprint

As supporting implementation evidence, the current backend tree contains:

- **246 tracked files**
- **194 TypeScript/TSX files**
- **85 TypeScript test files**
- **13 SQL migrations**
- **45 TypeScript files in the source-adapter package**
- **8 packages**
- **2 backend applications**: API and worker

These figures describe implementation scope only.

## Example: acceptance finding from real source data

A real EU read-path acceptance run exposed a structured-label edge case in which a non-breaking space prevented an otherwise valid article lookup.

The correction deliberately kept exact matching as the fast path and added only bounded whitespace normalization. Case, punctuation, abbreviations, language, type scope, and ambiguity semantics remain distinct.

The fix was independently reviewed and validated with **360 relevant resolver/API tests**, typechecks, linting, and formatting checks.

This illustrates the project's quality approach: use real source evidence to expose narrow interoperability failures, then correct only the demonstrated failure mode and regression-test the boundary without rewriting persisted source data.

## Current state

The platform is under active development. German and Swiss corpora have been processed, and the EU AI Act now provides a completed, production-like end-to-end vertical slice through the provider-neutral read path.

No public claim is made about measured user time savings, ROI, or a finished production service.

## Public scope

This case study is limited to disclosure-safe architecture, provider-integration concepts, aggregate corpus metrics, and verified engineering characteristics.

Private runtime configuration, infrastructure details, internal identifiers, operational logs, cached source corpora, and source code are not part of this public portfolio.

## Related public project

[European Law Lookup](https://github.com/GammaFunds/European-Law-Lookup) is an earlier public implementation in the same legal-information domain. The Obsidian plugin integrates official legal-text sources from the EU and several European jurisdictions and provides a publicly inspectable example of source-aware retrieval and provider integration that preceded the broader platform work.
