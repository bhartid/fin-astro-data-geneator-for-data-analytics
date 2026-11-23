# Current Progress and Handoff

**Knowledge-base version:** 0.2.0
**Date:** 2026-11-12
**Current stage:** Foundation (raw, tradition-neutral) finalisation, then Vedic audit, then Western audit, then code (D-016, D-017).
**Overall status:** IN PROGRESS. No architecture or implementation approval.

## Completed

- Project index, governance, inventories, dependency model and source archive (v0.1.0).
- Owner decisions D-016 to D-022 recorded (D-021 Python 3.11, D-022 experimental heliocentric Moon and heliocentric sidereal allowed).
- `02_foundation/FOUNDATION_CAPABILITY_REGISTER.md` v1.0: capabilities F-A to F-I, each with class and verification label; traceability to dependency layer 1; Western checklist; open questions.
- `02_foundation/SWISS_EPHEMERIS_VERIFICATION_REPORT.md`: binding status, licence, confirmed library behaviours, audit of `project.md`, validation rules the project must own.
- `02_foundation/verification/verify_swisseph_probe.py`: throwaway probe script for runtime checks (not library code).

## Not completed / not claimed

- Runtime probes P-01 to P-15 have NOT been run. Rows labelled `TEST` in the register stay unconfirmed until they are.
- Official documentation after the refraction section (heliacal, date/time, topocentric setter, sidereal mode detail, houses, house position, sidereal time) was not read in full; those rows are labelled `TOC` or `SRC`.
- Official ayanamsha constant list and house-letter table not retrieved (Q-020).
- Western and Vedic inventories not audited. No ID register yet. No MVP. No architecture. No code.
- Inventory audit register: IA-011 should now read "PARTIALLY DONE: documentation verified, runtime probes pending". IA-004 and IA-010 have started through the foundation register.

## Owner actions pending

1. Run the probe script on Python 3.11 and return `probe_results.json`.
2. No other owner decisions pending.

## Next exact task

1. Update `TEST` rows in the register from probe results; rewrite the `project.md` Section C matrix as a corrected compatibility document.
2. Expand each F- capability with `FEATURE_SPECIFICATION_TEMPLATE.md`, in this order: time (F-A), positions and frames (F-B, F-C), observer and sunrise (F-D), houses (F-E), event search (F-H), state and metadata (F-I), then the rest.
3. Build the Vedic ID register (all V-* and V-E* IDs) and begin the Vedic audit family by family, mapping each feature to F- capabilities and recording gaps as new F- IDs.
4. Ask the owner only for genuine decisions. Research first.

## Instructions to the next AI

Read `00_governance/00_PROJECT_INDEX.md` and all mandatory governance files first. Treat source catalogues as working material. Do not ask the owner to restate project intent. The owner has no astrology background: do the research, cite sources, and present choices in plain terms. Preserve IDs. Update this file at the end of the session.