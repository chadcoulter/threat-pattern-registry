# Interchange Contracts

Version: 0.1

This folder defines the language-neutral protocol between SOURCE, FACILITATOR, and RESOLVER components.

```text
SOURCE -> FACILITATOR -> RESOLVER
OBSERVE -> ORCHESTRATE -> RESOLVE
```

The contract layer allows Python adapters, Ruby/Rails facilitation, F# resolvers, and future components to evolve independently without changing the research exchange semantics.

## Contract files

### `envelope.schema.json`

Common message wrapper. Carries contract version, message identity, correlation/causation identifiers, producer identity, payload, provenance, timestamp, and optional integrity digest.

### `source-payload.schema.json`

Defines what a SOURCE may emit after observation or retrieval. Carries artifact identity, source state, content, observations, warnings, and any claims proposed from the artifact.

A source may create a `potential` claim. Repetition by a source does not by itself elevate claim authority.

### `facilitator-dispatch.schema.json`

Defines how the FACILITATOR routes work. Carries subject, current state, intent, target role/resolver, required capabilities, selected transform, referenced inputs, constraints, and expected output.

The facilitator orchestrates and records. It does not manufacture evidentiary authority.

### `resolver-request.schema.json`

Defines the language-neutral request made to a RESOLVER. Carries the claim, evidence references, current state, prior resolutions, pattern references, constraints, and required result fields.

### `resolver-result.schema.json`

Defines what a RESOLVER must return. A result includes decision, output state, confidence where applicable, evidence basis, contradictions, unresolved questions, and an explicit proposed state transition.

A resolver proposes epistemic state changes. Authorization remains a separate governance act unless the resolver is separately designated as an authorized governor.

### `provenance.schema.json`

Defines the provenance envelope that accompanies every stage. It preserves original source identity, source reference/version/URL, observation and retrieval timestamps, license, digest, citations, and append-only lineage steps.

Provenance is part of the payload contract, not optional descriptive metadata.

### `state-transition.schema.json`

Defines a single proposed or accepted claim-state transition. Every transition carries prior state, next state, reason, actor, evidence references, authority basis when applicable, timestamp, and transition status.

### `STATE-MACHINE.md`

Defines state semantics and allowed transition families for:

- `potential`
- `corroborated`
- `resolved`
- `authorized`
- `contradicted`
- `retracted`
- `revoked`

It also defines re-resolution behavior and the separation between resolution and authorization.

## Required invariants

1. **Provenance survives every hop.** A transform may append lineage but must not erase origin.
2. **Correlation and causation remain traceable.** Every derived message should be traceable to the message or artifact that caused it.
3. **Claims have explicit state.** State must never be inferred solely from wording or confidence score.
4. **Confidence and authority are different.** A high-confidence result is not automatically authorized.
5. **Resolution and authorization are different.** `resolved -> authorized` requires an explicit authority basis.
6. **Contradiction does not delete history.** It triggers re-resolution while preserving prior states and evidence.
7. **Retraction does not erase provenance.** A retracted claim remains historically traceable.
8. **Revocation removes authority, not automatically truth.** The underlying resolved state may survive a revocation.
9. **Resolvers expose basis.** A resolver result without evidence references or an explicit basis is incomplete.
10. **The facilitator records; it does not silently promote.** State transitions must be explicit protocol objects.

## Wire representation

JSON is the initial canonical interchange representation because it is implementation-neutral and maps cleanly into Ruby, Python, F#, JavaScript, Go, .NET, and other environments.

The semantics in these contracts are normative. Implementations may internally use richer native types, databases, events, or message formats, but crossing a triadic boundary must preserve an equivalent representation.

## Versioning

Contract version `0.1` is intentionally provisional.

Breaking semantic changes require a new contract version. Additive optional fields may be introduced without changing the major semantic version when existing consumers remain valid.

No executable application implementation belongs in this folder. This directory defines the protocol that implementations must honor.
