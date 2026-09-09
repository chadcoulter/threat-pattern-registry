# PLOT4AI Integration

This root-level project contains the interoperability layer for consuming, mapping, and contributing research between the Threat Pattern Registry and PLOT4AI.

## Goals

- Preserve PLOT4AI provenance and license boundaries.
- Map PLOT4AI atomic threat cards to higher-order registry patterns.
- Avoid copying upstream content into canonical pattern definitions.
- Make upstream contribution straightforward when local research yields a PLOT4AI-compatible atomic threat.

## Structure

- `manifest.yaml` - upstream source, license, retrieval, and pinning metadata.
- `mappings.yaml` - mappings from PLOT4AI cards to local pattern IDs.
- `CONTRIBUTING-UPSTREAM.md` - rules for turning local findings into upstream contributions.

The consumer implementation lives separately at `/consumer`.
