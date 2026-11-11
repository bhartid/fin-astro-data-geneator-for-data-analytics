# AI Operating Rules

**Applies to:** Every AI assistant or agent working on this project.  
**Purpose:** Allow an AI with no access to prior chats or persistent memory to understand the project and continue safely from the files alone.

## 1. Start-up protocol

Before answering or editing project material:

1. Read `00_governance/00_PROJECT_INDEX.md`.
2. Read this file and `PROJECT_AUTHORITY_AND_SOURCE_POLICY.md`.
3. Read `DECISION_LOG.md`, `OPEN_QUESTIONS_AND_CONFLICTS.md` and `05_delivery/CURRENT_PROGRESS.md`.
4. Read all task-relevant specifications and source documents.
5. Check whether the requested task is permitted at the current project stage.

Never rely on chat memory as the source of truth. The files are the project memory.

## 2. Project identity

The project is a research-oriented astronomical and astrology-derived data-generation library for financial time-series analysis. It produces timestamped raw astronomical values and derived feature values/events/periods that can be aligned with market candles or other market observations.

It does not generate investment advice, buy/sell signals, personal horoscopes or deterministic predictions. Do not drift into building a general-purpose astrology app.

## 3. Scope preservation

- Inventory broadly before designing narrowly.
- Do not delete or omit a feature because it is difficult, obscure, redundant-looking or deferred.
- Keep recognised variants separately identifiable where their calculation rules differ.
- If a feature is outside the initial implementation, retain it with a `DEFERRED` or other justified status.
- Do not assume the existing catalogues are exhaustive. Audit them against reputable primary sources and technical capabilities.
- Do not silently broaden the scope either. Record candidate features and their evidence before adding them to the approved inventory.
- Gann methods are an extension domain. Preserve them separately from standard Western/Vedic astrology and identify their astronomical inputs.

## 4. Shared foundation rule

Treat astronomy as a reusable, tradition-neutral service. Western and Vedic modules should request the astronomical quantities and configuration they need, then apply their own rule sets.

Do not hard-code astrology tradition into the low-level ephemeris adapter. Do not assume every tradition-specific difference is a flag: derived algorithms, reference tables, conventions and event rules may differ.

A foundation capability is not approved merely because one MVP feature uses it. It must be assessed against the full approved feature inventory and dependency graph.

## 5. Evidence and uncertainty

For every technical or tradition-specific claim:

- Identify the source and its authority.
- Verify exact Swiss Ephemeris function/flag behaviour against official documentation and the selected Python binding/version.
- Distinguish a library capability from an algorithm implemented by this project.
- Distinguish a widely used convention from a universal rule.
- Record alternate schools, regional conventions and disputed definitions.
- Do not turn an uncertain claim into a requirement.
- Use explicit labels: `SOURCE_CONFIRMED`, `OWNER_DECISION`, `AI_INFERENCE`, `NEEDS_RESEARCH`, `CONFLICTING_SOURCES`.
- If the supplied documents do not support a claim, say so and research it if the task permits.

## 6. Feature specification contract

Every feature must eventually have:

1. Stable feature ID and canonical name.
2. Tradition/domain and feature family.
3. Definition and intended research use.
4. Variants and school/convention differences.
5. Required raw astronomical inputs.
6. Required settings/flags and compatibility constraints.
7. Location and timezone requirements.
8. Dependencies on other features, reference tables or external data.
9. Calculation method, formula or rule sequence.
10. Output schema, units, coordinate basis and null/error semantics.
11. Time behaviour: instantaneous value, exact event, interval/period, fixed reference, or chart-relative value.
12. Boundary and event-detection semantics.
13. Provenance: direct ephemeris, mathematical derivation, tradition rule, search algorithm, external source.
14. Validation cases, expected values, tolerance and reference source.
15. Status, open questions and change history.

Do not mark a feature `DESIGNED` if its defining convention or output semantics remain ambiguous.

## 7. Do not conflate these categories

- **Direct ephemeris output:** returned by the ephemeris library.
- **Mathematical derivation:** computed from raw outputs using a general formula.
- **Tradition-specific rule:** computed using a defined astrological convention.
- **Event search:** finds an exact time or interval boundary by evaluating values over time and solving/searching for a condition.
- **Reference data:** fixed tables, mappings or constants.
- **External calendar data:** regional observance/festival data or other sources not determined solely by the ephemeris.
- **Research transformation:** feature engineering, statistical aggregation or Gann/market-specific calculation.

A feature may span more than one category; document each component separately.

## 8. Questions and decisions

Do not ask the owner questions whose answers are already in the knowledge base. Do not ask broad questions merely to avoid research.

Ask a question only when:
- two or more valid options materially affect scope or architecture;
- evidence cannot resolve a convention that the owner must choose;
- the decision has irreversible or expensive consequences;
- required project intent is genuinely absent.

When possible, recommend a default, explain consequences briefly, and ask one focused question. If no owner decision is needed, proceed autonomously and record uncertainty.

## 9. Document editing rules

- Preserve source documents in `99_source_documents/`.
- Do not edit archived originals.
- Preserve feature IDs and source wording unless a documented correction is approved.
- Add citations/source references inside the relevant document, not only in chat.
- Update the decision log only after an owner-approved decision.
- Update the open-questions register when discovering an unresolved issue.
- Update `CURRENT_PROGRESS.md` at the end of each work session.
- Never state that an audit is complete unless all listed audit checks have been performed.
- Avoid giant monolithic documents. Split feature families into small files when they become hard to navigate, but keep a central inventory index.

## 10. Session handoff format

At the end of each task, update the progress file with:
- stage and objective;
- files read;
- files created/changed;
- work completed;
- decisions confirmed (with decision IDs);
- open research questions;
- next exact task;
- instructions for the next AI.

The final chat response should briefly say what changed, what is not yet verified, and where the next AI should begin. Do not rely on conversational memory for handoff.
