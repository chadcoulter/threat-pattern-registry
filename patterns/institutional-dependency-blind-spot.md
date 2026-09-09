---
id: institutional-capture-001
title: "Institutional Dependency Blind Spot"
status: "provisional"
class: "institutional-capture"
subtype: "complementary-advocacy-capture"
version: "0.1"
---

# Institutional Dependency Blind Spot

## Definition

An Institutional Dependency Blind Spot occurs when a watchdog, standards body, nonprofit, auditor, regulator, advocacy organization, or similar institution develops a meaningful dependency or strategic alignment with an entity it is expected to scrutinize, and scrutiny subsequently becomes selectively weaker at the boundary of that relationship.

The pattern does not require bribery, conspiracy, explicit censorship, or conscious intent. It is a structural vulnerability in which ordinary institutional incentives can produce asymmetric scrutiny.

## Structural Signature

```text
historically meaningful scrutiny
        |
        v
relationship or dependency forms
        |
        v
scrutiny continues in aligned domains
        |
        v
scrutiny weakens in relationship-conflicting domains
        |
        v
relationship-boundary blind spot
```

A compact form is:

```text
A monitors B
C threatens or concerns both A and B
A and B cooperate against C
cooperation/dependency increases
A continues monitoring B
but disproportionately where A and B remain aligned
```

## Preconditions

- Entity A has a recognized scrutiny, advocacy, governance, audit, standards, regulatory, or watchdog role.
- Entity B is within the practical scope of A's scrutiny.
- A meaningful dependency, alliance, collaboration, or reciprocal relationship develops between A and B.
- The underlying issue remains relevant after the relationship forms.

## Dependency Vectors

Common vectors include:

- financial
- infrastructure
- legal/litigation
- policy collaboration
- personnel
- information access
- reputational reciprocity
- coalition membership
- platform dependency
- privileged access

See `../models/dependency-vectors.md`.

## Common Indicators

- strong historical scrutiny followed by selective decline
- continued criticism of peer organizations for materially comparable behavior
- continued advocacy on the general principle while the dependency partner receives less direct scrutiny
- documented knowledge of the dependency partner's conduct without a comparable public response
- criticism that persists in aligned domains but disappears where it would create friction with the relationship
- increasing operational or strategic switching costs tied to the scrutinized entity
- favorable ratings, endorsements, coalition work, or litigation alignment that become mutually reputational

## Evidence Thresholds

The pattern should not be inferred from silence alone.

| Threshold | Evidence | Classification |
|---|---|---|
| T0 | reduced scrutiny only | ordinary reprioritization |
| T1 | selective reduction versus peers | anomalous |
| T2 | dependency plus temporal correlation | potential blind spot |
| T3 | counterfactual asymmetry | corroborated blind spot |
| T4 | demonstrated knowledge without comparable action | corroborated blind spot |
| T5 | avoidance maps specifically to relationship boundary | strongly corroborated |
| T6 | evidence dependency affected decisions | dependency-induced distortion |
| T7 | explicit condition, control, quid pro quo, or suppression | captured |

## State Transition Rule

```text
silence alone != blind spot

silence + asymmetry = anomaly

asymmetry + dependency = potential blind spot

dependency + knowledge + differential treatment = corroborated blind spot

corroborated blind spot + causal influence = dependency-induced distortion

causal influence + explicit exchange/control = capture
```

## False-Positive Controls

Before elevating beyond ordinary reprioritization, test for:

- staff turnover
- explicit strategic changes applied across all comparable actors
- reduced organizational resources
- declining relevance of the underlying issue
- equivalent reduction in scrutiny across peer organizations
- transfer of advocacy work to another team or coalition
- lack of actual knowledge of the conduct

## Extraction Targets

For each candidate case, capture:

- scrutiny timeline
- relationship/dependency start dates
- dependency type and strength
- peer/control-group treatment
- evidence the organization knew of the underlying conduct
- public and internal statements where available
- decision or publication changes
- infrastructure/vendor relationships
- funding or donation pathways
- coalition and litigation history

## Related Patterns

- `consumer-pred-006` Distributed Flow-Limited Amplification
- regulatory capture
- advocacy capture
- conflict-of-interest drift
- mission-boundary erosion

## Pattern Composition Notes

This pattern may compose with other patterns where a dependency blind spot allows another exploit, abuse pattern, or policy change to persist longer than it otherwise would.

The blind spot is the enabling institutional condition, not necessarily the primary exploit.

## Case Hooks

- `../cases/eff-microsoft-institutional-dependency.md`
- `../cases/eff-microsoft-comparative-scrutiny.md`
