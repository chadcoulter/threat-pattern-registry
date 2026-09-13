---
id: collaboration-inhibition-001
title: "Collaboration Inhibition Attack"
status: "provisional"
class: "collaboration-coordination-threat"
version: "0.1"
---

# Collaboration Inhibition Attack

## Definition

A Collaboration Inhibition Attack occurs when an intermediary prevents collaborators from creating, persisting, sharing, or jointly modifying shared work, thereby disrupting the collaborative process itself.

## Structural Signature

```text
collaboration begins
-> shared work product develops
-> persistence, sharing, or modification is attempted
-> intermediary blocks the operation
-> shared state cannot advance
-> collaboration is inhibited
```

## Core Distinctions

`discussion permitted != collaboration permitted`

`artifact can exist != artifact can be persisted or shared`

## Core Effect

`Collaboration -> Intermediary Gate -> Inhibition -> Shared-State Disruption`
