# Current Progress and Handoff

**Knowledge-base version:** 0.3.0
**Date:** 2026-11-23
**Current stage:** Foundation (raw, tradition-neutral) finalisation, then Vedic audit, then Western audit, then code (D-016, D-017).
**Overall status:** IN PROGRESS. No architecture or implementation approval.

## Completed

- Project index, governance, inventories, dependency model and source archive (v0.1.0).
- Owner decisions D-016 to D-022 recorded.
- `02_foundation/FOUNDATION_CAPABILITY_REGISTER.md` v1.1: capabilities F-A to F-I with class and verification label, updated with probe results.
- `02_foundation/SWISS_EPHEMERIS_VERIFICATION_REPORT.md`: documentation verification plus probe results (section 6A).
- Runtime probes P-01 to P-15 run by the owner on 2026-11-23 (Windows, Python 3.12.10, pyswisseph 2.10.3.2, Swiss Ephemeris 2.10.03, Moshier ephemeris).

## Corrections made after the probes (AI statements that were wrong)

- Prebuilt wheels: the claim "only CPython 3.6 to 3.11" is contradicted; a cp312 binary loaded (Q-013 reopened).
- Sankranti: native `solcross_ut` DOES support the sidereal flag; the original dependency-document claim was right.
- Topocentric + heliocentric: the heliocentric flag is dropped (not the topocentric one).
- Moon position between cities: the `project.md` "1 to 2 degrees" claim is supported (1.54 degrees measured).
- Confirmed as expected: Fagan/Bradley default, heliocentric Moon works, Sun/nodes/apogees zero in heliocentric, sidereal state is per-thread, Moshier fallback visible only through returned flags, polar houses raise errors, azimuth counted from south, Hindu sunrise about 3.8 minutes later than astronomical at Mumbai.

## Not completed / not claimed

- Remaining `TEST` items: register section 9 (topocentric default state, barycentric with data files, house-letter table, `houses_ex2`, data-file functions, eclipse/occultation/heliacal calls, ayanamsha constant names).
- Official documentation after the refraction section not read in full.
- Western and Vedic inventories not audited. No ID register yet. No MVP, architecture or code.
- Inventory audit register: IA-011 should read "PARTIALLY DONE: documentation verified, core probes run, remaining items in register section 9". IA-004 and IA-010 have started through the foundation register.

## Owner action pending

Confirm the target Python version (Q-013). The probes ran on 3.12.10, but D-021 says 3.11. To see whether a prebuilt cp312 wheel exists, run in a terminal:

    pip download pyswisseph==2.10.3.2 --no-deps --only-binary=:all: --python-version 3.12 --platform win_amd64 -d wheelcheck

If it downloads a `.whl` file, a prebuilt wheel exists and either version works without a compiler. If pip reports no matching distribution, the package was built locally on that machine and 3.12 needs a compiler.

## Next exact task

1. Rewrite the `project.md` Section C compatibility matrix as a corrected compatibility document using D-022 and the probe results.
2. Expand each F- capability with `FEATURE_SPECIFICATION_TEMPLATE.md`, in this order: time (F-A), positions and frames (F-B, F-C), observer and sunrise (F-D), houses (F-E), event search (F-H), state and metadata (F-I), then the rest.
3. Build the Vedic ID register (all V-* and V-E* IDs) and begin the Vedic audit family by family, mapping each feature to F- capabilities and recording gaps as new F- IDs.
4. Ask the owner only for genuine decisions. Research first.

## Instructions to the next AI

Read `00_governance/00_PROJECT_INDEX.md` and all mandatory governance files first. Treat source catalogues as working material. Do not ask the owner to restate project intent. The owner has no astrology background: do the research, cite sources, and present choices in plain terms. Preserve IDs. Update this file at the end of the session.