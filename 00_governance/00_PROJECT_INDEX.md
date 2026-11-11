# Financial Astrology Data Generator — Project Index

**Document type:** Mandatory AI entry point  
**Knowledge-base version:** 0.1.0 (initial organisation of supplied source documents)  
**Status:** Inventory organisation started; feature completeness and technical claims are NOT YET VERIFIED.

## 1. Purpose

This project defines and ultimately builds a portable, extensible Python library that generates astronomical and astrology-derived time-series data for financial-market research. It aligns generated values, events and periods with market data timestamps and timeframes so that historical relationships, recurring patterns and possible correlations can be investigated.

It is not a horoscope application, natal-reading product, prediction engine, trading system, execution platform or UI project. The present work is scoping, research, specification and architecture. Implementation planning follows only after the full intended feature space and dependencies have been understood.

## 2. Mandatory reading order for every AI

Before doing any project task, read:

1. `00_governance/AI_OPERATING_RULES.md`
2. `00_governance/PROJECT_AUTHORITY_AND_SOURCE_POLICY.md`
3. `00_governance/DECISION_LOG.md`
4. `05_delivery/CURRENT_PROGRESS.md`
5. The task-specific files listed in section 5 below.

If the AI cannot access a listed file, it must say so and must not pretend it has read it. Do not ask the owner to repeat information already present in these documents.

## 3. Authority order

1. Explicit project-owner decisions recorded in this knowledge base.
2. `99_source_documents/project.md` (original owner-authored source).
3. Current approved specifications and decision log.
4. Official Swiss Ephemeris documentation and the exact selected Python binding documentation/version.
5. Primary or reputable sources for named Western, Vedic, financial-astrology and Gann methods.
6. Existing AI-generated catalogues and comparison documents: useful working material, not proof of correctness or completeness.

If sources conflict, record the conflict in `00_governance/OPEN_QUESTIONS_AND_CONFLICTS.md`. Do not silently choose a side. Owner-authored instructions outrank generated material, but technical claims still require validation before implementation.

## 4. Project-wide non-negotiable principles

- Do not omit a valid Western, Vedic or experimental feature merely because it is uncommon, difficult, or not planned for the first implementation.
- Keep Western, Vedic, financial-astrology and Gann-related feature families visible in the inventory. Mark them as deferred or experimental rather than deleting them.
- The complete inventory and dependency analysis must precede final foundation design.
- Prefer one shared, tradition-neutral astronomical foundation. Tradition-specific calculations consume shared astronomical outputs and apply their own conventions, rules and reference data.
- Do not assume that the only differences between traditions are input flags. Some differences are downstream algorithms, definitions, tables and event-boundary rules.
- Separate direct ephemeris outputs, mathematical derivations, tradition-specific rules, event searches, reference data and externally sourced calendar data.
- Every feature must identify its dependencies, configuration requirements, location requirements, output semantics, time behaviour, provenance and validation strategy.
- Preserve existing feature IDs. Never renumber or reuse an ID without an explicit migration record.
- Do not invent missing feature IDs or infer missing features from gaps in numbering.
- No implementation, architecture freeze or MVP pruning until the owner approves the relevant stage.
- Keep scope concise at the project level, but feature specifications must be sufficiently precise for a new AI to continue without oral explanation.
- Ask the owner only when a genuine owner decision is required. For research questions, research first and present evidence/options.
- Do not claim Swiss Ephemeris supports a calculation until verified against official documentation and the selected binding version.
- Respect licensing obligations before distribution or commercial use.

## 5. Document map

### Governance
- `00_governance/AI_OPERATING_RULES.md` — how any AI must work, preserve context and hand off.
- `00_governance/PROJECT_AUTHORITY_AND_SOURCE_POLICY.md` — source hierarchy and evidence standards.
- `00_governance/DECISION_LOG.md` — approved decisions and provisional assumptions.
- `00_governance/OPEN_QUESTIONS_AND_CONFLICTS.md` — unresolved owner decisions and research conflicts.

### Inventory
- `01_inventory/INVENTORY_METHOD_AND_STATUS.md` — inclusion rules, classifications, status definitions and audit process.
- `01_inventory/WESTERN_FEATURE_INVENTORY.md` — Western catalogue, retaining original IDs and wording.
- `01_inventory/VEDIC_FEATURE_INVENTORY.md` — Vedic catalogue, retaining original IDs, Marathi names and wording.
- `01_inventory/EXCLUSIONS_AND_BOUNDARIES.md` — excluded items and reasons from the source catalogue; exclusions remain reviewable.
- `01_inventory/INVENTORY_AUDIT_REGISTER.md` — gaps, duplicates, ambiguity, evidence and completeness audit results.

### Shared foundation
- `02_foundation/SHARED_ASTRONOMY_FOUNDATION_REQUIREMENTS.md` — tradition-neutral foundation capabilities and raw output domains.
- `02_foundation/INPUTS_FLAGS_AND_COMPATIBILITY.md` — configuration dimensions and compatibility rules requiring technical verification.
- `02_foundation/TIME_LOCATION_AND_COORDINATE_SEMANTICS.md` — time scales, locations, frames and coordinate conventions.

### Tradition specifications
- `03_tradition_features/WESTERN_FEATURE_SPECIFICATIONS.md` — specification contract and Western rule families; expand into smaller family files as research proceeds.
- `03_tradition_features/VEDIC_FEATURE_SPECIFICATIONS.md` — specification contract and Vedic rule families; expand into smaller family files as research proceeds.
- `03_tradition_features/FINANCIAL_ASTROLOGY_AND_GANN.md` — research extensions and input dependencies.

### Dependencies
- `04_dependencies/DEPENDENCY_MODEL_AND_LAYERS.md` — dependency layer model from the source analysis.
- `04_dependencies/SHARED_VS_TRADITION_SPECIFIC.md` — shared astronomy versus downstream tradition-specific computation.

### Delivery
- `05_delivery/ARCHITECTURE_AND_IMPLEMENTATION_GATE.md` — conditions that must be met before architecture is frozen.
- `05_delivery/CURRENT_PROGRESS.md` — exact continuation point and next actions.

### Source archive
- `99_source_documents/` — exact copies of the three supplied source documents. These are retained for traceability; do not edit them as part of normal updates.

## 6. How to continue a task

1. Identify the task and the files that govern it.
2. Read the full relevant sections, not only this index.
3. State which facts come from owner sources, which are externally verified, and which are AI analysis.
4. Make the smallest useful change that advances the current stage.
5. Preserve IDs, terminology and source traceability.
6. Update the inventory audit register if feature scope or completeness is affected.
7. Update the decision log only for decisions actually approved by the owner.
8. Update current progress before handing off.
9. Provide a concise change summary and list any unresolved issues.

## 7. Current project stage

**Stage:** Knowledge-base organisation and full feature-inventory audit.  
**Not approved yet:** Final feature completeness, foundation freeze, architecture freeze, MVP selection and implementation.  
**Immediate objective:** Turn the existing feature catalogues into a traceable, complete, dependency-aware knowledge base without losing source material or prematurely narrowing scope.
