---
title: "Entrenched Control"
id: "consumer-pred-005"
category: "Consumer Predation"
family: "Persistence and Lock-In"
status: "provisional"
version: "0.1"
---

# Entrenched Control

## Definition

A predation pattern in which software, a service, or a control mechanism becomes embedded deeply enough in a user's environment that practical removal, disablement, or escape is obstructed, allowing the controlling party to preserve influence beyond the user's continuing consent.

## Structural Signature

`Privileged Installation -> Persistence -> Removal Resistance -> Continued Control -> Extraction`

## Common Indicators

- multiple persistence mechanisms or reinstall behaviors
- removal requires unusual technical effort relative to installation
- disabling one component leaves other controlling components active
- product functionality is tied to core browsing, networking, identity, or system behavior
- the user's attempt to revoke consent does not fully terminate the control path
- lock-in creates continued commercial or telemetry value

## Extraction Targets

- continued subscription
- ecosystem lock-in
- telemetry continuity
- privileged access
- forced dependency on the installed control layer

## Evidence Threshold

A strong match requires reproducible evidence that the user's attempt to remove or revoke the control mechanism does not fully terminate its functional influence, and that persistence materially benefits the controlling party.

## Related Patterns

- Security Authority Inversion
- Threat Seeding
- Protective Interception
- Dependency Reinforcement

## Pattern Composition

Entrenched Control commonly appears as the persistence layer in compound predation chains. It can turn a temporary intervention into an ongoing control relationship.

## Case References

Store uninstall traces, service inventories, scheduled tasks, browser-extension state, reinstallation events, registry or configuration artifacts, and post-removal behavior in separate case records.
