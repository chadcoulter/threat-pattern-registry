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
