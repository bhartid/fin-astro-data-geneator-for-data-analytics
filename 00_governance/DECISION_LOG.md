# Decision Log

This file contains decisions explicitly established by owner instructions or confirmed in project source material. It is not a list of AI recommendations.

| ID | Decision / constraint | Status | Evidence |
|---|---|---|---|
| D-001 | The project generates astronomical and astrology-derived data for financial time-series research. | CONFIRMED | `99_source_documents/project.md` |
| D-002 | Western and Vedic astrology must both be supported. | CONFIRMED | `project.md`; owner reiterated |
| D-003 | Do not omit valid Western/Vedic feature combinations merely because they are experimental. | CONFIRMED | `project.md` |
| D-004 | Keep W. D. Gann teachings and techniques in mind as a future extension domain. | CONFIRMED | `project.md` |
| D-005 | The project is for historical financial-market research, not personal horoscope or prediction output. | CONFIRMED | Owner's project context and scope |
| D-006 | Generate raw astronomical data for specified date-time ranges or moments and requested timeframes. | CONFIRMED | `project.md` |
| D-007 | Distinguish direct generated data from derived data. | CONFIRMED | `project.md` |
| D-008 | Validate input combinations before generation. | CONFIRMED | `project.md` |
| D-009 | A shared, largely tradition-neutral astronomy foundation should serve Western and Vedic feature engines. | OWNER CONFIRMED | Owner statement; boundaries now in `FOUNDATION_CAPABILITY_REGISTER.md` |
| D-010 | Complete and organise the broad feature inventory and dependency analysis before freezing the foundation. | OWNER CONFIRMED, AMENDED BY D-017 | Owner statement |
| D-011 | Knowledge must be stored in detailed, precise, small Markdown documents so a new AI can continue without chat memory. | OWNER CONFIRMED | Owner statement |
| D-012 | Current work is scoping/design, not implementation. | CONFIRMED | `project.md` |
| D-013 | Prefer Python `datetime` for date/time handling where appropriate. | CONFIRMED | Prior owner decision |
| D-014 | Local-first development; no UI in the current scope. | CONFIRMED | Prior owner direction |
| D-015 | Do not add caching or database/query-language work without owner approval. | CONFIRMED | Prior owner direction |
| D-016 | The complete raw, tradition-neutral foundation (shared by Western and Vedic, built on Swiss Ephemeris) is finalised first. | OWNER CONFIRMED 2026-11-12 | Owner statement in conversation |
| D-017 | After the foundation: Vedic features are audited and finalised end to end, then Western, then code. The full dependency-chain approach is retained; the owner declined the pattern-based coverage alternative. This amends the precondition in `ARCHITECTURE_AND_IMPLEMENTATION_GATE.md` that both inventories be audited before architecture: the audit is staged (foundation, Vedic, Western). | OWNER CONFIRMED 2026-11-12 | Owner statement in conversation |
| D-018 | The Python binding is `pyswisseph` only. | OWNER CONFIRMED 2026-11-12 | Owner statement. See Q-013 for Python-version consequence |
| D-019 | The AI performs Swiss Ephemeris verification and review. Documentation verification is done (`SWISS_EPHEMERIS_VERIFICATION_REPORT.md`); runtime probes are pending. This replaces the earlier plan to verify last. | OWNER CONFIRMED 2026-11-12 | Owner request in conversation |
| D-020 | The generic event-search primitive (function of time, threshold, window, tolerance; returns crossings) is part of the foundation. Tradition modules supply conditions, orbs and naming. | OWNER CONFIRMED 2026-11-12 | Owner agreed with the recommendation |
| D-021 | Target Python version is 3.11 (prebuilt pyswisseph wheels, no compiler needed). Resolves Q-013. | OWNER CONFIRMED 2026-11-12 | Owner statement in conversation |
| D-022 | Heliocentric Moon and heliocentric sidereal calculations are allowed as valid experimental combinations, flagged experimental. Overrides the invalid marking in `project.md` B.12 rows 11 and 14. Resolves Q-017. Other rules stay: Sun, nodes and apogees are rejected in heliocentric and barycentric frames; observer location is rejected with those frames. | OWNER CONFIRMED 2026-11-12 | Owner accepted AI recommendation |

## Provisional items (not final decisions)

- Final body catalogue and ephemeris-file strategy.
- Exact feature inventory completeness.
- Selected Vedic school/conventions for each feature.
- Selected Western tradition/conventions for each feature.
- Final calculation-profile schema and compatibility matrix (see Q-015, Q-017).
- Final foundation interfaces and architecture.
- Initial implementation slice and build order.
- Licensing route for any distribution or web service (Q-005).

## Change control

When a decision changes, do not overwrite history. Add a new entry with a new ID, reference the superseded decision, explain the reason and mark the old decision `SUPERSEDED`.