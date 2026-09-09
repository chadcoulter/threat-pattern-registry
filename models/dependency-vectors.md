# Dependency Vector Taxonomy

Dependency vectors describe how an institution may become structurally reliant on, aligned with, or reciprocally connected to an entity it is expected to scrutinize.

## Vector Types

- `FINANCIAL` - direct funding, grants, sponsorship, donor-directed giving, revenue dependence
- `INFRASTRUCTURE` - hosting, identity, CRM, productivity, cloud, communications, data storage
- `LEGAL` - shared litigation, amicus coordination, defense strategy, legal-resource dependence
- `POLICY` - joint policy development, standards work, legislative coalitions
- `PERSONNEL` - board, staff, advisor, executive, or contractor crossover
- `INFORMATION` - privileged access, threat intelligence, research data, private briefings
- `REPUTATIONAL` - ratings, endorsements, public praise, reciprocal validation
- `COALITION` - recurring alliance membership or campaign coordination
- `ACCESS` - dependence on privileged meetings, APIs, internal contacts, or participation channels
- `PLATFORM` - dependence on a service provider for mission-critical public or internal activity

## Attributes

Each vector should be evaluated on:

- `directness`: direct / mediated / indirect
- `duration`: transient / recurring / persistent
- `replaceability`: easy / moderate / difficult
- `switching_cost`: low / medium / high
- `visibility`: public / partially public / opaque
- `reciprocity`: unilateral / asymmetric / mutual
- `mission_relevance`: peripheral / supporting / core
- `conflict_overlap`: none / adjacent / direct

## Suggested Record Shape

```yaml
vector_type: INFRASTRUCTURE
start_date: YYYY-MM-DD
end_date: null
directness: direct
duration: persistent
replaceability: moderate
switching_cost: medium
visibility: public
reciprocity: asymmetric
mission_relevance: supporting
conflict_overlap: adjacent
source: <provenance reference>
confidence: high
```

## Interpretation Rule

A dependency vector is not evidence of capture by itself. Its evidentiary value increases when it overlaps directly with the subject matter in which scrutiny becomes asymmetric.
