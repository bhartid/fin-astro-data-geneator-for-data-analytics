# Project Authority, Sources and Evidence Policy

## 1. Authority hierarchy

When statements conflict, use this order:

1. Explicit owner-approved decisions in the decision log.
2. Original owner-authored `99_source_documents/project.md`.
3. Owner-approved current requirements/specifications.
4. Official Swiss Ephemeris documentation and official documentation for the exact Python binding/version selected.
5. Primary texts, scholarly editions, reputable specialist references or well-documented implementations for astrology methods.
6. Reputable secondary references.
7. Existing AI-generated catalogues and dependency analysis as working hypotheses only.

The hierarchy governs project intent and evidence quality. It does not make an owner-authored technical statement automatically correct: technical statements still need verification before implementation. If owner intent conflicts with a verified technical limitation, preserve the intent and document the limitation and options.

## 2. Required evidence labels

Use these labels consistently:

| Label | Meaning |
|---|---|
| `OWNER_DECISION` | Explicitly approved by the project owner |
| `SOURCE_CONFIRMED` | Supported by a cited authoritative source |
| `AI_INFERENCE` | Reasoned conclusion, not directly stated by a source |
| `NEEDS_RESEARCH` | Insufficient evidence; do not treat as settled |
| `CONFLICTING_SOURCES` | Credible sources disagree or use different conventions |
| `TECHNICALLY_UNSUPPORTED` | The selected library/version cannot provide the claimed capability directly |
| `NOT_APPLICABLE` | Capability does not apply to the selected object or calculation mode |

## 3. Swiss Ephemeris verification

For every claimed library function, flag, body constant, return field or limitation, record:
- official C API function/flag/constant;
- official documentation section and URL or versioned reference;
- Python binding name and version;
- whether the binding exposes the function/constant;
- required ephemeris files and licensing implications;
- inputs, output units and coordinate semantics;
- known failure modes and error handling.

Never infer that a feature is directly supported just because a related concept exists in the library. A feature may require a project-side derivation or search.

## 4. Astrology-method verification

For each tradition-specific feature:
- identify the tradition and school/lineage where known;
- cite a primary or reputable source for the definition;
- document alternate definitions and regional practices;
- distinguish calculation from interpretation;
- specify the exact rule variant selected for reproducible output;
- preserve unselected variants in the inventory where they are recognised and relevant.

Do not present one convention as universally accepted when sources show alternatives.

## 5. Research reproducibility

Each generated result should eventually be traceable to:
- input timestamp and time scale;
- location and observer parameters, if applicable;
- body/object identity;
- ephemeris source and data files;
- calculation flags and profile;
- zodiac and ayanamsha settings;
- algorithm/rule version;
- reference-table version;
- software and binding version;
- precision/tolerance and any warnings.

The implementation design must decide the exact metadata schema later. This list is a requirement for reproducibility, not a final schema.

## 6. External data

Festivals, regional observances, exchange calendars, historical market calendars and some interpretive lookup datasets may not be derivable from Swiss Ephemeris. Identify their provider, license, geographic coverage, versioning, timezone and update policy. Do not disguise externally sourced data as ephemeris output.

## 7. Licensing

Before selecting or distributing the ephemeris library, inspect the current Swiss Ephemeris license terms and the selected binding's license. Record whether the intended local-only use, redistribution, web deployment or commercial use requires a particular license. Do not give legal conclusions without authoritative license text or qualified legal advice.
