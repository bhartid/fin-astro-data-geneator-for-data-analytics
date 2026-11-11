# Inputs, Flags and Compatibility — Working Specification

**Status:** Conceptual input taxonomy. The original compatibility matrix is retained in `99_source_documents/project.md` and must be audited against the official API before approval.

## 1. Input dimensions

Treat the following as independent configuration dimensions unless official API documentation proves a dependency:

1. **Time:** civil datetime, timezone, calendar, requested sampling interval, time scale.
2. **Ephemeris source:** Swiss Ephemeris, Moshier or JPL where supported.
3. **Body:** canonical body ID plus variant (for example mean node vs true node).
4. **Reference origin/frame:** geocentric, topocentric, heliocentric, barycentric.
5. **Coordinate family:** ecliptic, equatorial, horizontal or other supported system.
6. **Position semantics:** apparent/astrometric/true or other API-defined modes; do not use vague labels.
7. **Zodiac transformation:** tropical or sidereal; ayanamsha identifier and user-defined parameters when sidereal.
8. **Observer:** latitude, longitude, altitude, atmospheric/refraction assumptions when applicable.
9. **House geometry:** house system and any required location/time context.
10. **Output selection:** requested quantities and speed components.
11. **Search behaviour:** event condition, time window, search direction, tolerance and sampling/bracketing strategy.

## 2. Configuration profile versus feature request

A calculation profile describes reusable choices (for example ephemeris source, zodiac convention and coordinate settings). A feature request describes the actual feature and its dependencies. Do not let a profile silently request incompatible or irrelevant settings.

The system should validate:
- required inputs are present;
- unsupported combinations are rejected with a specific reason;
- irrelevant settings are ignored or rejected according to an explicit policy;
- actual API flags are recorded;
- global library state cannot leak between requests;
- multiple profiles can be evaluated deterministically.

## 3. Compatibility matrix requirements

For every combination, record:
- body eligibility;
- supported frame/origin;
- coordinate family;
- required flags;
- forbidden flags;
- required observer fields;
- required ephemeris files;
- API return semantics;
- fallback behaviour;
- exact documentation reference.

Do not infer support from a constant's existence. Validate the complete call signature and behaviour.

## 4. Known semantic traps to audit

- Geocentric versus topocentric is not the same as tropical versus sidereal.
- Heliocentric/barycentric origin is distinct from coordinate system (ecliptic/equatorial).
- Apparent versus true position must use the API's exact terminology and flag semantics.
- Mean node and true/osculating node are distinct definitions.
- Ketu/south node is generally derived as the antipode of the selected north node in the relevant coordinate convention; document the exact transformation.
- Mean lunar apogee and osculating lunar apogee are distinct; do not label both with an ambiguous "true Lilith".
- RA/Dec are equatorial coordinates; longitude/latitude may be ecliptic or another declared frame.
- House systems have individual limitations, including possible failures at high latitudes.
- A supplied location must not accidentally change calculations that are meant to be geocentric.
- Swiss Ephemeris settings can involve process/global state; isolate and restore settings or otherwise guarantee deterministic request handling.

## 5. Required validation before approval

Audit every source-project matrix row against the current official Swiss Ephemeris programmer documentation and the selected Python binding. Include positive and negative test cases. No matrix row is approved merely because it appears in the original project notes.
