# Research Consumer Framework

This root project defines the repository-level architecture for consuming external research, facilitating triadic transformations, and handing claims to one or more resolvers.

No implementation language is required by this structure. The intended initial role split is:

- **Source / analysis adapters:** commonly Python or other source-specific tooling
- **Facilitator:** Ruby / Rails
- **Formal resolver:** F# or another deterministic resolver

The architecture is organized around the triad:

`SOURCE -> FACILITATOR -> RESOLVER`

or, semantically:

`OBSERVE -> ORCHESTRATE -> RESOLVE`

The facilitator owns routing, provenance continuity, state transition coordination, resolver selection, event history, and composition of results. It does not need to perform every analysis or resolution itself.

## Root Structure

- `contracts/` - language-neutral interchange contracts and state boundaries
- `facilitator/` - Ruby/Rails facilitator responsibilities and orchestration model
- `adapters/` - external source and ingestion boundaries
- `resolvers/` - resolver capability and handoff boundaries
- `provenance/` - provenance propagation and event-history requirements

PLOT4AI is the first external research source, represented separately under `/plot4ai`.
