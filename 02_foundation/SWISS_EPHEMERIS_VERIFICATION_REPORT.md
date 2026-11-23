# Swiss Ephemeris and pyswisseph Verification Report (IA-011)

**Date:** 2026-11-12 (documentation); runtime probes added 2026-11-23. **Phase:** documentation and runtime probes complete for the foundation scope; remaining items in the register section 9.
**Labels:** `SOURCE_CONFIRMED`, `AI_INFERENCE`, `NEEDS_RESEARCH`, `CONFLICTING_SOURCES`, `TECHNICALLY_UNSUPPORTED` as defined in `PROJECT_AUTHORITY_AND_SOURCE_POLICY.md`.

## 1. Method and limits

- Read: official Swiss Ephemeris programmer documentation (`swephprg.htm`) from the start through refraction (about half the document), its full contents list, official ephemeris file naming, the pyswisseph and pysweph PyPI pages and docs, binding source excerpts, and `swehouse.c` excerpts.
- Not read in full: the sections after refraction (heliacal, date/time functions, topocentric setter, sidereal mode detail, houses, house position, sidereal time). For these, existence is confirmed from the official contents list and binding source; parameters are marked `TOC` or `SRC` in the register.
- The AI ran no code (its sandbox has no network access). The owner ran the probe script on 2026-11-23 (Windows, Python 3.12.10, pyswisseph 2.10.3.2, Swiss Ephemeris 2.10.03, Moshier ephemeris). Results are in section 6A.

## 2. Binding status (Q-004)

| Item | Finding | Label |
|---|---|---|
| pyswisseph latest release | 2.10.3.2, released 2023-06-04 | SOURCE_CONFIRMED (PyPI) |
| Wrapped library | Swiss Ephemeris 2.10.03 | SOURCE_CONFIRMED |
| Prebuilt wheels on PyPI | Earlier finding: CPython 3.6 to 3.11 only. **Contradicted by the probe machine:** it loaded `swisseph.cp312-win_amd64.pyd` on Python 3.12.10, so either a cp312 wheel exists or the package was built locally. Unresolved, see Q-013 | CONFLICTING_SOURCES |
| Project status | PyPI classifier "Alpha". Fork maintainer states the original documentation site went offline in mid-2025 and the maintainer is unresponsive | SOURCE_CONFIRMED for classifier; CLAIM by fork maintainer for the rest |
| Fork `pysweph` | Drop-in, same `import swisseph`, versions 2.10.3.3 to at least 2.10.3.6 (Feb 2026), wheels for CPython 3.13. Breaking changes: `calc`, `calc_ut`, `calc_pctr`, `deltat_ex` also return the error string; `houses` family returns 13 or 37 item tuples with an empty index 0 | SOURCE_CONFIRMED |
| Binding error behaviour (pyswisseph) | Raises `swisseph.Error` on fatal errors; the warning string is not returned (the fork says pyswisseph "attempted to hide" C-style errors) | SOURCE_CONFIRMED (binding source, migration guide) |
| Functions exposed | `fixstar2_ut`, `fixstar2_mag`, `heliacal_ut`, `helio_cross`, `helio_cross_ut`, `house_pos`, `house_name`, `solcross`, `mooncross`, `mooncross_node` (and `_ut` forms) appear in the binding source and manual | SOURCE_CONFIRMED |

**Owner decision stands:** `pyswisseph` only (D-018). The Python version (D-021 says 3.11) is under review because the probe ran on 3.12.10. See Q-013.

## 3. Licensing (Q-005)

- Official statement: Swiss Ephemeris is dual-licensed, AGPL or the Swiss Ephemeris Professional License. The choice must be made before distributing software that contains it and before any public service using it is activated. Choosing AGPL obliges the developer to place the whole software project under AGPL or a compatible licence. `SOURCE_CONFIRMED`.
- pyswisseph and pysweph are both licensed AGPL v3. `SOURCE_CONFIRMED`.
- Consequence for the stated "Windows OR Web OR Both" goal: any distribution or web service triggers the choice. Private research use without distribution or public service is the stated low-obligation case in the official text. This is a summary of the licence text, not legal advice.

## 4. Confirmed library behaviours that shape the foundation

| Topic | Finding | Label |
|---|---|---|
| No flags | Apparent geocentric ecliptic position of date | SOURCE_CONFIRMED |
| Fallback | Missing Swiss files cause silent fallback to Moshier with a warning in the error string; the returned flags show which ephemeris was used | SOURCE_CONFIRMED |
| Fatal error | Return `-1`, position and speed set to zero | SOURCE_CONFIRMED |
| Flag removal | Sidereal adds no-nutation (P-03a) and heliocentric adds no-aberration and no-deflection (P-03b): confirmed. Documentation says topocentric is dropped when combined with heliocentric or barycentric, but P-03c shows the HELIOCENTRIC flag is dropped and a topocentric position is returned | PARTLY CONTRADICTED by probe |
| Heliocentric | Computed for all planets including the Moon. Sun, lunar nodes, lunar apogees return zeros and NO error | SOURCE_CONFIRMED |
| Barycentric | "Not completely implemented". Swiss and JPL only (not Moshier); physical bodies only; zeros for nodes and apogees; barycentric Sun accuracy 0.1 arcsecond | SOURCE_CONFIRMED |
| Sidereal default | If `set_sid_mode` is not called, Fagan/Bradley is used | SOURCE_CONFIRMED |
| Sidereal user mode | Reference epoch is TT unless the UT bit is set; ayanamsha at epoch = tropical minus sidereal position | SOURCE_CONFIRMED |
| Crossings | Functions exist for Sun, Moon, Moon through ecliptic, heliocentric planets. "There are currently no functions for geocentric crossings of other planets." Introduced in 2.10.02 | SOURCE_CONFIRMED |
| Hindu sunrise | Official documentation defines it (disc centre, no refraction, geocentric, no ecliptic latitude) and provides a dedicated flag | SOURCE_CONFIRMED |
| Azimuth | Measured from the south point to the west | SOURCE_CONFIRMED |
| Houses | Placidus, Koch, Gauquelin cannot be computed beyond the polar circle; Porphyry is returned with an error code; Sunshine can also fail | SOURCE_CONFIRMED (official text quoted in third-party source; consistent with `swehouse.c`) |
| Body limits | Chiron not computable before 650 CE or after 4650 CE; Pholus before 3850 BCE; Apollo before 1870 CE | SOURCE_CONFIRMED |
| Data files | 600-year blocks. `sepl`, `semo`, `seas` for CE; `seplm`, `semom`, `seasm` for BCE. `seas` holds Ceres, Pallas, Vesta, Juno, Chiron, Pholus. Moshier needs no files, covers 3000 BCE to 3000 CE at about 1 arcsecond | SOURCE_CONFIRMED |
| Sidereal state per thread | A user issue (measured with pyswisseph 2.10.03 on 2026-11-07) reports sidereal mode is per-thread, so other threads fall back to Fagan/Bradley | CONFIRMED by probe P-10 |

## 5. Audit of `project.md`

### 5.1 Section B.12 behaviour table (17 rows)

| # | Row | Verdict | Notes |
|---|---|---|---|
| 1 | No frame flag = geocentric | CONFIRMED | |
| 2 | No equatorial flag = ecliptic | CONFIRMED | |
| 3 | Equatorial flag = RA/Dec | CONFIRMED | With sidereal modes the equinox reference differs |
| 4 | Sidereal without `set_sid_mode` = Fagan/Bradley | CONFIRMED | Matches the note |
| 5 | Topocentric without `set_topo` uses stale or default values silently | UNVERIFIED | The probe had already set the position earlier in the process (P-03c), so the default state was not tested. Policy stands: call `set_topo` before every topocentric request |
| 6 | Topocentric + ayanamsha valid | NOT TESTED | No restriction found in the documentation |
| 7 | Topocentric + house system valid | VACUOUS | House functions take latitude and longitude directly and ignore the frame flag |
| 8 | Topocentric without altitude invalid | PROJECT POLICY | The API takes altitude as an argument and zero is accepted. "Required" is a project rule, not an API rule |
| 9, 10 | Geocentric + ayanamsha / houses valid | CONFIRMED | |
| 11 | Heliocentric + ayanamsha INVALID | **CONTRADICTED by P-07** | Works; the offset equals the Lahiri ayanamsha (24.198 degrees). Matches rows 5 and 12 of matrix C.4. Allowed as experimental (D-022) |
| 12 | Heliocentric + houses invalid | PROJECT POLICY, reasonable | Houses depend on time and observer only |
| 13 | Heliocentric + location invalid | CONSISTENT IN INTENT, DIFFERENT MECHANISM | P-03c: the library drops the heliocentric flag and returns a topocentric geocentric position, with no error. Project must reject the combination |
| 14 | Heliocentric Moon invalid | **CONTRADICTED (docs and P-05)** | Returned longitude 270.58, distance 1.019 AU. Allowed as experimental (D-022) |
| 15 | Heliocentric nodes/apsides: flag ignored | PARTLY WRONG (P-05) | Confirmed: the library returns zeros with no error. Project validation must catch this |
| 16 | Heliocentric Sun undefined | CONFIRMED (P-05) | Returns zeros with no error |
| 17 | Vedic mode + outer planets allowed | CONFIRMED | Trivial |

### 5.2 Other findings in `project.md`

| Section | Finding | Severity |
|---|---|---|
| A.1 file table | Describes `seplmXX`, `semomXX`, `seasmXX` as "mean elements / lower precision". Official naming: the `m` marks BCE files; all files are 600-year blocks of the same precision. `seas` covers only six main asteroids | Error, fix |
| B.5 ayanamsha list | 48 entries including user-defined. P-12 confirms 47 predefined modes (0 to 46) with names; mode 255 is user-defined. The Python constant names in `project.md` were not individually checked | Partly confirmed |
| B.6 house letters | Consistent with third-party lists except letter `i`: third parties name it "Sunshine alternative (Makransky)"; `project.md` says "Sunshine / Altitude". Official letter table not retrieved | Check |
| B.7 "equal types" | Lists `Y` (APC) and `X` (axial rotation / meridian) as equal-house systems. Third-party descriptions do not support that | Check |
| B.10 / B.11 | `LilithMean` description says "Osculating apogee" (copy error). Interpolated apogee and perigee bodies exist in the library but are missing | Fix, add |
| B.11 | Uranus, Neptune, Pluto labelled "Tropical Astro Only", while C.4 row 17 and the Vedic outer-planet feature allow them in Vedic mode | Internal conflict |
| C.4 matrix | No barycentric rows at all, though C.3 defines the frame and library support is partial | Gap |
| C.4 row 4 | Says the Moon's position varies "1° to 2°" between cities. P-04: geocentric vs Mumbai 0.90°, Mumbai vs New York 1.54°. The claim is SUPPORTED; the AI's earlier doubt was wrong | Confirmed |
| C.5 | Lists Moon, nodes and Lilith as geocentric/topocentric only. True for nodes and apogees (zeros otherwise). Not true for the Moon | Conflicts with B.12 row 14 |
| Input schema `nutation` | Sidereal calculations force no-nutation, so the toggle has no effect in sidereal mode | Add rule |
| Input schema | `include_horizontal` needs observer location; barycentric needs Swiss or JPL ephemeris | Add rules |

### 5.3 Validation rules the project must own (library will not enforce them)

1. Reject sun, nodes, apogees with heliocentric or barycentric frames (library returns zeros silently).
2. Reject observer location with heliocentric or barycentric frames (P-03c: the library silently drops the heliocentric flag and returns a topocentric position).
3. Reject barycentric with the Moshier ephemeris and for non-physical bodies.
4. Never rely on the library default zodiac or ayanamsha. Always set sidereal mode explicitly per request.
5. Compare returned flags with requested flags on every call and record differences.
6. Check each body against its coverage window before the call.
7. Sidereal mode is per-thread (P-10). Set sidereal mode and topocentric position in the calling thread before every request.

## 6. Runtime probes (run `verification/verify_swisseph_probe.py`)

| Probe | Question | Settles |
|---|---|---|
| P-01 | Environment: Python, library and binding versions | Q-013 |
| P-02 | Default sidereal with no mode set | B.12 row 4 |
| P-03 | Flags returned for sidereal, heliocentric, topocentric+heliocentric | F-B04, F-C01 |
| P-04 | Topocentric Moon before and after `set_topo`; size of shift | B.12 rows 5, 6; C.4 row 4 |
| P-05 | Heliocentric Moon, Sun, nodes, apogees | B.12 rows 14 to 16 |
| P-06 | Barycentric under Moshier | C.3, F-C01 |
| P-07 | Heliocentric + sidereal | B.12 row 11 |
| P-08 | Swiss requested with no files: fallback flags | F-I05 |
| P-09 | Houses at polar latitude for Placidus, Koch, Porphyry, Whole Sign, Gauquelin | F-E01 |
| P-10 | Sidereal mode set on main thread, used on worker thread | F-I03 |
| P-11 | `solcross_ut` with and without the sidereal flag | F-H05, Sankranti |
| P-12 | Ayanamsha names for modes 0 to 59 and 255 | B.5 |
| P-13 | Rise with Hindu flag; circumpolar return | F-D03, F-D05 |
| P-14 | Azimuth convention at local noon | F-D02 |
| P-15 | `pheno_ut`, `helio_cross_ut`, `mooncross_node_ut`, `fixstar2_ut` calls and signatures | F-F01, F-H05, F-G01 |

## 6A. Probe results (2026-11-23)

Environment (P-01): Windows 64-bit, Python 3.12.10, `swisseph.cp312-win_amd64.pyd`, binding version 20230604 (pyswisseph 2.10.3.2), Swiss Ephemeris 2.10.03.

| Probe | Result |
|---|---|
| P-02 | Default sidereal offset 25.08 degrees: Fagan/Bradley is used when no mode is set. Confirmed |
| P-03 | Sidereal adds no-nutation. Heliocentric adds no-aberration and no-deflection. Topocentric + heliocentric returns topocentric flags only: the heliocentric flag is dropped silently |
| P-04 | Moon shift from geocentric: Mumbai 53.9 arcmin, New York 38.5 arcmin; Mumbai vs New York 92.4 arcmin. Default-state question not settled |
| P-05 | Heliocentric Moon computed. Sun, both nodes, both apogees return zeros, no error. Confirmed |
| P-06 | Barycentric under Moshier raises "barycentric Moshier positions are not supported" for Sun, Mars and node |
| P-07 | Heliocentric + sidereal works; offset equals the ayanamsha |
| P-08 | Requesting Swiss without data files silently uses Moshier; the returned flags show it; result has two items |
| P-09 | At 80 degrees latitude Placidus, Koch and Gauquelin raise an error; Porphyry and Whole Sign work; 12 cusps, 8 angles |
| P-10 | Sidereal mode is per-thread: worker thread used Fagan/Bradley. Confirmed |
| P-11 | `solcross_ut` honours the sidereal flag (Mesha crossing 2024-04-13 about 15:34 UT; sidereal Sun 359.99999999992). Confirmed |
| P-12 | Modes 0 to 46 have names (47 predefined); 47 and above, and 255, return empty names |
| P-13 | Hindu sunrise at Mumbai 00:35:49 UT vs astronomical 00:31:59 UT (about 3.8 minutes later). Polar winter sunrise returns code `-2` |
| P-14 | Azimuth 359.06 with the Sun at 61.9 degrees altitude near noon: measured from the south. Confirmed |
| P-15 | `pheno_ut` returns five values; `helio_cross_ut` returns a JD; `mooncross_node_ut` returns (JD, lon, lat); `fixstar2_ut` failed only because `sefstars.txt` is absent |

## 7. Decisions needed from the owner

| ID | Decision | Recommendation |
|---|---|---|
| Q-013 | Target Python version. REOPENED: the probe ran on 3.12.10 | Keep 3.11 per D-021 or switch to 3.12; run the wheel check in `CURRENT_PROGRESS.md` first |
| Q-017 | RESOLVED by D-022. Allow heliocentric Moon and heliocentric sidereal as experimental valid combinations | Allow both, flagged experimental, since the library computes them and D-003 forbids omitting valid experimental combinations |
| Q-005 | Licence route before any distribution or web service | Decide later; keep local use until then |