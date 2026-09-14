# Resolver-Scoped Authority Formal Schema

Canonical concept: `gr-ai-gamma:concept:resolver-scoped-authority`

Core resolution:

`R(I, C, O, P, S, H) -> (D, A')`

## Fields

### Identity (`I`)

Authenticated identity claim presented to the resolver.

`Identity != Authority`

Authentication establishes identity, not mutation authority.

### Context (`C`)

Contextual state in which the proposed operation is being resolved.

Context participates in authority resolution and therefore requires attributable provenance when it influences the decision.

### Operation (`O`)

The specific proposed transformation or operation for which authority is being resolved.

Authority attaches to the resolved operation rather than permanently to the identity.

### Provenance (`P`)

Provenance supporting the request, proposed state, context, and transformation basis.

### State (`S`)

Current authoritative state against which the proposed operation is resolved.

`Authority != State`

Authority to perform a transformation does not independently establish the validity of proposed state.

### History (`H`)

Relevant transformation history used to resolve accumulated or composed capability.

`H = Relevant Transformation History`

`H != TrustScore(Identity)`

Previous successful operations do not create permanent trusted-identity authority.

### Decision (`D`)

Resolver outcome.

`D in {Permit, Reject, Constrain, Challenge}`

- `Permit` - the requested transformation receives scoped authority.
- `Reject` - no mutation authority is produced.
- `Constrain` - a bounded subset of the requested transformation receives authority.
- `Challenge` - authority remains unresolved pending additional resolution input; no provisional authority is produced.

### Scoped Authority (`A'`)

Authority produced by resolution for the specific resolved transformation.

`A' = Authority(O, C, S, H)`

Authority is an output of resolution, not an input inherited from identity.

`Authenticated(I) -/-> A'`

`Possession(Credential) -/-> A'`

`A'(O_t) -/-> A'(O_(t+1))`

`A'(S_t) -/-> A'(S_(t+1))`

## Composition Constraints

Individual operations cannot be evaluated entirely independently when their composition creates new capability.

Given:

`O_1, O_2, ..., O_n`

the resolver evaluates the current operation against relevant transformation history:

`Authority(O_n) = R(I, C, O_n, P, S, H_(0..n-1))`

The composed sequence:

`O_1 o O_2 o ... o O_n`

must not accumulate authority beyond the authority produced for the resolved transforms.

A sequence of individually constrained operations therefore does not automatically compose into ungranted authority.

## Resolution Record

```text
ResolverScopedAuthority {
    identity: I
    context: C
    operation: O
    provenance: P
    state: S
    history: H
    decision: D
    scoped_authority: A'
    composition_constraints: {
        relevant_history: H_(0..n-1)
        composed_operations: [O_1 .. O_n]
        authority_must_not_exceed_resolved_scope: true
    }
}
```

## Governing Invariants

`Identity != Authority != State`

`Authentication -> Resolver Input`

`Permission_X -> Authority Claim -> Resolver`

`Compromised Identity -/-> Unconditional Mutation Authority`

`Prior State + Actor + Transform + Time + Basis -> New State`

`Authority exists only within the scope of its resolution.`

## Relationship

`gr-ai-gamma:concept:resolver-scoped-authority -> specializes -> defense-001`

Governing principle:

`Authority is not possessed. Authority is resolved.`

---

## Expanded Resolution Semantics

The schema separates the information presented to a resolver from the authority produced by that resolver. A request can therefore carry identity, credentials, permissions, claims, proposed state, and supporting provenance without any of those fields independently constituting authority.

The resolution boundary is:

`Request(I, C, O, P, S, H) -> Resolve -> (D, A')`

The resolver evaluates the relationship among the fields rather than promoting one field into a universal trust source.

This preserves the separation:

`Identity != Authority != State`

across the complete request lifecycle.

## Identity Semantics

`I` identifies the actor or source participating in the proposed transformation.

Identity can contribute to resolution without containing authority:

`I -> Resolution Input`

A valid identity can therefore participate in a rejected, constrained, or challenged operation without changing the validity of the identity itself.

`Reject(Operation) != Reject(Identity)`

Likewise, successful authentication does not collapse the remaining resolution dimensions:

`Authenticated(I) -> Resolve(C, O, P, S, H)`

## Context Semantics

`C` describes the conditions under which the requested transform is being evaluated.

Because context can change the resolution of the same identity and operation, authority remains context-bound:

`A'(O, C_1) != A'(O, C_2)`

when the relevant contexts resolve differently.

Context that contributes to an authoritative decision participates in the same provenance discipline as other resolution inputs.

## Operation Semantics

`O` is the proposed transform, not merely the name of a permission or capability.

The resolver therefore evaluates the actual requested state transition:

`S_t --O--> S_(t+1)`

rather than resolving a permanent class of authority for the actor.

A Permit decision applies to the resolved transform:

`Permit(I, O_t) -/-> Permit(I, O_(t+1))`

## Provenance Semantics

`P` records the basis upon which resolution inputs and resulting transforms can be traced.

For an authoritative mutation, provenance preserves the continuity path:

`S_t --[I, O, P, C, H, A']--> S_(t+1)`

This allows the resulting state to retain the basis of the transformation that produced it.

## State Semantics

`S` is both a resolution input and the state against which the proposed transformation is evaluated.

The same operation can therefore resolve differently as authoritative state changes:

`R(I, C, O, P, S_t, H) != R(I, C, O, P, S_(t+1), H)`

A prior authorization does not become authority over a later state merely because the identity and operation remain unchanged.

## History Semantics

`H` carries the relevant transform path into the current resolution.

Its purpose is composition awareness:

`H_(0..n-1) + O_n -> Resolve`

This allows the resolver to recognize that a sequence of individually bounded transforms can produce a combined capability greater than any individual operation.

History remains transform-centered:

`H = {T_0, T_1, ..., T_(n-1)}`

and does not become:

`H = Reputation(I)`

The distinction prevents accumulated successful resolutions from silently recreating permanent identity authority.

## Decision Semantics

The four decision states preserve different resolution outcomes without collapsing unresolved requests into binary authorization.

### Permit

`R(...) -> (Permit, A')`

The proposed transform resolves and receives authority bounded to that resolution.

### Reject

`R(...) -> (Reject, null)`

The proposed transform does not resolve. Authoritative state remains unchanged.

`S_(t+1) = S_t`

### Constrain

`R(...) -> (Constrain, A'_bounded)`

The requested operation is reduced to the portion that resolves:

`O_allowed subset O_requested`

The resulting authority is bounded to `O_allowed`.

### Challenge

`R(...) -> (Challenge, null)`

The current inputs do not produce sufficient resolution. Additional resolution input can be introduced and the resolver run again:

`R_0 -> Challenge -> Input_additional -> R_1`

Until a later resolution produces scoped authority, no mutation authority exists for the challenged transform.

## Scoped Authority Lifecycle

Scoped authority is created by resolution, used by the resolved transform, and does not automatically survive that transform.

`Resolution -> A'_t -> Transform_t -> State_(t+1)`

The next proposed transform returns to resolution:

`State_(t+1) + Request_(t+1) -> Resolver -> A'_(t+1)`

This produces a repeating authority lifecycle:

`Request -> Resolve -> Scoped Authority -> Transform -> State -> Request`

rather than an accumulating authority lifecycle:

`Identity -> Permission -> Permanent Authority`

## Composition Semantics

Composition constraints operate over the relationship between current operation and relevant transform history.

For a sequence:

`T_1, T_2, ..., T_n`

each new resolution can include the relevant preceding transforms:

`R_n = R(I, C, O_n, P, S_n, H_(0..n-1))`

The composition constraint is:

`Authority(T_1 o T_2 o ... o T_n) <= ResolvedScope(T_1 ... T_n)`

A chain of individually permitted or constrained operations cannot use composition alone to manufacture additional authority.

## Resolver Output Record

A completed resolution can be represented as:

```text
ResolverDecision {
    inputs: {
        identity: I
        context: C
        operation: O
        provenance: P
        state: S
        history: H
    }
    output: {
        decision: Permit | Reject | Constrain | Challenge
        scoped_authority: A' | null
    }
    composition: {
        relevant_history: H_(0..n-1)
        requested_operation: O_requested
        resolved_operation: O_allowed | O_requested | null
    }
}
```

## Defensive Transform

Trusted Identity Injection follows the authority-inheritance path:

`Trusted Identity -> Authority Inheritance -> Injected State -> Accepted Mutation`

Resolver-Scoped Authority changes that path to:

`Authenticated Identity -> Resolution Input -> Independent Authority Resolution -> Scoped Transform`

The interrupted edge is:

`Identity -/-> Inherited Mutation Authority`

This connects the schema directly to Identity Authority State Separation (`defense-001`) while preserving Trusted Identity Injection (`consumer-pred-008`) as the threat pattern whose authority-transfer mechanism is being interrupted.

## Expanded Composition Constraints

The composition model preserves these constraints across successive resolutions:

1. A prior Permit is history, not current authority.
2. A prior Constrain does not enlarge the next operation's scope.
3. A Challenge produces no provisional mutation authority.
4. A Reject does not invalidate identity; it rejects the proposed transform.
5. Successful transforms enter history as transforms, not identity reputation.
6. State changes require authority to be resolved against the resulting state again.
7. Composed operations cannot acquire authority solely because each component operation resolved independently.

## Expanded Invariant Set

`Identity != Authority != State`

`Authenticated(I) -/-> Authorized(O)`

`Authorized(O) -/-> Valid(State)`

`Previous Permit -/-> Current Authority`

`History != Identity Reputation`

`Challenge -> No Mutation Authority`

`Reject(Operation) != Reject(Identity)`

`Constrain(O) -> Authority(O_allowed)`

`State Mutation -> Preserved Transformation Provenance`

`Composed Capability <= Resolved Composition Scope`

`Compromised Identity -/-> Unconditional Mutation Authority`

The governing principle remains:

`Authority is not possessed. Authority is resolved.`
