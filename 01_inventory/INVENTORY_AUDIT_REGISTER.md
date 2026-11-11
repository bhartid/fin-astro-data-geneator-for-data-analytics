# Inventory Audit Register

**Audit status:** NOT STARTED — initial files organised only.  
**Important:** No claim is made that the feature catalogue is complete, technically accurate or internally consistent.

## 1. Source material under audit

| Source | Role | Audit state |
|---|---|---|
| `99_source_documents/project.md` | Owner-authored project goals, constraints, Swiss Ephemeris constants, input schema and compatibility notes | Imported; detailed technical audit pending |
| `99_source_documents/feature_catalogue_western_and_vedic.md` | Working Western/Vedic feature catalogue, exclusions and Marathi terminology | Split into Western and Vedic working inventories; semantic audit pending |
| `99_source_documents/feature_dependency_and_tradition_comparison.md` | Working dependency layers and tradition comparison | Preserved; technical and completeness audit pending |

## 2. Audit work packages

| Audit ID | Area | Required checks | Status |
|---|---|---|---|
| IA-001 | Source preservation | Confirm every source document is archived byte-for-byte or text-equivalent; preserve original IDs and tables | ORGANISATION DONE; hash verification pending |
| IA-002 | Western inventory | Review every W-* entry, family coverage, variants, definitions and omissions against reputable sources | NOT STARTED |
| IA-003 | Vedic inventory | Review every V-* entry, Marathi labels, school/lineage variants, definitions and omissions | NOT STARTED |
| IA-004 | Common astronomy | Inventory all raw astronomical outputs and relevant Swiss Ephemeris capabilities, including less obvious data needed downstream | NOT STARTED |
| IA-005 | Cross-tradition overlap | Distinguish shared raw inputs from distinct downstream definitions and algorithms | NOT STARTED |
| IA-006 | Financial astrology | Identify time-series research methods and derived features beyond conventional chart reading | NOT STARTED |
| IA-007 | Gann extensions | Catalogue methods separately; map their astronomical and market-data dependencies | NOT STARTED |
| IA-008 | Exclusions | Revisit each exclusion for financial-research relevance and external-data role | NOT STARTED |
| IA-009 | Dependency graph | Trace every accepted/candidate feature to raw inputs, settings, reference data and algorithms | NOT STARTED |
| IA-010 | Foundation gap analysis | Identify missing foundation capabilities before architecture design | BLOCKED UNTIL IA-002–IA-009 |
| IA-011 | Technical verification | Validate Swiss Ephemeris API claims, constants, flags, files, limitations and binding availability | NOT STARTED |
| IA-012 | Market-time semantics | Define candle timestamp, interval closure, exchange timezone and event-to-bar mapping | NOT STARTED |

## 3. Known cautions from initial reading

These are audit leads, not settled corrections:

- Catalogue IDs contain gaps. Do not infer missing features from them.
- Some source rows combine several concepts or variants; these may need parent/child feature decomposition.
- Some entries label an ayanamsha requirement even when the underlying raw astronomical quantity may be available in tropical coordinates and sidereal conversion is a later transformation. Verify at the correct layer.
- Some location requirements are too broad or potentially misleading. Separate observer coordinates, chart-origin location, market location, timezone and regional calendar.
- Some items called "direct" may actually require project-side derivation or an event search.
- A current-state feature and its exact start/end events often belong to different dependency stages.
- A single label such as "true" can mean different things in different contexts (true node, true position, osculating apogee, etc.); use precise definitions.
- The catalogue's rule that features must be recognised and time-determined may need an explicit candidate class for experimental financial research methods.
- The source project's parameter matrix must be checked against official API semantics, not accepted as universally correct.
- The source feature catalogue may mix classical, modern, regional and school-specific practices. These must be labelled rather than flattened.

## 4. Completion criteria

This register may be marked complete only when every audit work package has:
- a documented result;
- source references;
- identified additions, removals or splits;
- unresolved issues recorded;
- owner decisions clearly separated from AI recommendations;
- dependencies mapped to foundation requirements.

Only after this may the shared foundation requirements be considered complete enough for architecture design.
