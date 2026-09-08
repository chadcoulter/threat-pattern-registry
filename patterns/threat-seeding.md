---
title: "Threat Seeding"
id: "consumer-pred-003"
category: "Consumer Predation"
family: "Threat Creation and Dependency"
status: "provisional"
version: "0.1"
---

# Threat Seeding

## Definition

A predation pattern in which a trusted product, service, or authority introduces, facilitates, stages, or materially contributes to a condition that it can later detect, classify, remediate, or monetize.

## Structural Signature

`Trusted Access -> Introduced Condition -> Detection / Alarm -> Remediation Authority -> Extraction`

## Common Indicators

- a new risk condition appears only after installation or intervention by the trusted product
- the same product subsequently claims authority to detect or resolve the condition
- user refusal or limited consent is followed by additional components or capabilities
- remediation requires continued use, subscription, upgrade, or further access
- the sequence is reproducible across controlled observations

## Extraction Targets

- subscription revenue
- upgrade revenue
- telemetry
- continued privileged access
- user dependency

## Evidence Threshold

A strong match requires an observable causal chain between the trusted product's action and the later threat condition. Mere coexistence, misclassification, or aggressive alerting is insufficient.

## Related Patterns

- Security Authority Inversion
- Protective Interception
- Entrenched Control
- Threat Amplification

## Pattern Composition

Threat Seeding may be followed by Protective Interception or Dependency Reinforcement, producing a compound predation loop.

## Case References

Store process trees, hashes, timestamps, network events, consent state, and remediation behavior in separate case records.
