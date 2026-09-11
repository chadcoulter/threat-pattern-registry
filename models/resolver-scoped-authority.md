---
title: "Resolver-Scoped Authority"
id: "gr-ai-gamma:concept:resolver-scoped-authority"
type: "concept"
category: "Defensive Architecture"
family: "Trust and Authority Separation"
epistemic_status: "asserted"
state: "draft"
sensitivity: "open"
version: "0.1"
---

# Resolver-Scoped Authority

## Definition

Resolver-Scoped Authority is an authorization model in which authority is not an intrinsic property possessed by an identity, credential, role, application, agent, or service.

Authority is produced by resolving a specific proposed transformation against the identity presenting it, the current context, the requested operation, available provenance, authoritative state, and relevant transformation history.

`Authority is not possessed. Authority is resolved.`

An authenticated identity contributes evidence to an authorization decision but does not carry unconditional mutation authority.

This specializes the architectural invariant established by Identity Authority State Separation (`defense-001`):

`Identity != Authority != State`

## Core Resolution Model

Let:

- `I` = authenticated identity claim
- `C` = contextual state
- `O` = proposed operation
- `P` = provenance supporting the request
- `S` = current authoritative state
- `H` = relevant transformation history
- `D` = resolver decision
- `A'` = authority produced for the resolved transformation

Then:

`R(I, C, O, P, S, H) -> (D, A')`

where:

`D in {Permit, Reject, Constrain, Challenge}`

Authority `A'` is therefore an output of resolution, not an input inherited from identity.

## Core Transform

`Identity Claim + Context + Operation + Provenance + State + Relevant Transform History -> Resolve -> Decision + Scoped Authority`

Compact form:

`(I, C, O, P, S, H) -> Resolver -> (D, A')`

If the decision permits mutation:

`(S_t, A', O) -> Transform -> S_(t+1)`

with transition provenance preserved:

`S_t -> [I, O, P, C, H, A'] -> S_(t+1)`

## Authority Scope

Authority exists only within the resolution that produced it.

`A' = Authority(O, C, S, H)`

Therefore:

`A'(O_t) -/-> A'(O_(t+1))`

and:

`A'(S_t) -/-> A'(S_(t+1))`

A previous Permit decision is historical evidence, not automatic authorization for a future operation.

Likewise:

`Authenticated(I) -/-> A'`

`Possession(Credential) -/-> A'`

## Resolver Outcomes

### Permit

The requested transformation resolves within available authority.

`R(...) -> (Permit, A')`

`A'` authorizes the resolved operation only within its defined scope.

### Reject

The proposed transformation does not resolve as permissible.

`R(...) -> (Reject, null)`

No mutation authority is produced.

### Constrain

A subset or bounded form of the requested transformation resolves.

`O_allowed subset O_requested`

Therefore:

`R(...) -> (Constrain, A'_bounded)`

Authority exists only for the constrained transform.

### Challenge

Available information is insufficient to complete resolution.

`R(...) -> (Challenge, null)`

Challenge can acquire additional provenance, context, authentication, state reconciliation, user agency, or other resolution inputs before reevaluation.

`R_0 -> Challenge -> Input_additional -> R_1`

Challenge does not provisionally grant authority.

## Invariants

### 1. Identity Separation

`Identity != Authority`

Authentication establishes identity, not mutation authority.

### 2. State Separation

`Authority != State`

Possession of authority to perform one transformation does not establish the validity of proposed state.

### 3. Resolution-Bound Authority

`Authority exists only within the scope of its resolution.`

Authority does not automatically propagate between operations.

### 4. No Unconditional Mutation Authority

`Compromised Identity -/-> Unconditional Mutation Authority`

This remains true even for highly privileged identities.

### 5. Authentication Is an Input

`Authentication -> Resolver Input`

not:

`Authentication -> Authority`

### 6. Permission Is a Claim

Legacy permission and role systems are translated as resolver inputs:

`Permission_X -> Authority Claim -> Resolver`

not:

`Permission_X -> Automatic Authority`

### 7. Mutation Preserves Continuity

Every authoritative mutation retains its transformation history:

`Prior State + Actor + Transform + Time + Basis -> New State`

### 8. History Is Transform History, Not Reputation

`H = Relevant Transformation History`

not:

`H = TrustScore(Identity)`

Previous successful operations must not silently reconstruct permanent trusted-identity authority.

## Composition Rule

Individual operations cannot be evaluated entirely independently when their composition creates new capability.

Given:

`O_1, O_2, ..., O_n`

the resolver must be capable of evaluating:

`O_1 o O_2 o ... o O_n`

against relevant history `H`.

Therefore:

`Authority(O_n) = R(I, C, O_n, P, S, H_(0..n-1))`

This prevents a sequence of individually constrained operations from accumulating into authority that none of the individual resolutions granted.

## Resolver Authority Constraint

The resolver itself must not become a replacement trusted identity.

Invalid architecture:

`Request -> Trusted Resolver -> Decision`

Required architecture:

`Request + Rules + State + Context + Provenance + History -> Derived Resolution`

The resolver derives authority. It does not inherently possess the authority it resolves.

## Relationship to Identity Authority State Separation

Identity Authority State Separation (`defense-001`) establishes:

`Identity != Authority != State`

Resolver-Scoped Authority defines the mechanism by which authority exists after those domains are separated:

`I != A != S -> A = Output(Resolution)`

Relationship:

`gr-ai-gamma:concept:resolver-scoped-authority -> specializes -> defense-001`

It supports the defensive objective:

`Trusted Identity -/-> Inherited Mutation Authority`

## Relationship to Trusted Identity Injection

Trusted Identity Injection (`consumer-pred-008`) depends upon:

`Trusted Identity -> Inherited Authority -> Accepted Mutation`

Resolver-Scoped Authority interrupts the authority-inheritance edge:

`Trusted Identity -> Identity Evidence -> Independent Resolution`

Thus:

`Identity Compromise -> Identity Compromise`

rather than automatically:

`Identity Compromise -> Authority Compromise -> State Compromise`

## Open Design Constraints

1. Resolver authority: the resolver must not become a new root authority.
2. Challenge recursion: Challenge requires termination and resource-budget semantics.
3. Context provenance: context influencing authority must itself have attributable provenance.
4. Transform composition: individually permitted operations must not compose into ungranted authority.
5. History contamination: transformation history must not evolve into an implicit identity reputation system.
6. Concurrent resolution: authority semantics must remain coherent when multiple transforms operate against changing state simultaneously.

## Compact Definition

`R(I, C, O, P, S, H) -> (D, A')`

`A' is temporary, transform-specific, state-aware, context-aware, provenance-aware, and non-inheritable.`

Governing principle:

`Authority is not possessed. Authority is resolved.`

## Related Registry Entries

- Identity Authority State Separation (`defense-001`)
- Trusted Identity Injection (`consumer-pred-008`)
- Security Authority Inversion (`consumer-pred-002`)

## Provenance

Derived in the September 11, 2026 design conversation while developing the defensive inverse of Trusted Identity Injection and the resolver decision model for Identity Authority State Separation.
