---
title: "Protective Interception"
id: "consumer-pred-004"
category: "Consumer Predation"
family: "Interception and Coercive Control"
status: "provisional"
version: "0.1"
---

# Protective Interception

## Definition

A predation pattern in which a product or service positioned as protective inserts itself into a user's traffic, workflow, or access path, then blocks, alters, or redirects the user's intended action in a way that creates commercial leverage or dependency.

## Structural Signature

`Protective Authority -> Interception -> Access Restriction -> Redirect / Upsell -> Extraction`

## Common Indicators

- browsing, application, or network traffic is intercepted by a protective component
- benign or user-selected destinations become blocked or altered
- the user is redirected toward a remediation, upgrade, or commercial offer
- the protective layer becomes necessary to restore normal access
- the intervention is broader than the stated threat being mitigated
- disabling the feature is difficult, obscure, or incomplete

## Extraction Targets

- upgrade revenue
- subscription conversion
- continued privileged access
- behavioral telemetry
- product lock-in

## Evidence Threshold

A strong match requires reproducible evidence that the protective layer altered the user's intended path and that the altered path created measurable commercial or control value for the provider.

## Related Patterns

- Security Authority Inversion
- Threat Seeding
- Entrenched Control
- Bait-and-Gate

## Pattern Composition

Protective Interception frequently compounds with Authority Inversion and Entrenched Control.

## Case References

Store screenshots, redirect URLs, browser or DNS logs, component identities, timestamps, and user-consent state in separate case records.
