---
title: "Threat Pattern Registry"
status: "provisional"
version: "0.3"
---

# Threat Pattern Registry

This directory contains canonical threat-pattern definitions intended to remain readable as standalone Markdown while also being suitable for later assembly into EPUB, PDF, web, or machine-readable publication workflows.

## Current Patterns

### Consumer / Platform Abuse

1. [Bait-and-Gate](bait-and-gate.md) — `consumer-pred-001`
2. [Security Authority Inversion](security-authority-inversion.md) — `consumer-pred-002`
3. [Threat Seeding](threat-seeding.md) — `consumer-pred-003`
4. [Protective Interception](protective-interception.md) — `consumer-pred-004`
5. [Entrenched Control](entrenched-control.md) — `consumer-pred-005`
6. [Distributed Flow-Limited Amplification](distributed-flow-limited-amplification.md) — `consumer-pred-006`
7. [Fake Seller Profile Pattern](fake-seller-profile.md) — `consumer-pred-007`

### Institutional / Governance

8. [Institutional Dependency Blind Spot](institutional-dependency-blind-spot.md) — `institutional-capture-001`

### Design / Transformation

9. [Renewable Design Pattern](renewable-design.md) — `design-renewal-001`

## Common Structure

Each pattern should contain, at minimum:

- publication metadata/front matter
- definition
- structural signature
- common indicators
- extraction targets
- evidence threshold
- related patterns
- pattern composition notes
- case-reference hooks

## Supporting Layers

The registry now separates four layers:

- `patterns/` — reusable behavior signatures
- `models/` — evidence, dependency, and detection logic
- `cases/` — application of patterns to specific entities or incidents
- `evidence/` — provenance, timelines, relationship graphs, and source records

## Separation of Pattern and Case Evidence

Pattern files define reusable behavior signatures. Vendor-, product-, organization-, or incident-specific evidence should live in separate case records and link back to one or more canonical patterns.

This separation allows the registry to remain stable while individual cases move through potential, corroborated, resolved, retracted, or otherwise updated evidence states.
