# Facilitator Boundary

The facilitator is the middle component of the triadic research-resolution model.

Its role is not to be the authoritative solver. Its role is to coordinate the system.

## Responsibilities

The facilitator should eventually own:

- source registration and source selection
- transform selection
- resolver capability discovery and resolver selection
- provenance propagation across every handoff
- claim-state coordination
- contradiction and retry routing
- event/history persistence
- composition of multiple resolver outputs
- governance and authorization hooks
- outward API/workflow exposure

## Intended Framework

Ruby / Rails is the preferred facilitator framework because it can provide domain-oriented orchestration, persistence, jobs, APIs, events, and a readable DSL without forcing source adapters or deterministic resolvers into the same language.

## Non-Responsibilities

The facilitator should not assume that:

- ingestion must be written in Ruby
- every transform must execute locally
- probabilistic analysis and deterministic resolution are the same operation
- a resolver result is authoritative merely because it completed

The facilitator coordinates authority; it does not manufacture authority.

## Triadic Role

`SOURCE -> FACILITATOR -> RESOLVER`

The facilitator carries context and provenance from observation into resolution and carries the resulting state back into the research graph.
