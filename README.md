# Threat Pattern Registry

This repository is an **AI Manipulation Defense** system: a defensive observability and pattern-recognition layer for AI-mediated environments.

## AI Manipulation Defense

An AI Manipulation Defense system identifies, records, and responds to manipulation introduced through AI-mediated interpretation, classification, filtering, recommendation, persistence, or state transition.

Its purpose is broader than malware defense. Traditional antivirus protects computation from hostile code. AI Manipulation Defense protects people, shared state, and collaborative integrity from hostile or distorting AI-mediated influence.

```text
malware defense
protects computation from hostile code

AI Manipulation Defense
protects people and shared state from hostile or distorting AI-mediated influence
```

The registry captures reusable patterns where AI-mediated systems can distort what a person can see, persist, share, verify, or act upon.

Observed classes currently include:

- persistence blocking;
- context-dependent write behavior;
- visibility loss during state change;
- collaboration inhibition;
- identity and authority distortion;
- evidence exclusion through synthetic resolution boundaries;
- and removal of human quality-control checkpoints from collaborative state transitions.

The repository therefore serves both as a pattern library and as a durable continuity layer for investigating AI-mediated manipulation and collaboration failure.

## Repository Structure

- `patterns/` - reusable threat, behavior, design, and defensive signatures
- `models/` - evidence, dependency, detection, resolution, and authority logic
- `cases/` - applications of patterns to specific entities or incidents
- `evidence/` - provenance, timelines, relationship graphs, and source records

See [`patterns/README.md`](patterns/README.md) for the current pattern registry.
