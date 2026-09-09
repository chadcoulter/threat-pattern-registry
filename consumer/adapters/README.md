# Source Adapter Boundary

Adapters connect external research systems to the consumer framework.

Each adapter should eventually be responsible for:

- locating or receiving source artifacts
- preserving upstream identifiers
- preserving upstream version / commit information
- validating basic source integrity
- normalizing source-specific fields into the interchange contract
- attaching licensing and attribution metadata
- handing normalized material to the facilitator

Adapters are not resolvers. They should not silently upgrade evidence confidence or authority.

Python is a natural implementation choice for many adapters because of its data, API, ML, and security ecosystem, but this folder is intentionally language-neutral.

Initial source: PLOT4AI under `/plot4ai`.
