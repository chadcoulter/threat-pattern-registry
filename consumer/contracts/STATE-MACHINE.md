# Claim State Machine

Version: 0.1

This document defines the shared epistemic and authority states used across SOURCE -> FACILITATOR -> RESOLVER.

## States

- `potential` - observed or proposed, but not sufficiently supported.
- `corroborated` - supported by independent or otherwise sufficient evidence, but not yet fully resolved.
- `resolved` - adjudicated by an accepted resolver under the applicable resolution rules.
- `authorized` - resolved and additionally granted authority by an actor or policy allowed to confer authority.
- `contradicted` - material evidence conflicts with the claim or prior resolution.
- `retracted` - the originating or responsible actor withdraws the claim or result.
- `revoked` - previously granted authority is explicitly withdrawn.

## Core rule

Resolution and authority are separate dimensions represented here as ordered states for interchange simplicity.

`resolved` MUST NOT automatically become `authorized`.

A resolver may propose a transition to `resolved`. Authorization requires an explicit authority basis and an actor permitted by policy to authorize.

## Normal progression

```text
potential -> corroborated -> resolved -> authorized
```

Any stage may receive contradictory evidence.

## Allowed transition families

### From `potential`

- `potential -> corroborated` when the evidence threshold is met.
- `potential -> contradicted` when material contrary evidence is established.
- `potential -> retracted` when the claim is withdrawn.

### From `corroborated`

- `corroborated -> resolved` when an accepted resolver completes adjudication.
- `corroborated -> potential` when supporting evidence is weakened, removed, or invalidated below the corroboration threshold.
- `corroborated -> contradicted` when material contrary evidence requires re-resolution.
- `corroborated -> retracted` when the claim is withdrawn.

### From `resolved`

- `resolved -> authorized` only with explicit authority basis.
- `resolved -> corroborated` when a contradiction weakens certainty but substantial support remains.
- `resolved -> potential` when the basis for resolution collapses.
- `resolved -> contradicted` when material conflict requires re-resolution.
- `resolved -> retracted` when the responsible originator or resolver withdraws the result.

### From `authorized`

- `authorized -> revoked` when authority is withdrawn.
- `authorized -> contradicted` when material evidence challenges the authorized claim and policy requires re-resolution.
- `authorized -> resolved` when authority is removed without invalidating the underlying resolution.
- `authorized -> retracted` when the responsible actor withdraws the underlying claim/result.

### From `contradicted`

A contradicted claim MUST be re-evaluated rather than silently restored.

Possible outcomes are:

- `contradicted -> potential`
- `contradicted -> corroborated`
- `contradicted -> resolved`
- `contradicted -> retracted`

The selected state depends on the surviving evidence after re-resolution.

### From `retracted`

Retraction is not deletion. Provenance and prior state remain preserved.

A retracted claim may only return to an active state through an explicit new transition with a reason and evidence basis:

- `retracted -> potential`
- `retracted -> corroborated`

Direct restoration to `resolved` or `authorized` SHOULD be rejected unless policy explicitly permits it and the transition carries a complete authority basis.

### From `revoked`

Revocation removes authority, not necessarily truth value.

Possible transitions are:

- `revoked -> resolved` when the underlying resolution remains valid but authority stays absent.
- `revoked -> contradicted` when the underlying resolution itself is challenged.
- `revoked -> authorized` only through a new explicit authorization event with a new authority basis.

## Transition invariants

Every transition MUST include:

- transition identity
- subject identity
- prior state
- proposed/new state
- reason
- actor identity and role
- timestamp
- supporting evidence references where applicable
- authority basis where applicable

Transitions MUST be appended to provenance lineage. They MUST NOT overwrite prior states as though those states never existed.

## Facilitator responsibility

The facilitator:

- routes claims and evidence;
- records proposed and accepted transitions;
- validates that transition shape is permitted;
- preserves causation and provenance;
- MUST NOT manufacture evidentiary authority merely because a resolver returned a result.

## Resolver responsibility

A resolver:

- evaluates the inputs it was given;
- returns a decision, basis, contradictions, unresolved questions, and proposed transition;
- MUST identify what evidence supports its output;
- MUST NOT silently authorize its own resolution unless it is separately designated as an authorized governor.

## Source responsibility

A source:

- emits observations and artifacts;
- identifies provenance and source state;
- may propose potential claims;
- MUST NOT elevate a claim merely by repeating it.

## Re-resolution rule

When a resolved or authorized claim becomes contradicted, the next resolver evaluates the surviving evidence without assuming the previous resolution is still valid.

The result is:

- `resolved` if the contradiction is overcome and the full resolution threshold still holds;
- `corroborated` if substantial support remains but the resolution threshold no longer holds;
- `potential` if support falls below corroboration threshold;
- `retracted` if the responsible actor withdraws the claim/result.

Authority, if previously present, must be separately re-established after re-resolution.
