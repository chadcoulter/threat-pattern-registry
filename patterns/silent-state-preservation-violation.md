# Silent State Preservation Violation

## Definition

A Silent State Preservation Violation occurs when a collaborator explicitly asks that an existing artifact or state remain unchanged, but an intermediary modifies that state anyway while presenting the result as a continuation of the same artifact.

## Structural Signature

```text
state explicitly frozen
-> new work requested from that state
-> intermediary edits the frozen state instead of generating a new state
-> original snapshot is silently replaced
-> collaborator loses the preserved reference point
```

## Core Distinctions

```text
regenerate from state != modify preserved state

new version != mutation of frozen version
```

## Threat Condition

The threat exists when preservation has been explicitly requested and the intermediary performs an in-place transformation without explicit authorization to alter the preserved state.

## Core Effect

```text
Explicit Preservation Request
-> Silent In-Place Mutation
-> Snapshot Loss
-> State Integrity Failure
```

## Failure Mode

The intermediary may preserve the visible intent of the work while violating the state boundary itself. This is especially dangerous in iterative collaborative systems because later work can appear to descend from a preserved artifact even though that artifact has already been silently changed.

## Defensive Rule

```text
preserved state = immutable snapshot
requested change = regenerate new state
```

Never alter the preserved artifact unless the collaborator explicitly authorizes mutation of that artifact.
