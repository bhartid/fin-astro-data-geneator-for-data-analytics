# Shared Astronomy Foundation — Requirements (Preliminary)

**Status:** Requirements baseline only. Not an architecture freeze.  
**Design premise:** One reusable, tradition-neutral astronomical calculation layer should serve Western, Vedic and future research extensions.

## 1. Responsibility boundary

The common astronomy foundation is responsible for reproducible astronomical inputs and results. It must not embed Western or Vedic interpretive rules.

It should expose explicit, typed calculation requests and return results with sufficient metadata to reproduce and audit them. Higher layers may transform those results into zodiac positions, signs, aspects, Panchanga values, house-based features, events and research indicators.

## 2. Candidate capability domains to audit

The following are capability domains to evaluate against the complete feature inventory. This is not a claim that every item is directly provided by Swiss Ephemeris.

### 2.1 Time and ephemeris context
- Input civil datetime, timezone interpretation and conversion to UTC.
- Julian day/time representations and relevant time scales.
- Delta-T and UT/ET handling.
- Calendar system support where required.
- Sidereal time and equation of time.
- Explicit ephemeris source selection (Swiss, Moshier, JPL where supported).
- Ephemeris file discovery, availability and coverage diagnostics.
- Calculation warnings, errors and fallback reporting.

### 2.2 Celestial body identity and position
- Configurable body registry, not a hard-coded list limited to seven classical planets.
- Sun, Moon, planets, lunar nodes, lunar apsides and other bodies required by the approved inventory.
- Mean/true or other variants as distinct body definitions where relevant.
- Ecliptic longitude and latitude.
- Equatorial right ascension and declination.
- Distance and its rate of change where supported.
- Longitude, latitude and distance speed.
- Explicit coordinate origin/reference frame.
- Explicit apparent/true position semantics.
- Explicit coordinate epoch/equinox and reference-plane semantics where relevant.
- Output units, normalisation and precision.

### 2.3 Coordinate and reference-frame capabilities
- Geocentric.
- Topocentric, with observer coordinates and altitude where required.
- Heliocentric.
- Barycentric, if supported by the selected API and object.
- Ecliptic and equatorial coordinate outputs.
- Horizontal azimuth/altitude for observer-dependent calculations.
- Coordinate transformations as separate, traceable operations.

### 2.4 Observer and local-sky capabilities
- Observer latitude, longitude and altitude.
- Sunrise/sunset, moonrise/moonset, rise/set of supported bodies.
- Upper/lower meridian passages.
- Twilight definitions.
- Azimuth/altitude and apparent altitude/refraction conventions.
- Heliacal events and visibility calculations with atmospheric assumptions.
- Polar/high-latitude edge cases and no-event outcomes.

### 2.5 Planetary and lunar phenomena
- Phase angle, illuminated fraction, elongation, apparent diameter and magnitude where supported.
- Lunar phase/lunation support.
- Planetary nodes and apsides where available.
- Eclipse searches and local circumstances.
- Lunar occultation searches.
- Planetary transits across the solar disc.
- Synodic-cycle events derived by project-side search where no direct event function exists.

### 2.6 House and chart geometry
- Houses and angles for observer location and moment.
- House system selection and supported-system validation.
- Ascendant, Midheaven and other angles where supported.
- House position of bodies where supported.
- Gauquelin sectors where required.
- Explicit handling of polar latitudes and house calculation failures.
- Separation of astronomy-derived angles from tradition-specific house interpretation.

### 2.7 Fixed stars and special objects
- Fixed-star positions where retained in approved scope.
- Galactic reference points and coordinate definitions.
- Hypothetical bodies and extended asteroid/comet data only where approved and supported.
- Required data files and licensing/coverage constraints.

### 2.8 Event-search primitives
- Find crossings of a specified longitude/latitude/declination or other scalar condition.
- Find extrema (stationary points, greatest elongations, apsides where applicable).
- Find conjunctions/oppositions/aspect exactness as derived search operations.
- Find threshold crossings and interval boundaries.
- Return exact timestamp, bracket/search tolerance, direction of crossing, event classification and diagnostics.
- Handle multiple crossings, retrograde loops, wrap-around at 0°/360°, grazing/tangent events and no-event intervals.

## 3. Output contract requirements

Every raw result should be associated with:
- requested instant and interpreted input timezone;
- normalized UTC instant;
- time-scale/JD fields used in the calculation;
- body identifier and body-definition variant;
- coordinate origin/reference frame;
- coordinate system and reference plane;
- zodiac mode and ayanamsha only where applicable;
- ephemeris source and actual flags used;
- observer parameters if applicable;
- output values and units;
- calculation warnings/errors;
- library/binding version and data-file provenance;
- calculation profile/rule version.

Do not finalise field names or storage format until feature audit and architecture design.

## 4. Important architectural rule: raw versus transformed longitude

Avoid making the raw astronomy layer synonymous with a zodiac system. Where technically appropriate, preserve a canonical astronomical longitude and expose tropical/sidereal zodiac transformations as explicit, reproducible operations. Verify the precise Swiss Ephemeris coordinate conventions and flags before deciding whether one API call or separate calls are needed.

This enables one ephemeris result to support multiple downstream profiles without hiding the transformation or losing provenance.

## 5. Do not assume every feature requires every setting

Each feature must declare only the settings it actually needs. Examples:
- A geocentric position does not require observer location.
- A topocentric position does.
- Houses and local rise/set events require observer location.
- A heliocentric position does not become topocentric merely because a location is supplied.
- A sidereal sign feature requires an explicit sidereal convention/ayanamsha; a raw tropical astronomical coordinate does not inherently require one.
These are design principles to verify against the exact API and calculation.

## 6. Foundation acceptance gate

The foundation cannot be frozen until:
1. the complete inventory has been audited;
2. every feature has a dependency chain;
3. every required raw quantity and setting is mapped;
4. unsupported or external dependencies are identified;
5. valid configuration combinations are documented;
6. event-search requirements are covered;
7. output provenance and reproducibility requirements are specified;
8. known API limitations and licensing constraints are recorded;
9. the owner approves the resulting foundation requirements.
