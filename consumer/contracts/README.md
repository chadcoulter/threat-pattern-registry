# Interchange Contracts

This folder defines language-neutral contracts between sources, the facilitator, and resolvers.

The contracts should eventually specify:

- source identity
- source version
- artifact identity
- claim identity
- evidence identity
- transform identity
- resolver identity
- input state
- output state
- provenance envelope
- confidence / evidence state
- contradiction markers
- authorization state
- timestamps and checksums

The contract layer exists so Python adapters, Ruby/Rails orchestration, F# resolvers, and future components can evolve independently without breaking the research exchange model.

No executable implementation belongs here until the interchange model itself is stable.
