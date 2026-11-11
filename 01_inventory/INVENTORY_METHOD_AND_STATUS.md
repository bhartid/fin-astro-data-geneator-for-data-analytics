# Inventory Method, Classification and Status

## 1. Purpose

This document defines how the complete feature inventory is maintained. It prevents premature pruning and ensures that feature discovery, dependencies and foundation design are traceable.

## 2. Inclusion policy

The owner-authored project scope requires coverage of Western and Vedic astrology and says not to omit valid combinations merely because they are experimental. The existing catalogue uses a time-axis inclusion test: a recognised feature is included when it can be determined from astronomical positions, time, observer location and/or a chart of a person, company or instrument, and is time-varying or is fixed reference/chart data used with time-varying features.

For the expanded financial-research inventory, retain candidate features in one of these categories even if they do not meet the original catalogue's strict definition:
- recognised Western astrology;
- recognised Vedic astrology;
- common astronomical capability;
- financial astrology research method;
- Gann or related market-time method;
- external calendar/reference dataset;
- experimental or disputed method.

An item may be `CANDIDATE` pending evidence. Do not silently promote it to accepted scope.

## 3. Classification dimensions

Each inventory entry should be tagged along independent dimensions:

### 3.1 Domain
`ASTRONOMY`, `WESTERN`, `VEDIC`, `FINANCIAL_ASTROLOGY`, `GANN`, `EXTERNAL_DATA`, `CROSS_TRADITION`.

### 3.2 Computation provenance
`DIRECT_EPHEMERIS`, `ASTRONOMICAL_DERIVATION`, `TRADITION_RULE`, `EVENT_SEARCH`, `REFERENCE_LOOKUP`, `EXTERNAL_DATA`, `RESEARCH_TRANSFORMATION`.

A feature may have multiple provenance stages. Split the stages when their dependencies differ.

### 3.3 Temporal shape
`INSTANT_VALUE`, `EXACT_EVENT`, `INTERVAL`, `FIXED_REFERENCE`, `CHART_RELATIVE`, `AGGREGATE_SERIES`.

### 3.4 Location dependency
`NONE`, `OBSERVER_LOCATION`, `BIRTH_ORIGIN_LOCATION`, `MARKET_LOCATION`, `REGIONAL_CALENDAR`. Specify coordinates and timezone separately; do not use a vague single `LOCATION` label.

### 3.5 Maturity / evidence
`ESTABLISHED`, `SCHOOL_VARIANT`, `REGIONAL_VARIANT`, `EXPERIMENTAL`, `DISPUTED`, `UNVERIFIED_CANDIDATE`.

## 4. Lifecycle statuses

Use exactly one primary status per feature:

| Status | Definition |
|---|---|
| `NOT_REVIEWED` | Imported from source; not yet checked |
| `UNDER_RESEARCH` | Definition, tradition or technical capability is being investigated |
| `DEFINED` | Definition and relevant variants are documented |
| `DEPENDENCIES_MAPPED` | Inputs, settings, tables and upstream features are identified |
| `DESIGNED` | Algorithm, output contract, edge cases and validation plan are specified |
| `IMPLEMENTED` | Code exists in the approved implementation |
| `TESTED` | Tests pass against recorded references/tolerances |
| `DEFERRED` | Valid in scope but intentionally not in the current delivery stage |
| `REJECTED` | Reviewed and excluded with documented reason and owner approval where scope-affecting |

`REJECTED` must never mean "too difficult right now". Use `DEFERRED` for that.

## 5. Required inventory columns

At minimum:
- stable ID;
- canonical name;
- aliases/translations;
- domain and family;
- concise definition;
- temporal shape;
- computation provenance;
- tradition/school and variant;
- required raw astronomical inputs;
- required settings/flags;
- observer/chart/external-data requirements;
- dependencies;
- output units and semantics;
- source/evidence status;
- lifecycle status;
- unresolved questions;
- source catalogue location and change history.

## 6. IDs and traceability

- Preserve all original W-* and V-* IDs.
- Do not fill gaps based on numbering patterns.
- New items receive new IDs from a reserved range after checking for collisions.
- If one source entry contains several independently calculated variants, retain the original parent ID and create child variant identifiers (for example `V-014.a`) rather than destroying source traceability.
- If one source item must be split into multiple features, record the parent/source ID on every child.
- Never recycle IDs.

## 7. Completeness audit checklist

For every feature family, check:
1. The source catalogue entries are all present.
2. Important recognised variants are represented.
3. Time-series-relevant use cases are covered.
4. Chart-relative features are retained where applicable to company/instrument inception charts.
5. Direct ephemeris support is not confused with derived calculation.
6. Location and timezone needs are correctly identified.
7. Exact event/period boundaries are accounted for.
8. Required external tables/data are identified.
9. Western/Vedic overlap and differences are mapped.
10. Dependencies reach down to raw astronomical quantities and settings.
11. Output can be aligned reproducibly with market timestamps.
12. Evidence and uncertainty are recorded.

## 8. Review rule

Inventory review is not complete until every feature has a definition, provenance classification, dependency status and evidence status. A catalogue copied from an AI-generated source is not a verified inventory.
