---
title: "Threat Pattern Registry"
status: "provisional"
version: "0.5"
---

# Threat Pattern Registry

This directory contains canonical threat-pattern and defensive-pattern definitions intended to remain readable as standalone Markdown while also being suitable for later assembly into EPUB, PDF, web, or machine-readable publication workflows.

## Current Patterns

### Consumer / Platform Abuse

1. [Bait-and-Gate](bait-and-gate.md) — `consumer-pred-001`
2. [Security Authority Inversion](security-authority-inversion.md) — `consumer-pred-002`
3. [Threat Seeding](threat-seeding.md) — `consumer-pred-003`
4. [Protective Interception](protective-interception.md) — `consumer-pred-004`
5. [Entrenched Control](entrenched-control.md) — `consumer-pred-005`
6. [Distributed Flow-Limited Amplification](distributed-flow-limited-amplification.md) — `consumer-pred-006`
7. [Fake Seller Profile Pattern](fake-seller-profile.md) — `consumer-pred-007`
8. [Trusted Identity Injection](trusted-identity-injection.md) — `consumer-pred-008`

### Institutional / Governance

9. [Institutional Dependency Blind Spot](institutional-dependency-blind-spot.md) — `institutional-capture-001`

### Design / Transformation

10. [Renewable Design Pattern](renewable-design.md) — `design-renewal-001`

### Defensive Architecture

11. [Identity Authority State Separation](identity-authority-state-separation.md) — `defense-001`

Core invariant:

`Identity != Authority != State`

The defensive pattern interrupts Trusted Identity Injection by preventing authenticated identity from inheriting unconditional state-mutation authority.

## Supporting Models

- [Resolver-Scoped Authority](../models/resolver-scoped-authority.md) — `gr-ai-gamma:concept:resolver-scoped-authority`

Resolver-Scoped Authority develops the mechanism beneath `defense-001`:

`R(I, C, O, P, S, H) -> (D, A')`

where authority is an output of resolution rather than a property carried by identity, and:

`D in {Permit, Reject, Constrain, Challenge}`

## Threat / Defense Relationship

The registry now captures both the attack transport and its architectural inverse:

`Trusted Identity Injection -> Identity inherits mutation authority -> Authoritative state injection`

`Identity Authority State Separation -> Independent authority resolution -> Scoped state mutation`

The resolver model further sharpens the defensive side:

`Identity Claim + Context + Operation + Provenance + State + Transform History -> Resolution -> Scoped Authority`

Governing principle:

`Authority is not possessed. Authority is resolved.`

## Common Structure

Each threat pattern should contain, at minimum:

- publication metadata/front matter
- definition
- structural signature
- common indicators
- extraction or attack targets
- evidence threshold
- related patterns
- pattern composition notes
- case-reference hooks

Defensive patterns and supporting models may additionally define:

- invariants
- resolution rules
- state-transition constraints
- provenance requirements
- failure modes
- unresolved design constraints

## Supporting Layers

The registry separates four layers:

- `patterns/` — reusable threat, behavior, design, and defensive signatures
- `models/` — evidence, dependency, detection, resolution, and authority logic
- `cases/` — application of patterns to specific entities or incidents
- `evidence/` — provenance, timelines, relationship graphs, and source records

## Separation of Pattern and Case Evidence

Pattern files define reusable behavior signatures. Vendor-, product-, organization-, or incident-specific evidence should live in separate case records and link back to one or more canonical patterns.

This separation allows the registry to remain stable while individual cases move through potential, corroborated, resolved, retracted, or otherwise updated evidence states.

The registry also functions as a test bed: new models, defensive inverses, relationships, and experiments should accumulate context without rewriting earlier provenance merely to make the history appear cleaner.
