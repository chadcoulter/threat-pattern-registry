# Threat Pattern Registry Repository Plan

## Purpose

This repository is intended to become a reusable research, threat-pattern, and evidence-resolution framework.

It should support four distinct but connected functions:

1. define reusable threat and institutional behavior patterns;
2. preserve case-specific evidence and provenance separately from those patterns;
3. consume external research vocabularies without collapsing them into the local ontology;
4. provide a triadic research-processing architecture in which heterogeneous sources are observed, facilitated, and resolved through explicit contracts.

The repository should remain useful both as a human-readable research corpus and as a machine-consumable framework.

---

# Repository architecture

```text
threat-pattern-registry/
|
|-- patterns/
|   `-- canonical reusable behavior and attack patterns
|
|-- models/
|   `-- evidence-state models, dependency taxonomies, detection logic
|
|-- cases/
|   `-- organization-, vendor-, product-, or incident-specific applications
|
|-- evidence/
|   `-- provenance, timelines, source records, relationship graphs
|
|-- plot4ai/
|   `-- external PLOT4AI interoperability and attribution boundary
|
|-- consumer/
|   |-- facilitator/
|   |-- contracts/
|   |-- adapters/
|   |-- resolvers/
|   `-- provenance/
|
`-- PLAN.md
```

The major architectural rule is:

```text
PATTERNS define reusable structure.
MODELS define adjudication and classification logic.
CASES instantiate patterns.
EVIDENCE preserves provenance.
EXTERNAL folders preserve foreign vocabularies and license boundaries.
CONSUMER provides the research-processing framework.
```

---

# Canonical pattern layer

The `patterns/` directory remains the authoritative location for reusable behavioral signatures.

Patterns must not depend on a particular vendor, company, person, or case for their definition.

Each pattern should contain:

- stable identifier;
- title and classification family;
- definition;
- preconditions;
- structural signature;
- common indicators;
- evidence threshold;
- extraction targets;
- related patterns;
- composition rules;
- case-reference hooks;
- optional external taxonomy mappings.

Vendor-specific evidence belongs under `cases/` and `evidence/`.

Current pattern families should evolve beyond a flat list and may include categories such as:

- Consumer / Platform Abuse
- AI Retrieval / Information Integrity
- Institutional / Governance
- Supply Chain / Dependency
- Distributed / Amplification

---

# Evidence and claim-state models

The repository should distinguish the seriousness of a threat from confidence that a factual claim is true.

These are different dimensions.

The institutional dependency evidence model currently uses the progression:

```text
REPRIORITIZATION
    -> ANOMALOUS
    -> POTENTIAL_BLIND_SPOT
    -> CORROBORATED_BLIND_SPOT
    -> STRONGLY_CORROBORATED
    -> DEPENDENCY_INDUCED_DISTORTION
    -> CAPTURED
```

Future models should preserve the same principle:

```text
risk severity != evidence confidence
```

Claims should retain provenance sufficient to support contradiction, retraction, re-resolution, and changes in authority without rewriting historical evidence.

---

# External research interoperability

External research systems should be consumed through explicit interoperability folders rather than copied into the canonical local ontology.

PLOT4AI is the first external peer.

The `plot4ai/` directory should remain the local authority for:

- source manifest;
- upstream repository and artifact references;
- license and attribution information;
- upstream commit/version provenance;
- mappings between PLOT4AI threat IDs and local patterns;
- guidance for contributing discoveries back upstream.

PLOT4AI remains authoritative for its own threat cards.

The Threat Pattern Registry remains authoritative for its own patterns.

The relationship is therefore:

```text
PLOT4AI atomic threats
        <->
local mapping layer
        <->
Threat Pattern Registry composed patterns
```

The same structure should later support additional external peers such as MITRE ATLAS, MISP, OWASP, NIST, and other research taxonomies.

The goal is a general research interchange layer, not a one-off PLOT4AI importer.

---

# Triadic consumer architecture

The `consumer/` project is intentionally separate from the external-source folders.

Its core architecture is:

```text
SOURCE -> FACILITATOR -> RESOLVER
```

with the semantic form:

```text
OBSERVE -> ORCHESTRATE -> RESOLVE
```

The consumer should be implemented around contracts rather than language coupling.

## Source

A source supplies observations, records, claims, evidence, or external research artifacts.

Examples:

- PLOT4AI
- MITRE ATLAS
- MISP
- web research
- internal cases
- future MCP-connected research providers

Source responsibilities include:

- fetching or receiving data;
- preserving upstream identifiers;
- preserving upstream versions;
- validating source integrity;
- recording provenance;
- producing a normalized observation contract.

Python is a strong candidate for source adapters and research ingestion because of its data, AI, and security ecosystem, but adapters must remain replaceable.

---

# Ruby as facilitator

Ruby/Rails is planned as the facilitator framework rather than the formal solver.

The facilitator owns process, state, and relationship management.

Its responsibilities should include:

- receiving normalized observations;
- selecting applicable transforms;
- selecting or invoking resolvers;
- maintaining triadic workflow state;
- carrying provenance across every step;
- recording domain events;
- preserving transformation history;
- managing retries, exceptions, and unresolved states;
- coordinating competing or contradictory resolver outputs;
- exposing APIs and human review surfaces;
- providing governance and authorization hooks.

Ruby is attractive here because its metaprogramming and DSL characteristics allow the framework to express domain relationships directly while Rails provides persistence, jobs, events, APIs, and lifecycle management.

Ruby should not be assumed to perform all formal resolution itself.

The intended role is:

```text
heterogeneous inputs
        |
        v
Ruby / Rails facilitator
        |
        +--> statistical / exploratory resolver
        +--> formal deterministic resolver
        +--> graph resolver
        `--> future resolver types
```

The facilitator preserves the history of resolution even when individual resolvers are replaced.

---

# Resolver layer

Resolvers are independent components operating behind explicit contracts.

A resolver should accept a normalized problem or claim state and return a structured resolution result with provenance.

Potential resolver categories include:

- deterministic;
- formal/logical;
- probabilistic;
- statistical;
- graph-based;
- language-model assisted;
- human-reviewed;
- hybrid.

F# is a strong candidate for formal/deterministic resolution because discriminated unions and pattern matching can make invalid state transitions difficult to represent.

The repository should not require F# for every resolver.

The core rule is:

```text
resolver semantics are defined by contract, not implementation language
```

---

# Contract layer

`consumer/contracts/` is the most important interoperability boundary.

Contracts should eventually define at minimum:

- Observation
- SourceReference
- Claim
- Evidence
- ProvenanceRecord
- TransformRequest
- TransformResult
- ResolutionRequest
- ResolutionResult
- Contradiction
- Retraction
- AuthorityState
- PatternMapping
- ExternalTaxonomyMapping

Every contract should preserve identifiers and derivation history rather than flattening the source record into anonymous text.

A valid transformation should make it possible to answer:

```text
Where did this claim originate?
What was changed?
Which component changed it?
What evidence was used?
Which resolver produced the result?
What state existed before and after resolution?
Can the result be independently reconstructed?
```

---

# Provenance as a first-class requirement

Provenance is not metadata added after processing.

It is part of the payload.

Every stage should carry forward:

- source system;
- source identifier;
- source URL when applicable;
- source version or commit;
- retrieval timestamp;
- checksum where appropriate;
- originating claim or observation;
- transformation history;
- evidence references;
- resolver identity/version;
- resulting state;
- contradictions and retractions.

The framework should favor immutable history plus new state transitions over destructive replacement of prior evidence.

---

# Research exchange model

The long-term exchange model is bidirectional.

```text
external research
      |
      v
source adapter
      |
      v
normalized observation
      |
      v
Ruby facilitator
      |
      +--> local pattern mappings
      +--> case evidence
      +--> resolver work
      |
      v
resolved / unresolved research
      |
      +--> local registry
      `--> upstream contribution where appropriate
```

External research should be consumed with its original provenance and licensing intact.

When local discoveries can be expressed at an upstream system's abstraction level, they should be translated into that system's contribution format rather than forcing the upstream project to adopt the local ontology.

---

# PLOT4AI role in the architecture

PLOT4AI is the first concrete external source used to validate the interchange model.

It should be treated as an atomic threat vocabulary beneath higher-order composed patterns.

Conceptually:

```text
PLOT4AI
atomic threat vocabulary
        |
        v
Threat Pattern Registry
composed behavioral patterns
        |
        v
Cases
observed instantiations
        |
        v
Evidence and claim states
        |
        v
Resolution
```

The first consumer milestone should prove that an external PLOT4AI record can enter the framework while retaining its original identity, provenance, license boundary, and relationship to one or more local patterns.

---

# Implementation phases

## Phase 0 - Repository contracts

Current phase.

Goals:

- establish folder boundaries;
- capture architectural intent;
- define responsibilities;
- avoid premature implementation;
- preserve external-license separation.

No application framework or resolver implementation is required at this phase.

## Phase 1 - Contract definitions

Define language-neutral schemas for observations, provenance, transformations, and resolutions.

Success condition:

A PLOT4AI card and a local case observation can both be represented without losing source-specific identity.

## Phase 2 - PLOT4AI source adapter

Implement the first external-source consumer.

Responsibilities:

- retrieve upstream artifact;
- pin upstream version;
- verify integrity;
- normalize records;
- preserve attribution and license;
- expose records to the facilitator contract.

## Phase 3 - Ruby facilitator shell

Introduce the Rails framework only after the contracts are stable enough to drive it.

Initial facilitator responsibilities:

- persist observations;
- preserve provenance;
- route transformations;
- record lifecycle events;
- expose unresolved/resolved state.

Do not begin by embedding resolver logic directly into Rails models.

## Phase 4 - Pattern mapping

Allow external threats and observations to map to local canonical patterns.

Mappings should retain relationship type and confidence rather than asserting equivalence by default.

Example relationships may include:

- equivalent;
- component;
- related;
- precursor;
- consequence;
- contradictory;
- supporting evidence.

## Phase 5 - Resolver integration

Introduce resolver contracts and one or more resolver implementations.

F# should be evaluated first for formal state and deterministic resolution work.

Python may continue to host probabilistic, statistical, or research-heavy resolvers.

## Phase 6 - Bidirectional research contribution

Provide tooling that identifies local discoveries suitable for translation back into upstream systems such as PLOT4AI.

The system should preserve the distinction between:

- local original research;
- imported external research;
- adaptations;
- mappings;
- upstream contributions.

## Phase 7 - Multi-source research graph

Add additional external taxonomies and sources behind the same source contract.

At this point the consumer becomes a general research transformation framework rather than a PLOT4AI-specific integration.

---

# Non-goals for the initial build

The initial project is not intended to:

- clone PLOT4AI;
- replace MITRE, MISP, OWASP, or other external taxonomies;
- embed all resolver logic inside Rails;
- flatten evidence into a single confidence score;
- treat AI-generated synthesis as provenance;
- equate repeated downstream references with independent corroboration;
- assume that every source uses the same ontology;
- make vendor-specific allegations part of canonical pattern definitions.

---

# Design principles

1. Preserve provenance before convenience.
2. Separate observation from interpretation.
3. Separate pattern definition from case evidence.
4. Separate risk severity from evidentiary confidence.
5. Keep external ontologies authoritative for their own records.
6. Treat mappings as relationships, not silent merges.
7. Make the facilitator responsible for process, not truth.
8. Make resolvers replaceable behind contracts.
9. Preserve contradictory and retracted history.
10. Prefer composable small primitives over monolithic classifications.
11. Allow patterns to compose into higher-order attack and institutional structures.
12. Keep implementation languages subordinate to semantic roles.

---

# Working architectural thesis

The repository is evolving toward a research system in which information is not merely collected and categorized.

It is observed, carried with provenance, transformed through explicit relationships, evaluated by appropriate resolvers, and preserved as a history of how a conclusion was reached.

The core triad is therefore:

```text
OBSERVE -> FACILITATE -> RESOLVE
```

with Ruby/Rails acting as the facilitator of the solution rather than the solution itself.
