---
title: "Security Authority Inversion"
id: "consumer-pred-002"
category: "Consumer Predation"
family: "Authority Inversion"
status: "provisional"
version: "0.1"
---

# Security Authority Inversion

## Definition

A predation pattern in which an entity gains trust, privileged access, or technical control because it is expected to mitigate threats, then uses that privileged position in a way that itself becomes coercive, obstructive, extractive, or harmful.

## Structural Signature

`Trusted Protective Role -> Privileged Access -> Control Expansion -> User Harm -> Monetization`

## Common Indicators

- protection software receives unusually broad system or network privileges
- user consent is treated as expandable rather than bounded
- protective controls interfere with normal user choices
- the provider's intervention creates commercial leverage
- security authority is used to justify behavior unrelated to immediate threat mitigation
- the user cannot easily distinguish protection from product control

## Extraction Targets

- continued subscription
- upsell revenue
- telemetry and behavioral data
- ecosystem lock-in
- control over browsing or application choices

## Evidence Threshold

A strong match requires evidence that privileges granted for protection were used to create or enforce a condition that benefited the protector at the user's expense.

## Related Patterns

- Threat Seeding
- Protective Interception
- Entrenched Control
- Dependency Reinforcement

## Pattern Composition

Security Authority Inversion is often a parent pattern. More specific behaviors such as Threat Seeding or Protective Interception can occur underneath it.

## Case References

Document vendor-specific cases separately and link them here only after the relevant observable event chain has been preserved.
