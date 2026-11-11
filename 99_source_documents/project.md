# Project Details:
Design a financial astrology data generator library which is easily plugable, portable and extandable which can be used with Windows OR Web OR Both application.

## 1. Core Primary Goals:
  - For given date time range or specific date time and the timeframe (Any like 1min, 5 min , 1 day or week etc), it must generate the raw astronomical data with the help of swiss ephemeris python package (pyswisseph).
  - Data generated needs to be differentiated like directly generated data and derived data which is calculated from the generated one.
  - The generation code and how to store the generated/calculated data will be the 2nd phase of this project.
  - Library must generate it based on the various inputs (decided by secondary goals) by making sure that the combinations of those inputs are valid.

## 2. Secondary Goals:
  - The data generation support for western as well vedic astrology features.
  - We want to generate or use the generated data for the astrology features which can be directly or indirectly associated with time axis of the stock chart data timeframe.
  - For examples but not limited too.
    - query various types of astronomical data for given datetime range and check how was the stock behiour in that range.
    - query when a planet enters to specific sign, house, nakshatras, entry exit points, relationship between the planets like degrees, angels, aspects, punchangs?
    - query the speed, angles, motion of the planets of specific period or datetime or in range?
    - query the astronomical data w.r.t given geolocation + date + time like position at the time of birth chart and then match/cross check with current planet positions/relation to check the stock behaviour.


# Skills required for project:
	1. Software design, architecture, development.
	2. pyswissephe / Swiss Ephemeries (Astronomy)
	3. Western Astrology
	4. Indian Vedic Astrology
	5. Financial astrology
	6. W. D. Gann Teachings and all the techniques around it available on the internet.


# Important things to crosscheck before you answer each time:
1. Skip all the formalities. Do not answer unless asked.
2. Do not assume. Ask if unclear.
3. This is not actual implementation. Only scoping and design.
4. Our project covers Western and Vedic astrology. Also keep W. D. Gann Techings too in mind. We will go through them one by one.
5. Do NOT Exclude any Western + Vedic feature combination which is valid in terms of expermental research.
6. As in future we will be extending or using W. D. Gann Teachings as well so need to keep that in mind.
7. Most important, DO NOT SKIP OR IGNORE any feature available in the Western (modern) or Vedica astrology.
8. This project is strictly specific to financial astrology research purpose to find pattern based on the historical stock chart data over TIME and figuring out future repeatation of those pattern.
9. Following sections are for the reference purpose.


# Section A: Swiss Ephemeris Package / Library Details:

## A.1 (swisseph) Core C Language Implementation Of Swiss Ephemeris Library:
- [Documentation](https://www.astro.com/ftp/swisseph/doc/swisseph.htm)
- [Programing interface to the swiss ephemeris](https://www.astro.com/ftp/swisseph/doc/swephprg.htm)
- [Library Source Code](https://github.com/aloistr/swisseph)
- [Ephemeris Data Files](https://github.com/aloistr/swisseph/tree/master/ephe)

| File Name Pattern  | What it Contains                              | Details                                                                 |
|--------------------|-----------------------------------------------|-------------------------------------------------------------------------| 
| seplmXX.se1        | Planetary Positions, Mean Elements            | Lower precision planetary ephemeris; fast to calculate                  | 
| sepl_XX.se1        | Planetary Positions, High Precision           | Higher precision planetary data (better for astrological calculations)  | 
| semomXX.se1        | Moon Positions, Mean Motion                   | Lower precision lunar motion ephemeris                                  | 
| semo_XX.se1        | Moon Positions, High Precision                | Very high precision lunar data (important because Moon moves fast)      | 
| seasmXX.se1        | Asteroid/Small Body Positions, Mean Elements  | Lower precision asteroid/small body data                                | 
| seas_XX.se1        | Asteroid/Small Body Positions, High Precision | High precision asteroid/small body data                                 |


## A.2 Python packages implementation over core C library of swiss ephemeris
- [pyswisseph](https://pypi.org/project/pyswisseph/): Not maintained.
- [pysweph](https://pypi.org/project/pysweph/): New fork with ongoing community maintenance.
  - [Official Documentation](https://sailorfe.github.io/pysweph/installation.html)


## A.3 Additional details Or resources for reference
- [astro.com](https://www.astro.com/swisseph/swephinfo_e.htm)
- [horoscopes.astro-seek.com](https://horoscopes.astro-seek.com/)
  - It uses "Lahiri 1940" ayanmasa for generating ephemeris when you select (Sidereal-Lahari) on UI.
  - It displays the position within the SIGN when Degrees option selected as : "Degs Mins'"
  - When you select Degrees option as : "ABS Degs", it will match your calculation return by your program.


# Section B: Constants Defined In pyswisseph for Swiss Ephemeris:

## B.1. Types Of Swiss Ephemeris

| SN | Ephemeris Type    | swe constant   |
|----|-------------------|----------------|
| 1  | Swiss Ephemeris   | swe.FLG_SWIEPH |
| 2  | Moshier Ephemeris | swe.FLG_MOSEPH |
| 3  | JPL Ephemeris     | swe.FLG_JPLEPH |


## B.2. Types Of Zodiac System

| SN   | Zodiac System Type | swe constant     |
|------|--------------------|------------------|
| 1    | Tropical           | swe.FLG_TROPICAL |
| 2    | Sidereal           | swe.FLG_SIDEREAL |


## B.3. Types Of Calendars

| SN | Calendar Type | swe constant |
|----|---------------|--------------|
| 1  | Gregorian     | swe.GREG_CAL |
| 2  | Julian        | swe.JUL_CAL  |


## B.4. Types Of Coordinate Systems / Reference Frames

| SN | Reference Frame | swe constant            |
|----|-----------------|-------------------------|
| 1  | Geocentric      | Default. No Flag Passed |
| 2  | Topocentric     | swe.FLG_TOPOCTR         |
| 3  | Heliocentric    | swe.FLG_HELCTR          |
| 4  | Barycentric     | swe.FLG_BARYCTR         |


## B.5. Types Of Ayanamsha Types

| SN | Ayanamsha Type                   | swe constant                  |
|----|----------------------------------|-------------------------------|
| 1  | Aryabhata                        | swe.SIDM_ARYABHATA            |
| 2  | Aryabhata 522                    | swe.SIDM_ARYABHATA_522        |
| 3  | Aryabhata MSUN                   | swe.SIDM_ARYABHATA_MSUN       |
| 4  | Bhasin                           | swe.SIDM_JN_BHASIN            |
| 5  | Krishnamurti                     | swe.SIDM_KRISHNAMURTI         |
| 6  | Krishnamurti VP291               | swe.SIDM_KRISHNAMURTI_VP291   |
| 7  | Lahiri                           | swe.SIDM_LAHIRI               |
| 8  | Lahiri 1940                      | swe.SIDM_LAHIRI_1940          |
| 9  | Lahiri ICRC                      | swe.SIDM_LAHIRI_ICRC          |
| 10 | Lahiri VP285                     | swe.SIDM_LAHIRI_VP285         |
| 11 | Raman                            | swe.SIDM_RAMAN                |
| 12 | Sassanian                        | swe.SIDM_SASSANIAN            |
| 13 | Suryasiddhanta                   | swe.SIDM_SURYASIDDHANTA       |
| 14 | Suryasiddhanta MSUN              | swe.SIDM_SURYASIDDHANTA_MSUN  |
| 15 | True Citra                       | swe.SIDM_TRUE_CITRA           |
| 16 | True Mula                        | swe.SIDM_TRUE_MULA            |
| 17 | True Pushya                      | swe.SIDM_TRUE_PUSHYA          |
| 18 | True Revati                      | swe.SIDM_TRUE_REVATI          |
| 19 | True Sheoran                     | swe.SIDM_TRUE_SHEORAN         |
| 20 | Ushashashi                       | swe.SIDM_USHASHASHI           |
| 21 | Yukteshwar                       | swe.SIDM_YUKTESHWAR           |
| 22 | DeLuce                           | swe.SIDM_DELUCE               |
| 23 | Djwhal Khul                      | swe.SIDM_DJWHAL_KHUL          |
| 24 | Fagan Bradley                    | swe.SIDM_FAGAN_BRADLEY        |
| 25 | Valens Moon                      | swe.SIDM_VALENS_MOON          |
| 26 | Citra (SS)                       | swe.SIDM_SS_CITRA             |
| 27 | Revati (SS)                      | swe.SIDM_SS_REVATI            |
| 28 | User Defined                     | swe.SIDM_USER                 |
| 29 | Aldebaran 15° Taurus             | swe.SIDM_ALDEBARAN_15TAU      |
| 30 | B1950                            | swe.SIDM_B1950                |
| 31 | J1900                            | swe.SIDM_J1900                |
| 32 | J2000                            | swe.SIDM_J2000                |
| 33 | Galactic Align (Mardyks)         | swe.SIDM_GALALIGN_MARDYKS     |
| 34 | Galactic Center (0° Sagittarius) | swe.SIDM_GALCENT_0SAG         |
| 35 | Galactic Center (Cochrane)       | swe.SIDM_GALCENT_COCHRANE     |
| 36 | Galactic Center (Mula Wilhelm)   | swe.SIDM_GALCENT_MULA_WILHELM |
| 37 | Galactic Center (Gilbrand)       | swe.SIDM_GALCENT_RGILBRAND    |
| 38 | Galactic Equator (Fiorenza)      | swe.SIDM_GALEQU_FIORENZA      |
| 39 | Galactic Equator (IAU1958)       | swe.SIDM_GALEQU_IAU1958       |
| 40 | Galactic Equator (Mula)          | swe.SIDM_GALEQU_MULA          |
| 41 | Galactic Equator (True)          | swe.SIDM_GALEQU_TRUE          |
| 42 | Babylonian (Britton)             | swe.SIDM_BABYL_BRITTON        |
| 43 | Babylonian (ETPSC)               | swe.SIDM_BABYL_ETPSC          |
| 44 | Babylonian (Huber)               | swe.SIDM_BABYL_HUBER          |
| 45 | Babylonian (Kugler1)             | swe.SIDM_BABYL_KUGLER1        |
| 46 | Babylonian (Kugler2)             | swe.SIDM_BABYL_KUGLER2        |
| 47 | Babylonian (Kugler3)             | swe.SIDM_BABYL_KUGLER3        |
| 48 | Hipparchos                       | swe.SIDM_HIPPARCHOS           |


## B.6. Types Of House Systems

| SN | House System Type                | swe constant |
|----|----------------------------------|--------------|
| 1  | APC Houses                       | b"Y"         |
| 2  | Axial Rotation / Meridian Houses | b"X"         |
| 3  | Equal_A                          | b"A"         |
| 4  | Equal / 1 = Aries                | b"N"         |
| 5  | Equal_E                          | b"E"         |
| 6  | Equal (MC)                       | b"D"         |
| 7  | Equal / Vehlow                   | b"V"         |
| 8  | Equal / Whole Sign               | b"W"         |
| 9  | Alcabitius                       | b"B"         |
| 10 | Campanus                         | b"C"         |
| 11 | Carter Poli-equatorial           | b"F"         |
| 12 | Gauquelin Sectors                | b"G"         |
| 13 | Horizon / Azimuth                | b"H"         |
| 14 | Koch                             | b"K"         |
| 15 | Krusinski-Pisa-Goelzer           | b"U"         |
| 16 | Morinus                          | b"M"         |
| 17 | Placidus                         | b"P"         |
| 18 | Polich/Page                      | b"T"         |
| 19 | Porphyry                         | b"O"         |
| 20 | Pullen SD                        | b"L"         |
| 21 | Pullen SR                        | b"Q"         |
| 22 | Regiomontanus                    | b"R"         |
| 23 | Savard-A                         | b"J"         |
| 24 | Sripati                          | b"S"         |
| 25 | Sunshine                         | b"I"         |
| 26 | Sunshine / Altitude              | b"i"         |


## B.7. Types Of Equal House Systems

| SN | Equal Type House Systems         | swe constant |
|----|----------------------------------|--------------|
| 1  | APC Houses                       | b"Y"         |
| 2  | Axial Rotation / Meridian Houses | b"X"         |
| 3  | Equal_A                          | b"A"         |
| 4  | Equal / 1 = Aries                | b"N"         |
| 5  | Equal_E                          | b"E"         |
| 6  | Equal (MC)                       | b"D"         |
| 7  | Equal / Vehlow                   | b"V"         |
| 8  | Equal / Whole Sign               | b"W"         |


## B.8. Types Of Planet Positions

| SN | Planet Position Type | swe constant                                  |
|----|----------------------|-----------------------------------------------|
| 1  | Apparent             | NA - If Selected do not set "swe.FLG_TRUEPOS" |
| 2  | TRUE                 | swe.FLG_TRUEPOS                               |


## B.9. Types Of Lunar Nodes

| SN | Lunar Node Type | swe constant  |
|----|-----------------|---------------|
| 1  | MEAN            | swe.MEAN_NODE |
| 2  | TRUE            | swe.TRUE_NODE |


## B.10. Types Of Lilith Nodes

| SN | Lilith Node Type | swe constant  |
|----|------------------|---------------|
| 1  | MEAN             | swe.MEAN_APOG |
| 2  | TRUE             | swe.OSCU_APOG |


## B.11. Planets

| SN | Name       | Constant                      | Unicode | Unicode Image | Description                                                                                     |
|----|------------|-------------------------------|---------|---------------|-------------------------------------------------------------------------------------------------|
| 1  | Earth      | swe.EARTH                     | \u2295  | ⊕             | Traditional Planet - पृथ्वी                                                                     |
| 2  | Sun        | swe.SUN                       | \u2609  | ☉             | Traditional Planet - सूर्य (Surya) / Ravi (रवि)                                                 |
| 3  | Moon       | swe.MOON                      | \u263D  | ☽             | Traditional Planet - चंद्र (Chandra) / Soma (सोम)                                               |
| 4  | Mercury    | swe.MERCURY                   | \u263F  | ☿             | Traditional Planet - बुध (Budh)                                                                 |
| 5  | Venus      | swe.VENUS                     | \u2640  | ♀             | Traditional Planet - शुक्र (Shukra) / भृगु (सकाळचा तारा - Bhrigu)                               |
| 6  | Mars       | swe.MARS                      | \u2642  | ♂             | Traditional Planet - मंगळ (Mangal) / Kuja (कुज) / अंगारक (Aangarak)                             |
| 7  | Jupiter    | swe.JUPITER                   | \u2643  | ♃             | Traditional Planet - गुरु (Guru) / Brihaspati (बृहस्पति)                                        |
| 8  | Saturn     | swe.SATURN                    | \u2644  | ♄             | Traditional Planet - शनि (Shani)                                                                |
| 9  | RahuTrue   | swe.TRUE_NODE                 | \u260A  | ☊             | Vedic Only / Shadow Planets - Rahu (राहू) - North Lunar Node / Dragon's Head / Ascending Node   |
| 10 | RahuMean   | swe.MEAN_NODE                 | \u260A  | ☊             | Vedic Only / Shadow Planets - Rahu (राहू) - North Lunar Node / Dragon's Head / Ascending Node   |
| 11 | KetuTrue   | NA - Calculate From Rahu True | \u260B  | ☋             | Vedic Only / Shadow Planets - Ketu (केतू) - South Lunar Node / Dragon's Tail / Descending Node  |
| 12 | KetuMean   | NA - Calculate From Rahu Mean | \u260B  | ☋             | Vedic Only / Shadow Planets - Ketu (केतू) - South Lunar Node / Dragon's Tail / Descending Node  |
| 13 | Uranus     | swe.URANUS                    | \u2645  | ♅             | Tropical Astro Only - युरेनस, इंद्र, प्रजापती, हर्षल                                            |
| 14 | Neptune    | swe.NEPTUNE                   | \u2646  | ♆             | Tropical Astro Only - नेपच्यून, Varuna (वरुण), Greek god of ocean                               |
| 15 | Pluto      | swe.PLUTO                     | \u2647  | ♇             | Tropical Astro Only - प्लूटो, रुद्र, यम                                                         |
| 16 | LilithMean | swe.MEAN_APOG                 | \u26B8  | ⚸             | Lunar apogee / Lilith - Osculating apogee                                                       |
| 17 | LilithTrue | swe.OSCU_APOG                 | \u26B8  | ⚸             | Lunar apogee / Lilith - Osculating apogee                                                       |
| 18 | Chiron     | swe.CHIRON                    | \u26B7  | ⚷             | Minor planet / centaur                                                                          |
| 19 | Ceres      | swe.CERES                     | \u26B3  | ⚳             | Main-belt asteroids                                                                             |
| 20 | Pallas     | swe.PALLAS                    | \u26B4  | ⚴             | Main-belt asteroids                                                                             |
| 21 | Juno       | swe.JUNO                      | \u26B5  | ⚵             | Main-belt asteroids                                                                             |
| 22 | Vesta      | swe.VESTA                     | \u26B6  | ⚶             | Main-belt asteroids                                                                             |


## B.12. pyswisseph code behaviour / Validation

| SN | Situation                                                                           | Behaviour                                                                                    |
|----|-------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------|
| 1  | swe.calc_ut() without any `reference frame` flag                                    | No Error. Default is `Geocentric`                                                            |
| 2  | swe.calc_ut() if `equatorial` flag not given                                        | No Error. Default positions are ecliptic.                                                    |
| 3  | swe.calc_ut() if `equatorial` flag given                                            | No Error. Returns equatorial positions - RA/Dec instead of ecliptic lon/lat.                 |
| 4  | Passing `Sidereal` Flag Without Calling `swe_set_sid_mode()`                        | No error. Silently defaults to Fagan-Bradley ayanamsa.                                       |
| 5  | Passing `Topocentric` Flag Without Calling `swe_set_topo()`                         | No error. Uses default/previous topo values (0,0,0 or stale), giving wrong results silently. |
| 6  | `Topocentric` +  `Ayanamsha`                                                        | Valid                                                                                        |
| 7  | `Topocentric` +  `House System`                                                     | Valid                                                                                        |
| 8  | `Topocentric` +  No Altitude                                                        | Invalid. altitude required for topocentric corrections                                       |
| 9  | `Geocentric` + `Ayanamsha`                                                          | Valid                                                                                        |
| 10 | `Geocentric` + `House System`                                                       | Valid                                                                                        |
| 11 | `Heliocentric` + `Ayanamsha`                                                        | Invalid                                                                                      |
| 12 | `Heliocentric` +  `House System`                                                    | Invalid. houses UNDEFINED without a geocentric horizon                                       |
| 13 | `Heliocentric` + `Location`                                                         | Invalid. heliocentric frame does not use observer location                                   |
| 14 | `Heliocentric` + Planetary body as `Moon`                                           | Invalid. Moon has no heliocentric position                                                   |
| 15 | `Heliocentric` + `Lunar Nodes/Apsides`                                              | Invalid. Flag effectively ignored — nodes are Earth-Moon geometry, not heliocentric objects. |
| 16 | `Heliocentric` + Planetary body as `SUN`                                            | Invalid. Sun is the center, so its own heliocentric position is undefined.                   |
| 17 | `astrology_mode`=`vedic` + body ∈ {`Uranus`, `Neptune`, `Pluto`, `Uranian points`}  | Allowed.                                                                                     |


# Section C: Input Schema, Details, Validation

## C.1. Astrology Modes:
### 1. **Western:**
If selected then data needs to be generated only for Western Astrology supported features/functionality.
### 2. **Vedic:**
If selected then data needs to be generated only for Indian Vedic Astrology supported features/functionality.

## C.2. Zodiac Systems
- Zodiac system is a way we define the sky's coordinate map.
- `Because of a slow wobble in Earth's axis called precession, these two systems have drifted apart by about 24 degrees over time, causing them to show different sign placements for the same birth date.`
- They are different because around 2,000 years ago, the two systems perfectly overlapped. On the March Equinox, the Sun was physically entering the constellation of Aries.
- However, because Earth wobbles on its axis like a spinning top, the position of the stars relative to our equinoxes shifts backward by about 1 degree every 72 years.
- Today, on the March Equinox, the Sun physically rises in the constellation of Pisces, not Aries. The Tropical system still calls this day 0° Aries (because it's the start of spring). The Sidereal system accurately tracks it as Pisces.
- This is why your Sidereal sign is usually one full sign backward from your Tropical sign.

### 1. **Tropical:**
- It is based on Earths relationship to the sun. (Seasons and Solstices)
- This system locks 0° of Aries to the March Equinox (the start of Spring in the Northern Hemisphere).
- It completely ignores where the actual physical stars are. Instead, it divides the Sun’s yearly path into 12 equal 30-degree segments based purely on seasonal shifts.
- Does not account for *precession (slow wobble in Earth's axis)*. The zodiac moves with earth's seasons.
- A persons sign alignment is tide to birth month's season.

### 2. **Sidereal:**
- It is based on the Earth's relationship to the fixed/actual stars (constellations).
- This system aligns 0° of Aries with the actual physical constellation of Aries in the night sky.
- It accounts for precession.
- A persons sign alignment is tide to persons astronomical position of sky at the time of birth.
- Because Earth wobbles over thousands of years, the dates when the Sun passes through the real constellations change slightly every year.
- Sidereal astrology uses a calculation called an ayanamsa to shift the zodiac map and keep it aligned with the real stars.

## C.3. Reference Frame Types / Coordinate Systems:
These represents point of origin (Center) used when measuring positions, distance or orbits in space. Basically what object you are observing and from where.
 
### 1. **Geocentric:**
   - Calculations are based on considering Earth as center.
### 2. **Heliocentric:**
   - Calculations are based on considering Sun as center.
### 3. **Topocentric:**
   - Calculations are based on considering Earth as center and from specific geolocation on the Earth.
   - It means if used then it must be used in combination of Geocentric reference frame.
### 4. **Barycentric:**
   - Calculations are based on *Center of mass of the Solar system*, the barycenter rather than solely focusing on the Sun (heliocentric) or the Earth (geocentric).

## C.4. Configuration Combination Compatibility Matrix:
| SN | Astrology Mode | Zodiac System | Reference Frame | Is Location Required ?                 | Retrograde Applicable? | Is Combination Valid? | Do We Need to Implement? | Comments                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
|----|----------------|---------------|-----------------|----------------------------------------|------------------------|-----------------------|--------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 1  | Western        | Tropical      | Geocentric      | Not Applicable                         | YES                    | YES                   | YES                      | Valid Combination                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| 2  | Western        | Tropical      | Topocentric     | **Mandatory Geo Location Coordinates** | YES                    | YES                   | YES                      | Valid Combination                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| 3  | Western        | Sidereal      | Geocentric      | Not Applicable                         | YES                    | YES                   | YES                      | Valid Combination                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| 4  | Western        | Sidereal      | Topocentric     | **Mandatory Geo Location Coordinates** | YES                    | YES                   | YES                      | **Not Recommended.** Introduces localized surface coordinates to a fixed-star framework, adding unnecessary geometric noise to global asset backtesting.<br><br>Topocentric calculations introduce a variable known as parallax, which mathematically shifts a planet's apparent position depending on where you stand on Earth.<br><br>This shift is massive for the Moon (varying up to 1° to 2° of longitude depending on whether you calculate from New York or Tokyo).<br><br>For example, if you backtest a localized strategy based on the Moon hitting a precise sidereal degree, your algorithm will flash a trading signal at a completely different time in London than it will in New York.                                                                                                                                                                                                                                                                                                                        |
| 5  | Western        | Sidereal      | Heliocentric    | Not Applicable                         | **NO**                 | YES                   | YES                      | 1. **Hermetic Astrology:** Championed by modern researchers like Robert Powell, Hermetic Astrology explicitly integrates heliocentric planetary charts mapped onto the sidereal zodiac. It is used to look at the ""cosmic"" or mystical evolution of the soul, stripped of Earth-bound ego.<br><br>2. **Financial & Market Astrologers:** The Ultimate Gann Wheel Tool (Price-to-Degree Conversions). Traders who use astrology to forecast financial markets (such as Barry William Rosen or those following W.D. Gann's underlying principles) frequently use a heliocentric sidereal timing framework. They track the true, un-refracted orbital periods and angles of the planets against the fixed stars to predict long-term economic cycles.<br><br>3. **Esoteric / Galactic Astrology:** Astrologers tracking deep-space alignments (like a planet aligning with the Galactic Center or distant stars) prefer this combination. It provides a map of the solar system as an objective unit moving through the galaxy. |
| 6  | Western        | Tropical      | Heliocentric    | Not Applicable                         | **NO**                 | **NO**                | **NO**                   | It is mathematically valid as a data-fetching command in the Swiss Ephemeris, but it is conceptually flawed.<br>Measuring planetary longitudes from the center of the Sun using a coordinate grid anchored to Earth's atmospheric seasons creates a hybrid framework with no basis in physical astronomy or classical astrological theory.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| 7  | Vedic          | Sidereal      | Geocentric      | Not Applicable                         | YES                    | YES                   | YES                      | Absolute gold standard and default framework for traditional Indian Astrological science.<br>Valid Standard Combination                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| 8  | Vedic          | Sidereal      | Topocentric     | **Mandatory Geo Location Coordinates** | YES                    | YES                   | YES                      | Highly Valid for Intraday Nifty/Sensex Models.<br>Topocentric most effective for moon                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| 9  | Vedic          | Tropical      | Geocentric      | Not Applicable                         | YES                    | **NO**                | **NO**                   | NON standard. Experimental Only. No Ayanamsha, No Dashsa.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| 10 | Vedic          | Tropical      | Topocentric     | **Mandatory Geo Location Coordinates** | YES                    | **NO**                | **NO**                   | **INVALID**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| 11 | Vedic          | Tropical      | Heliocentric    | Not Applicable                         | **NO**                 | **NO**                | **NO**                   | **INVALID**<br>Reason: Vedic technique is fundamentally Moon-centric (panchanga, nakshatra timing, dashas all depend on the Moon), and the Moon has no heliocentric position, period - already enforced by helio_no_moon, unrelated to zodiac choice)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| 12 | Vedic          | Sidereal      | Heliocentric    | Not Applicable                         | **NO**                 | YES                   | YES                      | If we are running a quantitative backtest, this combination is incredibly powerful,<br>but it must be used for price and structural cycle modeling rather than traditional Vedic timing.<br><br>**The Ultimate Tool for Price-to-Degree Wheel Conversions:** Quantitative traders map these linear degrees directly onto price charts (e.g., Gann Wheels). For instance, if Heliocentric Sidereal Jupiter hits 135°, an algorithmic model checks for immediate support, resistance, or a trend vector at ₹135, ₹270, ₹540, or their exact harmonic fractions in an asset's price history                                                                                                                                                                                                                                                                                                                                                                                                                                       |


###### C.5. Planetary Calculations Only Valid For Geocentric / Topocentric Reference Frame:
- Moon
- Rahu  (Mean/True) / North Lunar Node / Dragon's Head / Ascending Node
- Ketu  (Mean/True) / South Lunar Node / Dragon's Tail / Descending Node
- Lilith (Mean/True)

#### Section D: Application UI must support the following parameters as input.


## 3. Input Schema

| Input Parameters From UI | Possible Values                                                                                                                                                                                                                                                                                            | Type                                                                      | Notes                                                                                                                                                                                              |
|--------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `astrology_mode`         | `Western` or `Vedic`                                                                                                                                                                                                                                                                                       | TBD                                                                       | Drives sensible defaults only; does not restrict cross-access to bodies/systems                                                                                                                    |
| `timezone`               | `Asia/Kolkata`                                                                                                                                                                                                                                                                                             | TBD                                                                       | Predefined world markets and their timezone list.                                                                                                                                                  |
| `datetime_start`         | `datetime(2026, 8, 1, 0, 0, tzinfo=ZoneInfo("Asia/Kolkata"))`                                                                                                                                                                                                                                              | local datetime + IANA timezone                                            | Convert internally to UT/Julian Day.<br>Start date of the range to fetch the data.<br>e.g. Inception Or listing date of stock.                                                                     |
| `datetime_end`           | **Optional.** `datetime(2026, 12, 31, 0, 0, tzinfo=ZoneInfo("Asia/Kolkata"))`                                                                                                                                                                                                                              | local datetime + IANA timezone                                            | Convert internally to UT/Julian Day.<br>If not given then current date is the end date of range<br>Omit for single-point query                                                                     |
| `interval`               | `1m, 5m, 10m, 15m, 1h, 4h, 1d, 1w, 1mo`                                                                                                                                                                                                                                                                    | list of string or enum (TBD)                                              | As per section #TODO                                                                                                                                                                               |
| `calendar`               | `Gregorian` Or `Julian`                                                                                                                                                                                                                                                                                    | TBD                                                                       | Default: `Gregorian`.<br>Julian for historical pre-1582 dates                                                                                                                                      |
| `location`               | <pre>GeoLocation(<br>&emsp;&emsp;country="India",<br>&emsp;&emsp;city="Mumbai",<br>&emsp;&emsp;longitude=72.53,<br>&emsp;&emsp;long_direction="East",<br>&emsp;&emsp;latitude=19.04,<br>&emsp;&emsp;lat_direction="North",<br>&emsp;&emsp;altitude_m=10,<br>&emsp;&emsp;timezone="Asia/Kolkata"<br>)</pre> | Object Or Dict Or TBD                                                     | Required for Geocentric / Topocentric calculations, Houses, Rise/Set.<br>Forbidden for Heliocentric<br>Can be a predefined set of locations as per the global markets and their exchange locations |
| `reference_frame`        | `Geocentric`, `Topocentric`, `Heliocentric`, `Barycentric`                                                                                                                                                                                                                                                 | TBD                                                                       |                                                                                                                                                                                                    |
| `zodiac`                 | `Tropical`, `Sidereal`                                                                                                                                                                                                                                                                                     | TBD                                                                       | It must be independent of `astrology_mode` as we will use sidereal with `western` mode too for experimental purpose                                                                                |
| `ayanamsha`              | REQUIRED ONLY IF `Zodiac` is `Sidereal`.<br>See point B.5 from Section B                                                                                                                                                                                                                                   | TBD                                                                       | Keep default `Lahiri`                                                                                                                                                                              |
| `house_system_code`      | FORBIDDEN FOR `Heliocentric` REFERENCE FRAME.<br>See point B.6 from Section B                                                                                                                                                                                                                              | TBD                                                                       | default **Whole Sign** for both modes                                                                                                                                                              |
| `bodies`                 | See point B.11 from Section B                                                                                                                                                                                                                                                                              | TBD. Signle Or List of pyswisseph constants for required planetary bodies |                                                                                                                                                                                                    |
| `nutation`               | `True` Or `False`                                                                                                                                                                                                                                                                                          | Boolean                                                                   | Apply/omit nutation correction                                                                                                                                                                     |
| `position_type`          | `Apparent` Or `TRUE`                                                                                                                                                                                                                                                                                       | TBD                                                                       |                                                                                                                                                                                                    |
| `lunar_node_type`        | See point B.9 from Section B                                                                                                                                                                                                                                                                               | TBD                                                                       |                                                                                                                                                                                                    |
| `lilith_node_type`       | See point B.10 from Section B                                                                                                                                                                                                                                                                              | TBD                                                                       |                                                                                                                                                                                                    |
| `include_equatorial`     | `True` Or `False`                                                                                                                                                                                                                                                                                          | Boolean                                                                   | In addition to default swe.calc_ut() ecliptic positions generate equatorial RA/Dec positions too                                                                                                   |
| `include_horizontal`     | `True` Or `False`                                                                                                                                                                                                                                                                                          | Boolean                                                                   | To include horizontal positions                                                                                                                                                                    |
| `output_format`          | TBD from - `CSV`, `Json`, `Parquet`, `DuckDB`, `Dataframe` etc                                                                                                                                                                                                                                             | TBD                                                                       |                                                                                                                                                                                                    |
