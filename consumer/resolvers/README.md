# Resolver Boundary

Resolvers receive claims, evidence, context, and provenance from the facilitator and return a structured resolution result.

A resolver may be probabilistic, deterministic, formal, graph-based, statistical, or domain-specific.

## Resolver responsibilities

- declare its capability and supported claim classes
- accept the language-neutral interchange contract
- preserve provenance references
- return a resolution state and supporting derivation metadata
- surface contradiction, insufficiency, or logical failure explicitly
- avoid asserting authority beyond its declared capability

F# is a preferred candidate for formal or deterministic resolvers because strict types and explicit state transitions can make invalid resolution states harder to represent.

The framework must allow multiple resolvers to participate in the same case without requiring them to share an implementation language.
