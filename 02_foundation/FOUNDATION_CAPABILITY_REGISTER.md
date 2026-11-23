# Foundation Capability Register (v1.0)

**Status:** Reviewed and documentation-verified. Runtime probes pending (see `verification/verify_swisseph_probe.py`). Not an architecture freeze. Replaces draft v0.1.
**Binding:** `pyswisseph` only (decision D-018). Evidence and findings: `SWISS_EPHEMERIS_VERIFICATION_REPORT.md`.
**Scope:** the raw, tradition-neutral foundation used by Western, Vedic, financial-astrology and Gann modules.

## 1. Rules

- No tradition rules here: no signs-as-meaning, nakshatras, tithis, dignities, aspects, dashas, yogas.
- The generic event-search primitive IS foundation (D-020). Tradition modules supply the condition, orb and naming.
- IDs use the prefix `F-`. Never renumber or reuse. Added items continue the sequence inside each group.
- Constraint D-015 (no caching) applies. Search speed must come from algorithm design.

## 2. Classes and verification labels

| Class | Meaning |
|---|---|
| `DIRECT` | Returned by a Swiss Ephemeris call |
| `DERIVED_FOUNDATION` | Generic math or conversion on raw values; no tradition rule |
| `EVENT_SEARCH` | Finds moments or intervals by evaluating values over time |
| `PLUMBING` | Time, configuration, validation, state, metadata, errors |

| Verification label | Meaning |
|---|---|
| `DOC` | Read in the official Swiss Ephemeris programmer documentation |
| `TOC` | Function existence confirmed in the official contents list only; parameters not read |
| `SRC` | Confirmed in Swiss Ephemeris or binding source code or binding documentation |
| `COMM` | Third-party or community source only |
| `TEST` | Needs a runtime probe on the owner's machine |
| `DESIGN` | Project-side design item; nothing to verify |

## 3. Capabilities

### A. Time and ephemeris context

| ID | Capability | Class | Candidate pyswisseph name | Verification and notes |
|---|---|---|---|---|
| F-A01 | Civil datetime + IANA timezone to UTC instant; reject naive or ambiguous input | PLUMBING | Python `datetime`, `zoneinfo` | DESIGN. D-013 |
| F-A02 | UTC to Julian Day (UT) and TT/ET; delta-T | DIRECT | `julday`, `utc_to_jd`, `deltat_ex` | TOC + SRC. Leap seconds via `seleapsec.txt` |
| F-A03 | Calendar selection | PLUMBING | `GREG_CAL`, `JUL_CAL` | SRC |
| F-A04 | Sidereal time (Greenwich and local, ARMC) | DIRECT | `sidtime` | TOC |
| F-A05 | Equation of time | DIRECT | `time_equ` | TOC |
| F-A06 | Ayanamsha value | DIRECT | `set_sid_mode`, `get_ayanamsa_ex_ut` | DOC. If no mode is set the default is Fagan/Bradley |
| F-A07 | Ephemeris source selection, data path, coverage diagnostics | PLUMBING | `set_ephe_path`, flags | DOC. `set_ephe_path` first; env `SE_EPHE_PATH` overrides; 256-byte limit; Swiss falls back to Moshier when files are missing |
| F-A08 | Local mean and apparent solar time | DIRECT | `time_equ`, `lmt_to_lat`, `lat_to_lmt` | TOC |
| F-A09 | Sampling-grid generator for interval and range | PLUMBING | n/a | DESIGN. Bar convention deferred to IA-012 |
| F-A10 | Delta-T, leap-second and Earth-orientation data policy (`swe_deltat.txt`, `seleapsec.txt`, tidal acceleration, user delta-T, optional EOP files) | PLUMBING | `set_tid_acc`, `set_delta_t_userdef` | TOC + DOC. NEW in v1.0 |

### B. Bodies and positions

| ID | Capability | Class | Candidate pyswisseph name | Verification and notes |
|---|---|---|---|---|
| F-B01 | Body registry: ID, variant, constant, data-file need, frame eligibility, date coverage | PLUMBING | n/a | DESIGN. Numbering seen in docs: 0 to 22, fictitious 40 to 54, planetary moons 9000+, asteroids 10000+, nutation `-1` |
| F-B02 | Ecliptic longitude, latitude, distance and three speeds | DIRECT | `calc_ut` | DOC. No flags gives apparent geocentric ecliptic of date. Speed needs the speed flag |
| F-B03 | Equatorial RA, declination, distance and speeds | DIRECT | `calc_ut` + equatorial flag | DOC. With sidereal modes the equinox reference varies (see report) |
| F-B04 | Position semantics: apparent, true, astrometric, J2000, no-nutation, ICRS, JPL Horizons, XYZ, radians | DIRECT | flags | DOC. Sidereal calculations force the no-nutation flag. Heliocentric and barycentric force no-aberration and no-deflection |
| F-B05 | Lunar nodes, mean and true | DIRECT | `MEAN_NODE`, `TRUE_NODE` | DOC |
| F-B06 | South node (antipode of chosen north node) | DERIVED_FOUNDATION | from F-B05 | DESIGN |
| F-B07 | Lunar apogee: mean, osculating, interpolated; interpolated perigee | DIRECT | `MEAN_APOG`, `OSCU_APOG`, `INTP_APOG`, `INTP_PERG` | DOC. Interpolated variants were missing from `project.md` |
| F-B08 | Earth as a body | DIRECT | `EARTH` | DOC. Geocentric Earth returns zeros |
| F-B09 | Chiron, Pholus, Ceres, Pallas, Juno, Vesta | DIRECT | `CHIRON`, `PHOLUS`, `CERES`, `PALLAS`, `JUNO`, `VESTA` | DOC. Needs `seas_*` files |
| F-B10 | Numbered asteroids | DIRECT | `AST_OFFSET` + number | DOC. Files in `ast0` to `ast9` subfolders; long (6000 yr) and short (600 yr) files |
| F-B11 | Hypothetical bodies: Uranian set, Transpluto, Nibiru, Harrington, and others | DIRECT | fictitious range 40 to 54 | DOC. Built-in elements; user-defined via `seorbel.txt` |
| F-B12 | Planetary moons and centre-of-body positions | DIRECT | moon offset 9000 | DOC. NEW. Needs `sat/` files; COB limited to 1900 to 2047 |
| F-B13 | Obliquity of the ecliptic and nutation values | DIRECT | `ECL_NUT` body | DOC. NEW |
| F-B14 | Per-body time-coverage validation (for example Chiron valid 650 to 4650 CE; Pholus not before 3850 BCE) | PLUMBING | n/a | DOC. NEW. Out-of-range returns error code and zero position |
| F-B15 | Planetocentric positions (positions seen from another body) | DIRECT | `calc_pctr` | DOC. NEW. CANDIDATE, deferred |

### C. Frames, coordinates and zodiac

| ID | Capability | Class | Candidate pyswisseph name | Verification and notes |
|---|---|---|---|---|
| F-C01 | Origin: geocentric (default), topocentric, heliocentric, barycentric | DIRECT | flags | DOC. Heliocentric: all planets including Moon; Sun, nodes, apogees return zeros with no error. Barycentric "not completely implemented": Swiss/JPL only, physical bodies only, zeros for nodes and apogees |
| F-C02 | Topocentric observer setup (lon, lat, altitude m) | DIRECT | `set_topo` | DOC. Topocentric flag is dropped if combined with heliocentric or barycentric |
| F-C03 | Zodiac: tropical or sidereal; ayanamsha ID or user-defined (reference epoch, initial value); user epoch in UT option; ecliptic-of-t0 and solar-system-plane projection options | DIRECT | `FLG_SIDEREAL`, `set_sid_mode` | DOC. No silent default allowed in this project (Fagan/Bradley is the library default) |
| F-C04 | Tropical-to-sidereal transform as a separate operation | DERIVED_FOUNDATION | from F-A06 | Valid only for the traditional (subtraction) method. Projection modes need the library flag. Q-F1 |
| F-C05 | Coordinate transforms (ecliptic and equatorial, with speed) | DIRECT | `cotrans`, `cotrans_sp` | TOC |
| F-C06 | Angle normalisation, signed and unsigned difference, wrap-around | DERIVED_FOUNDATION | n/a | DESIGN. Library helpers exist (`degnorm`, `difdeg2n`) |
| F-C07 | Longitude to equal-division index and offset | DERIVED_FOUNDATION | n/a | DESIGN. Meaning of divisions is tradition-owned |

### D. Observer and local sky

| ID | Capability | Class | Candidate pyswisseph name | Verification and notes |
|---|---|---|---|---|
| F-D01 | Observer model: lat, lon, altitude, datum/source; timezone kept separate | PLUMBING | n/a | DOC. East longitude and north latitude are positive. Geographic vs geocentric latitude is a documented distinction |
| F-D02 | Horizontal coordinates, refraction | DIRECT | `azalt`, `azalt_rev`, `refrac` | DOC. **Azimuth is measured from the south point towards the west**, not from north |
| F-D03 | Rise, set, upper/lower meridian transit, civil/nautical/astronomical twilight | DIRECT | `rise_trans` | DOC. Returns the next event after the start time. Code `-2` means circumpolar (no event) |
| F-D04 | Day/night interval between consecutive rise and set events | DERIVED_FOUNDATION | from F-D03 | DESIGN. Sunrise-anchored day rules belong to tradition |
| F-D05 | Rise/set convention profiles: astronomical (upper limb, refraction on) vs Hindu (disc centre, no refraction, geocentric, no ecliptic latitude); disc-bottom; fixed disc size; local horizon height | DIRECT | `BIT_*` flags, `rise_trans_true_hor` | DOC. NEW. A dedicated Hindu flag exists. Critical for Vara and all sunrise-based features |

### E. Houses and angles

| ID | Capability | Class | Candidate pyswisseph name | Verification and notes |
|---|---|---|---|---|
| F-E01 | House cusps and angles for a chosen system, tropical or sidereal | DIRECT | `houses_ex` | DOC + SRC. 12 cusps (36 for Gauquelin). Angles: Asc, MC, ARMC, Vertex, equatorial ascendant, two co-ascendants, polar ascendant; Sun declination returned for Sunshine systems. Placidus, Koch and Gauquelin fail beyond the polar circle (Porphyry returned plus error); Sunshine can also fail |
| F-E02 | House position of a body (number with fraction) | DIRECT | `house_pos` | TOC |
| F-E03 | Gauquelin sectors | DIRECT | `gauquelin_sector`, `house_pos` | TOC + COMM. Methods 0 to 5 exist |
| F-E04 | Whole-sign and equal-house variants | DIRECT | letters `W`, `N`, `A`, `E`, `D`, `V` | COMM for letters. Which are computed by the library vs derivable: TEST |
| F-E05 | Cusp and angle speeds; houses computed directly from ARMC | DIRECT | `houses_ex2`, `houses_armc` | SRC. NEW |
| F-E06 | House-system registry (letter, name, latitude limits, needs-Sun flag) | PLUMBING | `house_name` | DESIGN. Letter `i` naming differs between `project.md` and third-party lists (see report) |

### F. Phenomena, apsides, eclipses

| ID | Capability | Class | Candidate pyswisseph name | Verification and notes |
|---|---|---|---|---|
| F-F01 | Phase angle, illuminated fraction, elongation, apparent diameter, magnitude | DIRECT | `pheno_ut` | DOC. Moon age is not returned |
| F-F02 | Nodes and apsides of planets and Moon: mean, osculating, barycentric-osculating, second focal point | DIRECT | `nod_aps_ut` | DOC |
| F-F03 | Solar eclipses: global search, local circumstances, attributes, location of maximum | DIRECT | `sol_eclipse_when_glob`, `_when_loc`, `_how`, `_where` | DOC. Times in UT. Saros series and member returned only "if available". Umbra/penumbra limits and some times not implemented |
| F-F04 | Lunar eclipses: search, local circumstances, attributes | DIRECT | `lun_eclipse_when`, `_when_loc`, `_how` | DOC. Moon azimuth/altitude in `_how` not implemented |
| F-F05 | Lunar occultations of planets and stars | DIRECT | `lun_occult_when_glob`, `_when_loc`, `_where` | DOC. One-try flag prevents endless search |
| F-F06 | Heliacal rising/setting, visibility limit, heliacal details | DIRECT | `heliacal_ut`, `vis_limit_mag`, `heliacal_pheno_ut` | TOC + SRC. Needs atmospheric and observer inputs |
| F-F07 | Planetary transits across the Sun (Mercury, Venus) | EVENT_SEARCH | built on F-H | DESIGN |
| F-F08 | Osculating orbital elements, orbital periods, synodic period, max/min distance | DIRECT | `get_orbital_elements`, `orbit_max_min_true_distance` | DOC. NEW. Useful to size search windows. Not for apsis positions |

### G. Fixed stars and special points

| ID | Capability | Class | Candidate pyswisseph name | Verification and notes |
|---|---|---|---|---|
| F-G01 | Fixed-star position by name, Bayer designation or index | DIRECT | `fixstar2_ut` | DOC. Needs `sefstars.txt`. New function has exact-match and `%` wildcard behaviour |
| F-G02 | Galactic Center | DIRECT | via F-G01 | DOC. Entry "Galactic Center,SgrA*" |
| F-G03 | Galactic pole and plane entries; galactic-equator points | DIRECT + DERIVED_FOUNDATION | F-G01 + F-C05 | DOC for catalogue entries. Equator points derived |
| F-G04 | Fixed-star magnitude | DIRECT | `fixstar2_mag` | DOC. NEW. Valid for year 2000 only |

### H. Event-search framework (owner-approved)

| ID | Capability | Class | Notes |
|---|---|---|---|
| F-H01 | Scalar root finder: scan, bracket, refine to tolerance | EVENT_SEARCH | DOC confirms the library has NO geocentric crossing function for planets other than Sun and Moon, so this is required |
| F-H02 | Circular quantity support (wrap at 360, targets at any multiple) | EVENT_SEARCH | Uses F-C06 |
| F-H03 | Extremum finder (stations, greatest elongation, declination extremes, apsides) | EVENT_SEARCH | |
| F-H04 | Interval builder: boolean state over time to start/end intervals | EVENT_SEARCH | |
| F-H05 | Native crossings: Sun, Moon, Moon through ecliptic (true node), heliocentric planets | DIRECT | `solcross_ut`, `mooncross_ut`, `mooncross_node_ut`, `helio_cross_ut`. DOC. Sun/Moon forward-only; error is signalled by a returned time earlier than the start; precision 1 milliarcsecond; documented flags exclude sidereal (TEST) |
| F-H06 | Multi-body relative functions (difference, sum, midpoint) as search inputs | DERIVED_FOUNDATION | |
| F-H07 | Search behaviours: repeated crossings, retrograde loops, tangent contacts, no-event windows, step-size safety | EVENT_SEARCH | |
| F-H08 | Event result contract: UTC time, bracket, tolerance, direction, classification, diagnostics | PLUMBING | Field names deferred |

Constraint: D-015 (no caching) applies.

### I. Configuration, state, metadata

| ID | Capability | Class | Notes |
|---|---|---|---|
| F-I01 | Calculation profile separate from feature request | PLUMBING | |
| F-I02 | Request validation, compatibility rules, policy for irrelevant settings | PLUMBING | The library silently drops or zeroes many invalid combinations; project-side validation is mandatory (report section 5) |
| F-I03 | Isolation of library global state: ephemeris path, sidereal mode, topocentric position | PLUMBING | DOC for global setters. Community report says sidereal mode is per-thread in the binding (TEST). Library is not thread-safe per binding authors (COMM). Default policy: single-threaded, set state before every request |
| F-I04 | Result provenance metadata | PLUMBING | Schema deferred |
| F-I05 | Error and warning model | PLUMBING | pyswisseph raises `swisseph.Error` on fatal errors and does not return the warning string, so fallback to Moshier must be detected from the returned flags. Rise/set uses return codes; crossings use a time earlier than the start |
| F-I06 | Direct vs derived tagging on every output | PLUMBING | `project.md` primary goal |
| F-I07 | Version capture: library, binding, data-file coverage | PLUMBING | `version`, `get_current_file_data` DOC |
| F-I08 | Data-file manifest per capability and time range | PLUMBING | NEW. Planet, moon, asteroid files in 600-year blocks; star, orbital-element, asteroid-name, delta-T and leap-second text files; `ast*` and `sat` folders |

## 4. Traceability to dependency document layer 1

| Dependency doc section | Foundation capabilities |
|---|---|
| 1.1 Time values and zodiac offset | F-A02, F-A04, F-A05, F-A06, F-A10 |
| 1.2 Body positions | F-B01 to F-B15, F-C01 to F-C03 |
| 1.3 Fixed stars and galactic points | F-G01 to F-G04 |
| 1.4 Houses and angles | F-E01 to F-E06 |
| 1.5 Horizontal coordinates | F-D02 |
| 1.6 Rise, set, transit | F-D03, F-D05 |
| 1.7 Planetary phenomena | F-F01 |
| 1.8 Nodes and apsides | F-F02 |
| 1.9 Eclipses and occultations | F-F03 to F-F05 |
| 1.10 Heliacal events | F-F06 |
| 1.11 Crossing searches | F-H05 |
| Layer 5 | F-H01 to F-H08 |

**Correction to the dependency document:** it says Sankranti (Sun crossing a sidereal longitude) is returned directly by the library. The official crossing documentation lists no sidereal flag. Treat Sankranti as `EVENT_SEARCH` on a sidereal longitude unless probe P-11 shows the native function handles it.

## 5. Western needs checklist

Present in the foundation for Western even though Vedic does not need them: heliocentric and barycentric frames (F-C01), all house systems and Gauquelin sectors (F-E), fixed stars and galactic points (F-G), asteroids, centaurs, hypothetical bodies (F-B09 to F-B11), planetary nodes and apsides (F-F02), phenomena (F-F01), occultations (F-F05), heliacal events (F-F06), declination for parallels (F-B03), harmonics and midpoints (F-C06, F-H06), interpolated apogee (F-B07).

## 6. Review changes from v0.1

- Added: F-A10, F-B12 to F-B15, F-D05, F-E05, F-E06, F-F08, F-G04, F-I08.
- Corrected: F-H05 scope and the Sankranti note; F-I03 and F-I05 (binding behaviour); F-D02 azimuth convention; F-E01 polar-latitude failures; F-C04 limits of the subtraction method; F-B07 interpolated apogee.
- Added verification labels to every row.

## 7. Open foundation questions

| ID | Question | Owner input? |
|---|---|---|
| Q-F1 | Canonical raw longitude: tropical plus separate transform, or sidereal per call. The transform is only valid for the traditional method | No. Decide after probes |
| Q-F2 | Event search accepts any foundation quantity, including topocentric and horizontal values. Recommended yes | No |
| Q-F3 | Bar timestamp convention and event-to-bar mapping | Later (IA-012) |
| Q-F4 | Scope of extended asteroids, moons, hypothetical bodies; data files and licence | Later |
| Q-F5 | Policy for combinations the library computes but `project.md` marks invalid (heliocentric Moon, heliocentric sidereal) | No. Resolved by D-022 (allowed as experimental) |

## 8. Next steps

1. Owner runs the probe script and returns its output.
2. Update `TEST` rows with results.
3. Expand each `F-` capability with `FEATURE_SPECIFICATION_TEMPLATE.md`.
4. Map each Vedic feature (V-*) to F- capabilities; record gaps as new F- IDs.