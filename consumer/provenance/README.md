# Provenance Boundary

Provenance must survive every transition through the triadic framework.

At minimum, the framework should eventually preserve:

- originating system
- originating artifact ID
- source URL or repository reference
- upstream version / commit
- retrieval timestamp
- checksum where available
- license / attribution requirements
- transform history
- facilitator decisions
- resolver handoffs
- resolver outputs
- contradiction / retraction history
- authorization changes

The provenance layer is not merely audit logging. It is part of the evidence model.

A transformed claim should always be traceable backward through:

`RESOLUTION -> FACILITATOR EVENT -> TRANSFORM -> SOURCE ARTIFACT`

and forward through any later reuse or composition.
