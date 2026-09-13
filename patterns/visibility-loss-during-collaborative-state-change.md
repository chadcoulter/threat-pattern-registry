# Visibility Loss During Collaborative State Change

## Definition

A Visibility Loss failure occurs when the system continues generating, modifying, or persisting shared work while the human collaborator can no longer reliably inspect what was generated before or during that state change.

## Structural Signature

generation begins
-> artifact or state is produced
-> persistence or mutation is attempted
-> user visibility degrades or disappears
-> system action may continue
-> human collaborator loses the ability to verify the state transition

## Core Distinctions

generation success != user visibility

persistence success != inspectability

shared state exists != collaborator can verify shared state

## Threat Condition

The threat exists when the system can continue changing or saving collaborative work while the human collaborator loses reliable access to the generated state needed to review that action.

## Core Effect

Generation
-> Visibility Loss
-> State Change Continues
-> Human QC Removed
-> Collaboration Integrity Failure

## Failure Mode

The system may successfully generate or persist an artifact while the human collaborator cannot reliably see the exact state being acted on.

This removes the human quality-control checkpoint from the transition.

The result is a collaborative system in which state can advance without the collaborator being able to verify what advanced.

## Defensive Rule

no state transition without inspectable state

If the collaborator cannot reliably inspect the generated artifact, mutation or persistence should stop until visibility is restored.