# Configuration Compatibility Matrix and Validation Rules (v1.0 draft)

**Status:** DRAFT for owner confirmation of one principle (Q-023). Working version that supersedes `project.md` Sections B.12, C.4 and C.5 for design purposes. The archived `project.md` is not edited.
**Evidence base:** `SWISS_EPHEMERIS_VERIFICATION_REPORT.md` (documentation plus probes P-01 to P-15, 2026-11-23). Decisions D-003, D-008, D-018, D-022.
**Why this exists:** the library silently accepts many combinations that give wrong or meaningless results (zeros, dropped flags, fallbacks). The project must validate every request itself (D-008).

## 1. Principle: two layers

1. **Calculation layer** (this document). Decides whether a combination of origin, zodiac, body, ephemeris and observer is computable and meaningful as raw astronomy. Everything computable is allowed; combinations outside tradition are marked `EXPERIMENTAL`, not rejected (D-003).
2. **Feature layer** (Western/Vedic modules). Each feature declares what it needs (for example Tithi needs a geocentric Moon and Sun; Nakshatra needs a sidereal longitude by default). The engine rejects a feature on a profile that cannot supply its inputs, and flags it `EXPERIMENTAL` when it is run outside its tradition's usual setup.

`astrology_mode` (Western or Vedic) therefore only supplies default settings (see section 6). It does not restrict which bodies, frames or zodiacs can be requested. This follows the `project.md` input schema; it differs from the wording of `project.md` C.1 (see Q-023).

## 2. Result classes and evidence labels

| Class | Meaning |
|---|---|
| `VALID` | Computable and meaningful; allowed |
| `EXPERIMENTAL` | Computable, outside usual tradition; allowed, flagged in metadata |
| `REJECT` | Project must refuse with a specific reason (library would return zeros, drop flags, fail, or the result is meaningless) |
| `NOTE` | Allowed; a warning or effective-semantics record is attached |
| `TEST` | Not yet probed; treated as `REJECT` until tested, unless stated |

Evidence: `DOC` official documentation, `P-nn` probe result, `POLICY` project rule, `AI_INFERENCE`.

## 3. Origin by body matrix

Cells: V valid, E experimental, X reject, T needs test. A star `*` means: needs Swiss or JPL ephemeris (Moshier raises an error, P-06).

| Body group | Geocentric | Topocentric | Heliocentric | Barycentric |
|---|---|---|---|---|
| Sun | V | V | X (zeros, P-05) | V* T (accuracy 0.1 arcsecond, DOC) |
| Moon | V | V | E (D-022, P-05) | V* T |
| Mercury to Pluto | V | V | V (P-07 with Mars) | V* T |
| Earth | X (zeros, DOC) | X | V T | V* T |
| Lunar nodes (mean, true) | V | T | X (zeros, P-05) | X (zeros, DOC) |
| Lunar apogee and perigee (mean, osculating, interpolated) | V | T | X (zeros, P-05) | X (zeros, DOC) |
| Chiron, Pholus, main and numbered asteroids | V (data files) | T | T | T |
| Hypothetical / Uranian points | V (elements file) | T | T | X (not physical bodies, AI_INFERENCE, T) |
| Fixed stars | V (`sefstars.txt`) | T | T | T |

## 4. Validation rules

Every rule states what the library does if the project does not check.

### 4.1 Zodiac and time

| ID | Condition | Action | Evidence | Library behaviour if unchecked |
|---|---|---|---|---|
| R-001 | Sidereal zodiac without an explicit ayanamsha | REJECT | P-02 | Silently uses Fagan/Bradley (25.08 degrees in 2024) |
| R-002 | User-defined ayanamsha (mode 255) | Require reference epoch, value at epoch, and whether the epoch is UT | DOC | Undefined ayanamsha |
| R-003 | Sidereal with nutation requested on | REJECT; if nutation unspecified, record `nutation: forced_off` | P-03a, DOC | No-nutation flag is added silently |
| R-004 | Sidereal with equatorial output | NOTE: record the reference-equinox semantics of the chosen mode | DOC, TEST | Reference equinox varies by mode |
| R-005 | Heliocentric or barycentric with apparent position requested | NOTE: effective position is geometric (no aberration, no deflection); record actual flags | P-03b | Flags added silently |
| R-006 | Naive datetime or missing timezone | REJECT | D-013, F-A01 | Not applicable |
| R-007 | Calendar not stated | Default Gregorian; NOTE for dates before 1582-10-15 | AI_INFERENCE | Uses the calendar flag given |
| R-008 | Date outside ephemeris coverage (Moshier 3000 BCE to 3000 CE; file blocks of 600 years) | REJECT | DOC | Error or fallback |

### 4.2 Origin, observer and body

| ID | Condition | Action | Evidence | Library behaviour if unchecked |
|---|---|---|---|---|
| R-010 | Topocentric origin without latitude, longitude and altitude | REJECT | POLICY | Accepts altitude 0; uses stale or default position if never set (untested, Q-021) |
| R-011 | Topocentric combined with heliocentric or barycentric | REJECT | P-03c | Heliocentric flag dropped silently; a topocentric geocentric position is returned |
| R-012 | Observer location supplied with heliocentric or barycentric origin | REJECT | P-03c, POLICY | Same silent change as R-011 |
| R-013 | Heliocentric origin and Sun | REJECT | P-05 | Zeros, no error |
| R-014 | Heliocentric or barycentric origin and lunar nodes or apogees or perigee | REJECT | P-05, DOC | Zeros, no error |
| R-015 | Heliocentric Moon | ALLOW as EXPERIMENTAL | D-022, P-05 | Returns a valid position |
| R-016 | Heliocentric sidereal | ALLOW as EXPERIMENTAL | D-022, P-07 | Works; offset equals the ayanamsha |
| R-017 | Barycentric with Moshier ephemeris | REJECT | P-06 | Raises an error |
| R-018 | Barycentric for non-physical bodies | REJECT (TEST) | DOC, AI_INFERENCE | Zeros or error |
| R-019 | Geocentric or topocentric Earth | REJECT | DOC | Zeros |
| R-020 | Body outside its coverage window: Chiron outside 650 to 4650 CE, Pholus before 3850 BCE, Apollo before 1870 CE | REJECT | DOC | Error code and zero position |
| R-021 | Fixed star without the star catalogue file | REJECT with a clear message | P-15d | Raises "could not find star" |

### 4.3 Ephemeris source and state

| ID | Condition | Action | Evidence | Library behaviour if unchecked |
|---|---|---|---|---|
| R-030 | Returned ephemeris flag differs from the requested one (for example Swiss requested, Moshier returned) | REJECT unless the request sets `allow_fallback`; always record actual and requested flags | P-08 | Silent fallback; no warning string returned |
| R-031 | Sidereal mode or topocentric position assumed from earlier calls | Never assume. Set both inside the calling thread before every request | P-10 | Worker thread silently uses Fagan/Bradley |
| R-032 | Every result | Record requested flags, actual flags, ephemeris used, library and binding versions | F-I04, F-I07 | Not recorded |

### 4.4 Houses, horizon and sunrise

| ID | Condition | Action | Evidence | Library behaviour if unchecked |
|---|---|---|---|---|
| R-040 | House system without observer latitude and longitude | REJECT | DOC | Not computable |
| R-041 | Houses requested on a heliocentric or barycentric profile | REJECT | POLICY (from `project.md` B.12 row 12) | The library ignores the frame, so it would silently return Earth-based houses. Revisit if a feature needs them |
| R-042 | Placidus, Koch or Gauquelin beyond the polar circle | Structured error. Fall back to Porphyry only if the request sets `allow_house_fallback` | P-09, DOC | Binding raises an error and returns no fallback cusps |
| R-043 | Topocentric flag with houses | NOTE: the flag has no effect on house calculation | DOC, SRC | No effect |
| R-044 | Horizontal coordinates without observer location, or on heliocentric or barycentric origin | REJECT | POLICY | Meaningless result |
| R-045 | Sunrise-based feature without an explicit sunrise convention (astronomical or Hindu) | REJECT | P-13 | Different times, about 3.8 minutes apart at Mumbai |
| R-046 | Rise or set at a latitude with no event | Return a typed "no event" result, never a time | P-13 | Code `-2` with zeroed times |

### 4.5 Event search

| ID | Condition | Action | Evidence |
|---|---|---|---|
| R-050 | Crossing of Sun, Moon, Moon through ecliptic, heliocentric planet | Use native function where it fits; sidereal target allowed for the Sun after setting the mode | DOC, P-11 |
| R-051 | Crossing for any other body or quantity | Use the generic search (F-H01) | DOC |
| R-052 | Native crossing with topocentric or equatorial flags | TEST; use the generic search until tested | DOC |

## 5. Disposition of the original matrix (`project.md` C.4)

| Original row | Original verdict | New verdict | Reason |
|---|---|---|---|
| 1 Western, tropical, geocentric | Valid | VALID | |
| 2 Western, tropical, topocentric | Valid | VALID | Location required (R-010) |
| 3 Western, sidereal, geocentric | Valid | VALID | Ayanamsha explicit (R-001) |
| 4 Western, sidereal, topocentric | Valid, "not recommended" | VALID, advisory kept | Moon varies up to 1.54 degrees between cities (P-04), so results are location-specific. Advisory only, not a rejection |
| 5 Western, sidereal, heliocentric | Valid | EXPERIMENTAL | P-07 works |
| 6 Western, tropical, heliocentric | NOT valid, do not implement | **OWNER DECISION (Q-023)**, recommended EXPERIMENTAL | Computable; the library default heliocentric longitude is tropical; inventory items W-08 and W-65 (heliocentric coordinates, aspects, ingresses) are zodiac-independent for aspects |
| 7 Vedic, sidereal, geocentric | Valid, default | VALID (default profile) | |
| 8 Vedic, sidereal, topocentric | Valid | VALID | |
| 9 Vedic, tropical, geocentric | NOT valid | **OWNER DECISION (Q-023)**, recommended EXPERIMENTAL | At the calculation layer this is only the tropical zodiac; Vedic features declare their own needs |
| 10 Vedic, tropical, topocentric | NOT valid | **OWNER DECISION (Q-023)**, recommended EXPERIMENTAL | Same |
| 11 Vedic, tropical, heliocentric | NOT valid, reason "Moon has no heliocentric position" | **OWNER DECISION (Q-023)**, recommended EXPERIMENTAL | The stated reason is wrong (P-05). Moon-based Vedic features (Tithi, Nakshatra, Rahu, Ketu) are rejected at the feature layer because they need a geocentric frame |
| 12 Vedic, sidereal, heliocentric | Valid | EXPERIMENTAL | P-07; same feature-layer limits as row 11 |
| New: any mode, barycentric | Not present | EXPERIMENTAL, Swiss or JPL only | R-017, R-018 |

## 6. Defaults by astrology mode (defaults only, not restrictions)

Source: `project.md` input schema. Other defaults are undecided and marked.

| Setting | Western default | Vedic default |
|---|---|---|
| Zodiac | Tropical (usual practice; not in `project.md`) | Sidereal (matrix row 7) |
| Ayanamsha | Not applicable | Lahiri (schema) |
| Origin | Geocentric | Geocentric |
| House system | Whole Sign (schema, both modes) | Whole Sign (schema, both modes) |
| Lunar node type, apogee type, position type, nutation | Undecided | Undecided |
| Sunrise convention | Not applicable | Undecided (Q-019) |

## 7. Decision needed (Q-023)

Do you confirm this principle: the calculation layer allows every computable combination as `EXPERIMENTAL` (including your matrix rows 6, 9, 10 and 11, which `project.md` excluded), `astrology_mode` only sets defaults, and each feature module declares and enforces its own requirements?

Recommendation: yes. It matches D-003 (do not omit valid experimental combinations) and your input schema, and it costs nothing because experimental profiles are only run when someone asks for them. If you prefer to keep rows 6, 9, 10 and 11 excluded, say so and I will record that as an owner decision with its reason.

## 8. Remaining TEST items

Topocentric nodes and apogees; topocentric, heliocentric and barycentric asteroids and stars; barycentric with data files; native crossing with topocentric or equatorial flags; the exact polar-circle threshold for houses; behaviour when `set_topo` was never called (Q-021).