# Feature Specification Contract

Use this contract for every feature family and individual feature. Copy it into a dedicated file when the family is researched. Do not leave fields blank without stating why they are unknown or not applicable.

## A. Identity
- Feature ID:
- Canonical name:
- Aliases / translations:
- Domain:
- Family:
- Tradition / school / lineage:
- Parent feature / source catalogue ID:
- Status:

## B. Definition
- Operational definition:
- What the value/event/period means:
- Intended financial time-series research use:
- What it does NOT mean:
- Recognised variants:
- Disputed or regional conventions:

## C. Provenance
- Computation class: direct ephemeris / astronomical derivation / tradition rule / event search / reference lookup / external data / research transformation.
- Direct source/API function, if any:
- Project-side formula or rule:
- Reference tables and versions:
- External data source/license, if any:

## D. Inputs and configuration
- Required timestamp and time scale:
- Required body/object IDs and variants:
- Required raw quantities and units:
- Required coordinate origin/reference frame:
- Required coordinate system/reference plane:
- Required zodiac/ayanamsha:
- Required position semantics:
- Required observer location/altitude:
- Required timezone/calendar:
- Required house/chart context:
- Required market context:
- Optional inputs:
- Valid/invalid configuration combinations:

## E. Dependencies
- Upstream feature IDs:
- Required foundation capabilities:
- Required reference data:
- Required event-search primitives:
- Dependency edge types:
- Optional dependencies:

## F. Calculation
- Formula or algorithm, step by step:
- Normalisation/wrap-around:
- Boundary conditions:
- Rounding policy:
- Precision/tolerance:
- Missing-data/error behaviour:
- Retrograde/repeated-crossing behaviour, if applicable:

## G. Output contract
- Output fields:
- Types:
- Units:
- Coordinate semantics:
- Value domain:
- Temporal shape: instant / event / interval / fixed reference / chart-relative / aggregate.
- Start/end inclusivity:
- Nullability and error/warning semantics:
- Provenance metadata:

## H. Validation
- Authoritative references:
- Golden/reference cases:
- Expected outputs:
- Tolerance:
- Cross-check implementation:
- Edge cases:
- Regression tests:

## I. Decisions and change history
- Open questions:
- Owner decision required? Why?
- Recommended default and alternatives:
- Change history:
