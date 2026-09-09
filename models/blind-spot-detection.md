# Blind-Spot Detection Algorithm

This model provides a repeatable process for identifying a possible Institutional Dependency Blind Spot without conflating correlation with capture.

## Inputs

For each monitored entity `E`, gather:

- historical scrutiny intensity
- current scrutiny intensity
- peer/control-group scrutiny
- issue relevance over time
- known conduct by `E`
- dependency vectors connecting the watchdog to `E`
- evidence of organizational knowledge
- evidence of behavioral or editorial influence

## Detection Flow

```text
for each monitored entity E:

    measure historical_scrutiny(E)
    identify dependencies(E)
    measure post_dependency_scrutiny(E)

    compare against:
        peer_scrutiny
        issue_continuity
        known_conduct
        stated_organizational_doctrine

    if scrutiny declines selectively:
        state = ANOMALOUS

    if dependency exists
       and selective decline follows dependency formation
       and issue relevance remains material:
        state = POTENTIAL_BLIND_SPOT

    if comparable actors receive stronger scrutiny
       or documented knowledge exists without comparable action:
        state = CORROBORATED_BLIND_SPOT

    if avoidance follows the dependency boundary:
        state = STRONGLY_CORROBORATED

    if evidence shows dependency affected a decision:
        state = DEPENDENCY_INDUCED_DISTORTION

    if explicit exchange, condition, control, or suppression exists:
        state = CAPTURED
```

## Counterfactual Test

The strongest reusable discriminator between reprioritization and a dependency blind spot is:

> Does the organization continue applying the same principle to comparable actors while failing to apply it to an actor on whom it has developed a meaningful dependency?

Represented as:

```text
Conduct(A) ~= Conduct(B) ~= Conduct(C)
Response(A) ~= Response(B) >> Response(C)
Dependency(C) > Dependency(A,B)
```

## Knowledge Test

A case strengthens materially when there is evidence that the watchdog:

1. knew of the conduct,
2. understood its significance,
3. retained the analytical framework needed to criticize it, and
4. did not apply that framework comparably to the dependency partner.

## Output

Each run should produce:

- evidence state
- supporting observations
- unresolved alternatives
- missing evidence needed for next-state transition
- provenance links

## Guardrail

The algorithm classifies structural evidence. It must not infer motive, corruption, conspiracy, or explicit capture without evidence supporting those higher-order claims.
