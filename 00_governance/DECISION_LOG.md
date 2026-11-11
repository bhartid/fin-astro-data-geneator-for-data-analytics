# Decision Log

This file contains decisions that are explicitly established by owner instructions or confirmed in project source material. It is not a list of AI recommendations.

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
| D-009 | A shared, largely tradition-neutral astronomy foundation should serve Western and Vedic feature engines. | OWNER CONFIRMED — ARCHITECTURE PRINCIPLE | Owner's explicit statement in conversation; detailed boundaries remain to be specified |
| D-010 | Complete and organise the broad feature inventory and dependency analysis before freezing the foundation. | OWNER CONFIRMED — PROCESS PRINCIPLE | Owner's explicit statement in conversation |
| D-011 | Knowledge must be stored in detailed, precise, small Markdown documents so a new AI can understand and continue without relying on chat memory or asking the owner to restate known context. | OWNER CONFIRMED — DOCUMENTATION PRINCIPLE | Owner's explicit statement in conversation |
| D-012 | Current work is scoping/design, not implementation. | CONFIRMED | `project.md` and prior owner direction |
| D-013 | Prefer Python `datetime` for date/time handling where appropriate. | CONFIRMED | Prior owner decision |
| D-014 | Local-first development; no UI in the current scope. | CONFIRMED | Prior owner direction |
| D-015 | Do not add caching or database/query-language work without owner approval. | CONFIRMED | Prior owner direction |

## Provisional items — not final decisions

- Exact Python binding (`pyswisseph` versus `pysweph`) and pinned version.
- Final body catalogue and ephemeris-file strategy.
- Exact feature inventory completeness.
- Selected Vedic school/conventions for each feature.
- Selected Western traditions/conventions for each feature.
- Final calculation-profile schema and compatibility matrix.
- Final foundation interfaces and architecture.
- Initial implementation slice and build order.
- Licensing route for any future distribution/commercial use.

## Change control

When a decision changes, do not overwrite history. Add a new entry with a new ID, reference the superseded decision, explain the reason and mark the old decision `SUPERSEDED`.
