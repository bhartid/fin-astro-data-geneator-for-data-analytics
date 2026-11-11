# Features Sequenced by Dependency, and Western and Vedic Comparison

This document does two things with the list of Western and Vedic astrology features that can be placed on a time axis:

1. **Part 1** groups the features and puts them in order of dependency. The features that the Swiss Ephemeris library (through its Python package pysweph) calculates directly come first. Everything calculated afterwards from those results follows, each layer needing only the layers before it.
2. **Part 2** compares the two traditions feature by feature, to separate what is common to both from what belongs to only one.

## Terms used

| Term | Meaning |
|---|---|
| Calculated directly by the library | The value or exact moment is returned by a library function. It is stored exactly as returned. |
| Derived | Calculated afterwards from values that already exist, using our own rules and tables. |
| Birth or inception chart | The chart of a person, company or instrument at its starting moment. |
| Mixed feature | A feature whose current-state part and event part sit in different layers. It appears in both layers, with a note saying which part belongs where. |

# Part 1: Features in order of dependency

## The order at a glance

| Order | Layer | What it holds | Needs |
|---|---|---|---|
| 0 | Fixed reference tables | Fixed reference tables | Nothing |
| 1 | Calculated directly by the library (pysweph) | Values and exact moments returned directly by the library | The moment in time, the location and the settings |
| 2 | Derived at each moment from layer 1 values and fixed tables | Per-moment values derived from positions, from sunrise and sunset, and from houses | Layer 1 values and fixed tables, for the same moment |
| 3 | Relationships between bodies at each moment | Aspects, conjunctions, drishti and other relationships | Layer 2 values compared with each other |
| 4 | Conditions, strengths and combinations at each moment | Dignities, strengths, yogas, doshas, chakras and indices | Layers 2 and 3 with fixed tables |
| 5 | Exact moments and periods found by searching through time | Exact moments and periods found by searching | Layers 1 to 4 evaluated repeatedly across time |
| 6 | Calendar structures and charts at event moments | Calendar structures and charts at event moments | Exact moments from layer 5, and layers 1 to 4 at those moments |
| 7 | Features that need a birth or inception chart | Dashas, progressions, returns and annual charts | A birth or inception chart plus the passing of time |
| 8 | Comparison of a birth or inception chart with later moments or other charts | Transits against a chart and chart-to-chart comparisons | A birth or inception chart plus a later moment or a second chart |

The inputs behind every layer are the moment in time (converted to a Julian day), the observer location, and the settings: zodiac (tropical or sidereal), ayanamsha, reference frame (geocentric, heliocentric, barycentric or topocentric), house system and position type (true or apparent). 

## Layer 0. Fixed reference tables

Depends on nothing. These tables are read by the later layers.

### Fixed tables

No calculation. Fixed values that give meaning to the later layers.

| Feature | Marathi name (Vedic features) | Tradition | Note |
|---|---|---|---|
| Natural significations | नैसर्गिक कारकत्व | Vedic |  |
| Nakshatra attributes | नक्षत्र गुणधर्म (गण, योनी, नाडी, वर्ण) | Vedic |  |
| Static lookup tables | कोष्टके | Vedic |  |

## Layer 1. Calculated directly by the library (pysweph)

Depends only on the moment in time, the observer location and the settings (zodiac, ayanamsha, reference frame, house system, position type). Each result is stored exactly as the library returns it. Function names are those of the Swiss Ephemeris library as exposed by pysweph and must be confirmed against the installed version.

### 1.1 Time-related values and the zodiac offset

Library functions: equation of time; sidereal time; ayanamsha value. (Julian day and delta T conversions are supporting calculations.) Returns: the equation of time in days; the sidereal time in hours; the ayanamsha in degrees.

| Feature | Marathi name (Vedic features) | Tradition | Note |
|---|---|---|---|
| Equation of time | — | Western |  |
| Sidereal time | — | Western |  |
| Ayanamsha value | — | Western | Returned directly by the library for the ayanamsha chosen. It supports every sidereal feature. |
| Ayanamsha value | अयनांश | Vedic | Same value as the Western entry; it supports every sidereal feature. |

### 1.2 Body positions

Library function: the body position calculation (one call per body and moment, with flags for tropical or sidereal, geocentric, heliocentric, barycentric or topocentric, ecliptic or equatorial, true or apparent). Returns, for each call: longitude (or right ascension), latitude (or declination), distance, and the speed in each of the three, plus the flags actually used and any message text.

| Feature | Marathi name (Vedic features) | Tradition | Note |
|---|---|---|---|
| Ecliptic longitude | — | Western |  |
| Ecliptic latitude | — | Western |  |
| Distance | — | Western |  |
| Speed | — | Western |  |
| Right ascension | — | Western |  |
| Declination | — | Western |  |
| Heliocentric coordinates | — | Western |  |
| Barycentric coordinates | — | Western |  |
| Topocentric coordinates | — | Western |  |
| Planetary position (Navagraha) | ग्रह स्फुट / ग्रहस्थिती (नवग्रह) | Vedic | Ketu is not returned by the library. It is calculated as the point opposite Rahu (Rahu plus 180 degrees). |
| Outer planets | हर्षल (अरुण), नेपच्यून (वरुण), प्लूटो (यम) | Vedic |  |
| Lunar nodes | — | Western | Mean and true node are separate library bodies. The south node is the point opposite the north node. |
| Lilith (lunar apogee) | — | Western | Mean apogee and osculating (true) apogee are separate library bodies. |
| Chiron and Pholus | — | Western |  |
| Main asteroids | — | Western |  |
| Further asteroids and distant bodies | — | Western | Needs the extended asteroid data files. |
| Uranian (Hamburg School) hypothetical points | — | Western | The library provides these hypothetical bodies from an orbital elements file. |

### 1.3 Fixed stars and galactic points

Library function: the fixed star position calculation. Returns the position of a named star with the same values as the body positions.

| Feature | Marathi name (Vedic features) | Tradition | Note |
|---|---|---|---|
| Fixed stars | — | Western |  |
| Galactic points | — | Western | Only the Galactic Center position comes directly from the library (as a star). Points defined by the galactic equator come from a coordinate conversion and belong to layer 2. |

### 1.4 Houses and angles

Library functions: the houses calculation and the house position calculation. Returns: all house cusps (12 for most systems, 36 for the Gauquelin sectors), the Gauquelin sector of a body, the Ascendant, Midheaven, sidereal time at the Midheaven, Vertex, equatorial ascendant, the two co-ascendants and the polar ascendant; and the house number of a body.

| Feature | Marathi name (Vedic features) | Tradition | Note |
|---|---|---|---|
| Ascendant and Descendant | — | Western |  |
| Midheaven and IC | — | Western |  |
| Other angles | — | Western |  |
| House cusps | — | Western |  |
| Lagna (Ascendant) | लग्न | Vedic |  |
| Houses | भाव | Vedic | Whole-sign and equal houses follow directly from the Lagna; the other systems are returned by the library. |
| Planets in houses | — | Western | The library returns the house number of a body directly. It can also be worked out from the cusps (layer 2). |
| Graha in bhava | ग्रह भाव स्थिती | Vedic | Same as above; with whole-sign houses it is simply the sign counted from the Lagna. |
| Gauquelin sectors | — | Western | Returned directly by the library (the Gauquelin sector of a body, or the 36 sector boundaries from the houses calculation). |
| Position within a house | — | Western | Returned directly by the library as the house position of a body, a number with a fraction. |

### 1.5 Horizontal coordinates

Library function: the azimuth and altitude conversion. Returns: azimuth, true altitude and apparent altitude of a body for an observer.

| Feature | Marathi name (Vedic features) | Tradition | Note |
|---|---|---|---|
| Azimuth and altitude | — | Western |  |

### 1.6 Rise, set and meridian crossing

Library function: the rise and set calculation. Returns: the moment of rising, setting, upper and lower meridian crossing, and twilight events for a body and an observer.

| Feature | Marathi name (Vedic features) | Tradition | Note |
|---|---|---|---|
| Rise, set and twilight | — | Western |  |
| Sunrise, sunset, moonrise, moonset | सूर्योदय / सूर्यास्त / चंद्रोदय / चंद्रास्त | Vedic |  |

### 1.7 Planetary phenomena

Library function: the planetary phenomena calculation. Returns: phase angle, illuminated fraction, elongation from the Sun, apparent diameter and apparent magnitude.

| Feature | Marathi name (Vedic features) | Tradition | Note |
|---|---|---|---|
| Planetary phenomena | — | Western |  |
| Moon phase | — | Western | Phase angle and illuminated fraction come directly from the library. Moon age is calculated in layer 2. |

### 1.8 Nodes and apsides of planets

Library function: the nodes and apsides calculation. Returns: positions of the ascending node, descending node, perihelion and aphelion of a body.

| Feature | Marathi name (Vedic features) | Tradition | Note |
|---|---|---|---|
| Planetary nodes and apsides | — | Western | Nodes and apsides of the planets. The Moon is available as a body (nodes and apogee) in the positions group. |

### 1.9 Eclipses and occultations

Library functions: the global and local solar eclipse searches, the lunar eclipse searches, the eclipse attribute calculations and the lunar occultation searches. Returns: the moment of each contact, the eclipse type, magnitude, obscuration and (where available) the series number.

| Feature | Marathi name (Vedic features) | Tradition | Note |
|---|---|---|---|
| Solar eclipses | — | Western | Global and local circumstances, contact times and magnitude come directly from the library. |
| Lunar eclipses | — | Western | Same as above. |
| Occultations | — | Western | The library finds occultations by the Moon. |
| Eclipses | सूर्य ग्रहण / चंद्र ग्रहण | Vedic | Same data as the Western eclipses. Visibility from a location uses the library local-circumstances function. |

### 1.10 Heliacal events

Library functions: the heliacal event calculation and the visibility limit calculation. Returns: the moment of heliacal rising or setting for a body, an observer and given atmospheric conditions.

| Feature | Marathi name (Vedic features) | Tradition | Note |
|---|---|---|---|
| Greatest elongations and heliacal events | — | Western | Only heliacal rising and setting come from the library here. Greatest elongations are found by searching in layer 5. |

### 1.11 Crossing searches

Library functions: the Sun crossing search, the Moon crossing search, the Moon node crossing search and the heliocentric planet crossing search. Returns: the exact moment the body reaches a given longitude.

| Feature | Marathi name (Vedic features) | Tradition | Note |
|---|---|---|---|
| Cardinal points | — | Western | The Sun crossing 0, 90, 180 and 270 degrees of the tropical zodiac. |
| Sankranti | संक्रांती | Vedic | The library finds the exact moment the Sun crosses a given longitude, using the sidereal zodiac. |
| Sign ingress | — | Western | Only the part the library returns directly is here: Sun and Moon crossings, and heliocentric planet crossings. Ingress of the other planets is in layer 5. |
| Sign ingress | राशी प्रवेश | Vedic | Same as above: Sun and Moon crossings are direct; the other grahas are in layer 5. |

## Layer 2. Derived at each moment from layer 1 values and fixed tables

Each result is calculated from values already available for that same moment. No searching through time is needed.

### 2A. From body positions only

Needs only the position values from layer 1, the chosen zodiac and ayanamsha, and the fixed tables. No observer location is needed.

| Feature | Marathi name (Vedic features) | Tradition | Note |
|---|---|---|---|
| Sign and degree | — | Western |  |
| Sign (Rashi) of each graha | राशी | Vedic |  |
| Sign lord and star lord | राशी स्वामी / नक्षत्र स्वामी | Vedic |  |
| Nakshatra and Pada | नक्षत्र आणि चरण | Vedic |  |
| Sun's nakshatra | सूर्य नक्षत्र (पावसाचे नक्षत्र) | Vedic |  |
| Ritu and Ayana | ऋतू / अयन (उत्तरायण, दक्षिणायन) | Vedic | Season and half-year from the Sun position. |
| Decans (faces) | — | Western |  |
| Terms (bounds) | — | Western |  |
| Dodecatemoria | — | Western |  |
| Critical degrees | — | Western |  |
| Harmonic positions | — | Western |  |
| Out of bounds | — | Western | Current state here (declination compared with the Sun maximum). Start and end moments are in layer 5. |
| Retrograde and direct | — | Western | Current state here (sign of the speed). Stationary points are in layer 5. |
| Retrograde and direct | वक्री / मार्गी | Vedic | Current state here. Stationary points and period boundaries are in layer 5. |
| Speed class | — | Western |  |
| Speed and fast transits | गती / अतिचारी | Vedic | Current speed here. Fast-transit events are in layer 5. |
| Element and modality balance | — | Western |  |
| Oriental and occidental | — | Western |  |
| Antiscia and contra-antiscia | — | Western |  |
| Vargottama | वर्गोत्तम | Vedic | Compares the sign in the first divisional chart (Rashi) with the sign in the ninth (Navamsha). |
| Pushkara navamsha and bhaga | पुष्कर नवांश / पुष्कर भाग | Vedic |  |
| Gandanta | गंडांत | Vedic |  |
| Mrityu bhaga and sandhi | मृत्यू भाग / संधी | Vedic |  |
| Chara karakas | चर कारक | Vedic |  |
| Rahu-Ketu hemming | कालसर्प स्थिती | Vedic |  |
| Moon and Sun as lagna | चंद्र लग्न / सूर्य लग्न | Vedic |  |
| Shodashavarga: sixteen divisional charts | षोडशवर्ग | Vedic |  |
| Extended vargas | विस्तारित वर्ग | Vedic |  |
| Lunar mansions | — | Western |  |
| Star lord, sub lord, sub-sub lord | नक्षत्र स्वामी / उप-स्वामी / उप-उप स्वामी | Vedic | Looked up from the longitude in the table of 249 unequal sub-divisions. |
| Tithi | तिथी | Vedic | Moon minus Sun longitude divided into 30 parts. Start and end moments (spans) are in layer 5. |
| Paksha | पक्ष | Vedic |  |
| Yoga (Nitya yoga) | योग | Vedic | Sun plus Moon longitude divided into 27 parts. Spans are in layer 5. |
| Karana | करण | Vedic | Half-tithi parts. Spans are in layer 5. |
| Lunation cycle phase | — | Western |  |

### 2B. From positions plus sunrise and sunset

Needs the sunrise and sunset from layer 1.6 and the weekday.

| Feature | Marathi name (Vedic features) | Tradition | Note |
|---|---|---|---|
| Vara | वार | Vedic | The Vedic day starts at sunrise, so the weekday needs the sunrise time. |
| Day and night length | दिनमान / रात्रिमान | Vedic |  |
| Ghatika and pala | घटिका / पळ | Vedic |  |
| Hora | होरा | Vedic |  |
| Choghadiya | चौघडिया | Vedic |  |
| Inauspicious periods | राहुकाळ / यमगंड / गुलिक काळ | Vedic |  |
| Auspicious muhurtas | अभिजित मुहूर्त / ब्रह्म मुहूर्त | Vedic |  |
| Further muhurta periods | दुर्मुहूर्त / वर्ज्य / अमृत काळ | Vedic |  |
| Planetary day and hour rulers | — | Western |  |
| Disha Shoola | दिशाशूल | Vedic |  |

### 2C. From positions plus houses and angles

Needs positions from layer 1.2 and the houses and angles from layer 1.4, so an observer location is needed.

| Feature | Marathi name (Vedic features) | Tradition | Note |
|---|---|---|---|
| Bhava Chalit | भाव चलित | Vedic |  |
| Bhava madhya and sandhi | भाव मध्य / संधी | Vedic |  |
| House lords | भावेश | Vedic |  |
| House rulers | — | Western |  |
| House types | केंद्र / त्रिकोण / दुःस्थान | Vedic |  |
| Hemisphere and quadrant emphasis | — | Western |  |
| Sect | — | Western |  |
| Special lagnas | विशेष लग्न | Vedic |  |
| Arudha padas | आरूढ पदे | Vedic |  |
| Upagrahas | उपग्रह | Vedic | Gulika and Mandi positions come from the Lagna at a segment of the day; this needs sunrise, sunset and the houses. |
| Sahams | सहम | Vedic |  |
| Sensitive points | भृगू बिंदू / योगी-अवयोगी / प्राणपद | Vedic |  |
| Lots and Arabic parts | — | Western | Needs the angles, the positions and whether it is a day or night chart. |
| Cusp sub lords | भाव उप-स्वामी | Vedic | Needs the house cusps and the sub-division table. |
| Ruling planets | रुलिंग प्लॅनेट्स | Vedic | Needs the Lagna and the weekday. |
| Angular, succedent and cadent houses | — | Western | Worked out from the house a body occupies: angular for houses 1, 4, 7 and 10; succedent for 2, 5, 8 and 11; cadent for 3, 6, 9 and 12. |

## Layer 3. Relationships between bodies at each moment

Compares two or more layer 2 values with each other (angles between bodies, shared signs, adjacent signs).

### Relationships

Needs layer 2 values for the bodies being compared.

| Feature | Marathi name (Vedic features) | Tradition | Note |
|---|---|---|---|
| Major aspects | — | Western |  |
| Minor aspects | — | Western |  |
| Aspects to angles and cusps | — | Western |  |
| Parallels and contra-parallels | — | Western |  |
| Midpoints | — | Western |  |
| Midpoint trees and 90-degree dial | — | Western |  |
| Mutual reception | — | Western |  |
| Parivartana | परिवर्तन | Vedic |  |
| Graha drishti | ग्रह दृष्टी | Vedic |  |
| Rashi drishti | राशी दृष्टी | Vedic |  |
| Conjunction | युती | Vedic |  |
| Argala | अर्गला / विरोधार्गला | Vedic |  |
| Geometric aspects in the sidereal zodiac | कोनात्मक दृष्टी (सायन/निरयन) | Vedic |  |
| Planetary war | ग्रहयुद्ध | Vedic | Current state (two grahas within one degree) here. Period boundaries are in layer 5. |
| Combust, cazimi, under the beams | — | Western | Current state (distance from the Sun) here. Period boundaries are in layer 5. |
| Combustion and rising or setting | अस्त / उदय | Vedic | Current state here. Rising and setting periods are in layer 5. |
| Heliocentric aspects and ingresses | — | Western | Aspects seen from the Sun here. Heliocentric ingresses are in layer 5. |
| Kartari | पापकर्तरी / शुभकर्तरी | Vedic |  |

## Layer 4. Conditions, strengths and combinations at each moment

Combines layer 2 and layer 3 results with fixed tables to judge the condition of a body or a chart at that moment.

### Conditions and strengths

Needs layer 2 and layer 3 results and the fixed tables.

| Feature | Marathi name (Vedic features) | Tradition | Note |
|---|---|---|---|
| Essential dignities | — | Western |  |
| Detriment, fall, peregrine | — | Western |  |
| Dignity state | उच्च / नीच / स्वक्षेत्र / मूलत्रिकोण | Vedic |  |
| Planetary friendship | मित्र / शत्रू / सम (नैसर्गिक, तात्कालिक, पंचधा) | Vedic |  |
| Avasthas | अवस्था | Vedic |  |
| Accidental dignities | — | Western |  |
| Almuten and lords | — | Western |  |
| Vimshopaka bala | विंशोपक बल | Vedic |  |
| Shadbala | षड्बल | Vedic |  |
| Ishta and Kashta phala | इष्ट / कष्ट फल | Vedic |  |
| Bhava bala | भाव बल | Vedic |  |
| Ashtakavarga | अष्टकवर्ग | Vedic |  |

### Combinations, doshas and rule libraries

Needs layer 2 and layer 3 results evaluated against rules.

| Feature | Marathi name (Vedic features) | Tradition | Note |
|---|---|---|---|
| Aspect patterns | — | Western |  |
| Composite aspect indices | — | Western |  |
| Pancha Mahapurusha yogas | पंच महापुरुष योग | Vedic |  |
| Raja, Dhana and cancellation yogas | राजयोग / धनयोग / विपरीत राजयोग / नीचभंग | Vedic |  |
| Moon-based yogas | गजकेसरी / सुनफा / अनफा / दुरुधरा / केमद्रुम / अधी | Vedic |  |
| Sun-based yogas | बुधादित्य / वेशी / वाशी / उभयचरी | Vedic |  |
| Nabhasa yogas | नाभस योग | Vedic |  |
| Other classical yogas | इतर शास्त्रीय योग | Vedic |  |
| Dosha-type combinations | कालसर्प / गुरू चांडाल / ग्रहण / शापित / अंगारक / विष योग | Vedic |  |
| Mangal Dosha in a chart | मांगलिक दोष / मंगळ दोष | Vedic | Evaluated on any chart: the chart of a moment, or the birth or inception chart. |
| Mangal Dosha cancellation and strength | मंगळ दोष परिहार | Vedic |  |
| Kala Sarpa Dosha and its twelve types | कालसर्प दोष (अनंत, कुलिक, वासुकी, शंखपाल, पद्म, महापद्म, तक्षक, कर्कोटक, शंखचूड, घातक, विषधर, शेषनाग) | Vedic |  |
| Pitru Dosha | पितृ दोष | Vedic |  |
| Muhurta yogas | सर्वार्थ सिद्धी / अमृत सिद्धी / रविपुष्य / गुरुपुष्य / द्विपुष्कर / त्रिपुष्कर / व्यतिपात / वैधृती | Vedic |  |
| Inauspicious panchang combinations | कुयोग: दग्ध तिथी, रिक्ता तिथी, हुताशन योग, यमघंट योग, मृत्यू योग, क्रकच योग, विष योग | Vedic |  |
| Sarvatobhadra Chakra | सर्वतोभद्र चक्र | Vedic |  |
| Other chakras | सप्तशलाका / कोट / नवतारा / राहू चक्र | Vedic |  |
| Teji-Mandi rules | तेजी-मंदी | Vedic |  |
| Significators | भाव कारक | Vedic | Needs house lords, occupants and aspects. |

## Layer 5. Exact moments and periods found by searching through time

Needs layers 1 to 4 evaluated repeatedly across time and then narrowed to the exact moment. Where the library already returns an exact moment, that part is in layer 1.

### Events and periods of motion and position

Found by searching the positions and speeds of the bodies.

| Feature | Marathi name (Vedic features) | Tradition | Note |
|---|---|---|---|
| Earth and Moon apsides | — | Western | Moments of Earth perihelion and aphelion and of Moon perigee and apogee. |
| Angle sign changes | — | Western | Moments the Ascendant or Midheaven enters a new sign. |
| Angular transits | — | Western | Moments a body crosses the Ascendant, Midheaven, Descendant or IC. |
| Fixed-star parans | — | Western | Moments stars and planets rise, set or culminate together. |
| Sign ingress | — | Western | The Sun, Moon and heliocentric crossings are returned directly by the library (layer 1). This row is the ingress of the other planets, found by searching. |
| Sign ingress | राशी प्रवेश | Vedic | The Sun and Moon crossings are returned directly by the library (layer 1). This row is the sign ingress of the other grahas, found by searching. |
| Retrograde and direct | — | Western | Moments a planet becomes stationary (turns retrograde or direct). |
| Retrograde and direct | वक्री / मार्गी | Vedic | Moments a graha becomes stationary, and the boundaries of retrograde periods. |
| Retrograde periods and shadows | — | Western | Start and end of retrograde stretches and of the shadow periods before and after them. |
| Speed and fast transits | गती / अतिचारी | Vedic | Fast-transit events, for example a graha moving through a sign unusually quickly. |
| Out of bounds | — | Western | Start and end of the periods a body is out of bounds. |
| Combust, cazimi, under the beams | — | Western | Start and end of the periods a body is combust or under the beams. |
| Combustion and rising or setting | अस्त / उदय | Vedic | Start and end of the periods of combustion (Ast), and the moments of rising (Udaya) and setting. |
| Planetary war | ग्रहयुद्ध | Vedic | Start and end of the periods of planetary war. |
| Exact aspect times | — | Western | Moments an aspect becomes exact, including repeated exactness during retrograde motion. |
| Aspect windows | — | Western | Start and end of the stretch during which an aspect is within orb. |
| Heliocentric aspects and ingresses | — | Western | Moments a planet enters a new sign as seen from the Sun. |
| Nakshatra ingress | नक्षत्र प्रवेश | Vedic | Moments a graha enters a new nakshatra. |
| Varga sign changes | वर्ग राशी बदल | Vedic | Moments a graha changes sign in a divisional chart. The Moon changes its ninth-chart sign about every 6 hours. |
| Lagna changes | लग्न बदल | Vedic | Moments the Lagna sign or nakshatra changes (about every two hours). |
| Kakshya gochar | कक्ष्या गोचर | Vedic | Boundaries of the eight parts of each sign that a graha crosses. |
| Sub-lord changes | उप-स्वामी बदल | Vedic | Moments a graha changes its sub-lord (for the Moon, every few hours). |

### Lunar, planetary-cycle and eclipse-related events and periods

Found by searching the Sun and Moon relationship and the planetary geometry.

| Feature | Marathi name (Vedic features) | Tradition | Note |
|---|---|---|---|
| Principal lunar phases | — | Western | Moments of new, first quarter, full and last quarter Moon. |
| Void-of-course Moon | — | Western | From the Moon last major aspect until it enters the next sign. |
| Lunar declination extremes | — | Western | Moments of the Moon greatest north and south declination. |
| Eclipse seasons and series | — | Western | Windows when the Moon is near a node, and Saros and Inex series membership. |
| Planetary transits of the Sun | — | Western | Mercury and Venus crossing the disc of the Sun. |
| Greatest elongations and heliacal events | — | Western | Greatest elongations of Mercury and Venus (the heliacal events are returned directly by the library, layer 1). |
| Synodic cycles of body pairs | — | Western | Conjunction, opposition and quadrature moments of body pairs. |
| Great Conjunction series | — | Western | Jupiter-Saturn conjunctions and the periods of their element changes. |
| Planet-Sun relations | — | Western | Superior and inferior conjunctions, oppositions and quadratures with the Sun. |

### Panchang spans and nakshatra-based periods

Found by searching the Sun and Moon longitudes for the boundaries.

| Feature | Marathi name (Vedic features) | Tradition | Note |
|---|---|---|---|
| Tithi spans | तिथी कालावधी / क्षय-वृद्धी | Vedic | Start and end moments of each tithi. |
| Nakshatra spans | नक्षत्र कालावधी | Vedic | Start and end moments of each nakshatra of the Moon. |
| Yoga (Nitya yoga) | योग | Vedic | Start and end moments of each yoga. |
| Karana | करण | Vedic | Start and end moments of each karana. |
| Bhadra (Vishti) | भद्रा / विष्टी | Vedic | Periods of the Vishti karana. |
| Panchaka and Gand Mool | पंचक / गंडमूळ | Vedic | Periods when the Moon is in the Panchaka or Gand Mool nakshatras. |
| Visha Ghati | विषघटी | Vedic | Stretches within each nakshatra, found from the nakshatra boundaries. |
| Lattaa and Pata | लत्ता / पात | Vedic | Moments a graha reaches the nakshatra struck by the prescribed count. |

## Layer 6. Calendar structures and charts at event moments

Needs the exact moments from layer 5 and the layers 1 to 4 values at those moments.

### Calendar structures

Built from lunar month starts, new-year moments and daily rules.

| Feature | Marathi name (Vedic features) | Tradition | Note |
|---|---|---|---|
| Lunar month | मास (अमांत / पौर्णिमांत, अधिक मास, क्षय मास) | Vedic | Needs the new-moon moments and the Sun sign at those moments. |
| Samvatsara and eras | संवत्सर / विक्रम संवत / शके | Vedic | Needs the lunar new-year moment and the Jupiter cycle. |
| Festivals and vrata days | सण / व्रत | Vedic | Needs the tithi, lunar month and nakshatra rules for each day. |
| Sutak | सूतक | Vedic | Needs the eclipse contact times and the location. |

### Charts at moments

A chart cast for an exact moment.

| Feature | Marathi name (Vedic features) | Tradition | Note |
|---|---|---|---|
| Sankranti charts | संक्रांती कुंडली | Vedic | Chart cast at the moment of the Sun ingress. |
| Lunation and new-year charts | अमावस्या / पौर्णिमा / वर्षप्रतिपदा कुंडली | Vedic | Chart cast at the new Moon, full Moon or the lunar new year. |
| Chart at an instant (Prashna chart) | प्रश्न कुंडली | Vedic | Chart cast at any chosen moment; it holds the same values that exist at that instant in the lower layers. |
| Charts at event instants | — | Western | Chart cast at an ingress, lunation, eclipse or great conjunction. |

## Layer 7. Features that need a birth or inception chart

Needs the layers 1 to 4 values at the birth or inception moment, combined with the passing of time.

### Time-lord period systems and annual charts

Periods and annual charts counted from the birth or inception moment.

| Feature | Marathi name (Vedic features) | Tradition | Note |
|---|---|---|---|
| Vimshottari dasha | विंशोत्तरी दशा | Vedic | Starts from the Moon position in its nakshatra at the birth or inception moment. |
| Dasha lord changes | दशा बदल / दशा संधी | Vedic |  |
| Ashtottari dasha | अष्टोत्तरी दशा | Vedic |  |
| Yogini dasha | योगिनी दशा | Vedic |  |
| Chara dasha | चर दशा | Vedic |  |
| Kalachakra dasha | कालचक्र दशा | Vedic |  |
| Other sign-based dashas | इतर राशी दशा | Vedic |  |
| Other nakshatra-based dashas | इतर नक्षत्र दशा | Vedic |  |
| Dasha balance at the birth or inception moment | दशा शेष | Vedic | The part of the first dasha remaining at the birth or inception moment. |
| KP dasha-bhukti-antara | KP दशा-भुक्ती-अंतर | Vedic | Same method as Vimshottari, using the KP ayanamsha. |
| Maraka lords and Maraka periods | मारक ग्रह / मारक दशा | Vedic |  |
| Badhaka lord and Badhaka periods | बाधकेश / बाधक दशा | Vedic |  |
| Longevity calculation | आयुर्दाय (पिंडायू, अंशायू, नैसर्गिकायू) | Vedic |  |
| Karakamsha and Swamsha | कारकांश / स्वांश | Vedic |  |
| Varsha Pravesh | वर्ष प्रवेश | Vedic |  |
| Muntha and Varshesha | मुंथा / वर्षेश | Vedic |  |
| Mudda and Patyayini dasha | मुद्दा दशा / पात्यायनी दशा | Vedic |  |
| Tajika sahams | ताजिक सहम | Vedic |  |
| Tajika aspects | ताजिक दृष्टी (इत्थशाल, इशराफ) | Vedic |  |
| Annual and monthly profections | — | Western |  |
| Firdaria | — | Western |  |
| Zodiacal releasing | — | Western |  |
| Decennials | — | Western |  |

### Progressions, directions and returns

Positions moved forward from the birth or inception chart by a rule, and returns to its positions.

| Feature | Marathi name (Vedic features) | Tradition | Note |
|---|---|---|---|
| Secondary progressions | — | Western |  |
| Solar arc directions | — | Western |  |
| Primary directions | — | Western |  |
| Tertiary and minor progressions | — | Western |  |
| Returns | — | Western | Moment the Sun, Moon or a planet returns to its birth or inception longitude. |
| Draconic positions | — | Western |  |

## Layer 8. Comparison of a birth or inception chart with later moments or other charts

Needs the birth or inception chart (layer 7 foundation) and the layers 1 to 5 values at a later moment or for a second chart, compared with each other.

### Transit comparisons

A later moment compared with the birth or inception chart.

| Feature | Marathi name (Vedic features) | Tradition | Note |
|---|---|---|---|
| Transits to a birth or inception chart | — | Western | Positions of a later moment compared with the birth or inception chart. |
| Gochar from Moon, Lagna or Sun | चंद्र / लग्न / सूर्यापासून गोचर | Vedic | Houses counted from the Moon, Lagna or Sun of the birth or inception chart. |
| Vedha | वेध | Vedic |  |
| Sade Sati | साडेसाती | Vedic | Shani position compared with the Moon sign of the birth or inception chart. |
| Dhaiyya and Kantaka Shani | ढैय्या / अष्टम शनी / कंटक शनी | Vedic |  |
| Guru and Rahu-Ketu gochar | गुरू गोचर / राहू-केतू गोचर | Vedic |  |
| Ashtakavarga gochar | अष्टकवर्ग गोचर | Vedic |  |
| Mangal Dosha by transit against a birth or inception chart | गोचर मांगलिक दोष | Vedic | Mars position at a later moment counted from the birth or inception chart. |
| Chandra Bala, Tara Bala, Chandrashtama | चंद्र बल / तारा बल / चंद्राष्टम | Vedic |  |

### Chart-to-chart comparisons

Two charts compared with each other.

| Feature | Marathi name (Vedic features) | Tradition | Note |
|---|---|---|---|
| Compatibility score between two charts | अष्टकूट / गुणमिलन | Vedic | Compares the Moon of the birth or inception chart with the Moon (or another chart) of a later moment. |
| Synastry aspects | — | Western | One of the two charts can be the chart of any moment. |
| Composite chart | — | Western |  |
| Davison relationship chart | — | Western |  |

# Part 2: Western and Vedic comparison

Each feature is shown with its status in each tradition and a classification.

| Status | Meaning |
|---|---|
| Applicable | The feature is used in that tradition in the same way. |
| Applicable with a different method or name | The tradition has the same idea but calculates it differently or calls it something else. |
| Not applicable | The tradition does not use the feature. |

| Classification | Meaning |
|---|---|
| Common to both (same method) | Both traditions use it in the same way. |
| Common to both (different method or name) | Both traditions have it, with a different method or name. |
| Western only | Only Western astrology has it. |
| Vedic only | Only Vedic astrology has it. |

## Totals

| Classification | Number of features |
|---|---|
| Common to both (same method) | 9 |
| Common to both (different method or name) | 43 |
| Western only | 37 |
| Vedic only | 50 |
| All compared features | 139 |

## Positions and coordinates

| Feature | Western astrology | Vedic astrology | Classification | Note |
|---|---|---|---|---|
| Ecliptic position (longitude, latitude, distance, speed) | Applicable: Ecliptic longitude, Ecliptic latitude, Distance, Speed | Applicable: Planetary position (Navagraha) | Common to both (same method) | Western astrology usually uses the tropical zodiac and Vedic astrology the sidereal zodiac, but the calculation is the same. |
| Equatorial position (right ascension, declination) | Applicable: Right ascension, Declination | Applicable with a different method or name: used inside the strength calculations rather than as a stand-alone feature | Common to both (different method or name) |  |
| Horizontal position (azimuth, altitude) | Applicable: Azimuth and altitude | Not applicable as a stand-alone feature | Western only |  |
| Heliocentric position (seen from the Sun) | Applicable: Heliocentric coordinates | Not applicable: Vedic technique is Moon-centred | Western only | A Vedic profile with a heliocentric frame is not valid. |
| Barycentric position | Applicable: Barycentric coordinates | Not applicable | Western only |  |
| Topocentric position (seen from the observer) | Applicable: Topocentric coordinates | Applicable: optional | Common to both (same method) | Matters mainly for the Moon. |
| Lunar nodes | Applicable: Lunar nodes | Applicable with a different method or name: Rahu and Ketu | Common to both (different method or name) | Ketu is the point opposite Rahu. |
| Outer planets (Uranus, Neptune, Pluto) | Applicable: included in the ecliptic position | Applicable: Outer planets (used by some modern Indian astrologers) | Common to both (same method) |  |
| Lilith (lunar apogee) | Applicable: Lilith (lunar apogee) | Not applicable: not part of classical Vedic astrology | Western only |  |
| Chiron, Pholus and asteroids | Applicable: Chiron and Pholus, Main asteroids, Further asteroids and distant bodies | Not applicable | Western only |  |
| Uranian (Hamburg School) hypothetical points | Applicable: Uranian hypothetical points | Not applicable | Western only |  |
| Fixed stars and galactic points | Applicable: Fixed stars, Galactic points | Not applicable as a stand-alone feature (the nakshatras are defined by star groups) | Western only |  |
| Nodes and apsides of planets | Applicable: Planetary nodes and apsides | Not applicable | Western only |  |
| Earth and Moon apsides (perigee, apogee) | Applicable: Earth and Moon apsides | Not applicable | Western only |  |
| Ayanamsha value | Applicable: Ayanamsha value (for the sidereal zodiac) | Applicable: Ayanamsha value | Common to both (same method) |  |
| Equation of time | Applicable: Equation of time | Not applicable as a stand-alone feature (used inside sunrise calculation) | Western only |  |
| Sidereal time | Applicable: Sidereal time | Not applicable as a stand-alone feature (used inside the Lagna calculation) | Western only |  |

## Houses, angles and the day

| Feature | Western astrology | Vedic astrology | Classification | Note |
|---|---|---|---|---|
| Ascendant (rising sign) | Applicable: Ascendant and Descendant | Applicable: Lagna (Ascendant) | Common to both (different method or name) | Vedic astrology gives the rising sign more weight than the exact degree. |
| Midheaven and IC | Applicable: Midheaven and IC | Applicable with a different method or name: counted as the tenth house | Common to both (different method or name) |  |
| Other angles (Vertex, East Point and similar) | Applicable: Other angles | Not applicable | Western only |  |
| House cusps and house systems | Applicable: House cusps | Applicable: Houses | Common to both (different method or name) | Vedic astrology mostly uses whole-sign, Sripati or equal houses; Western astrology uses many systems. |
| Planets in houses | Applicable: Planets in houses | Applicable: Graha in bhava | Common to both (different method or name) |  |
| House rulers (lords) | Applicable: House rulers | Applicable: House lords | Common to both (different method or name) |  |
| House types (angular, succedent, cadent; kendra, panapara, apoklima) | Applicable: Angular, succedent and cadent houses | Applicable: House types (kendra, panapara, apoklima, trikona, dusthana) | Common to both (different method or name) | Kendra, panapara and apoklima correspond to angular, succedent and cadent houses. Trikona and dusthana are used only in Vedic astrology. |
| Gauquelin sectors | Applicable: Gauquelin sectors | Not applicable | Western only |  |
| Position within a house | Applicable: Position within a house | Not applicable as a stand-alone feature | Western only |  |
| Bhava Chalit (planets shifting between houses) | Not applicable | Applicable: Bhava Chalit | Vedic only |  |
| Angle and Lagna sign changes | Applicable: Angle sign changes | Applicable: Lagna changes | Common to both (different method or name) |  |
| Angular transits (planets crossing the angles) | Applicable: Angular transits | Not applicable | Western only |  |
| Fixed-star parans | Applicable: Fixed-star parans | Not applicable | Western only |  |
| Rise, set and twilight | Applicable: Rise, set and twilight | Applicable: Sunrise, sunset, moonrise, moonset | Common to both (same method) |  |
| Planetary day and hour rulers | Applicable: Planetary day and hour rulers | Applicable: Hora | Common to both (different method or name) |  |
| Day and night length | Applicable: part of Rise, set and twilight | Applicable: Day and night length | Common to both (same method) |  |
| Vedic time units (ghatika and pala) | Not applicable | Applicable: Ghatika and pala | Vedic only |  |
| Daily auspicious and inauspicious periods | Not applicable | Applicable: Choghadiya, Inauspicious periods (Rahu Kala, Yamaganda, Gulika Kala), Auspicious muhurtas, Further muhurta periods | Vedic only |  |

## Signs and their subdivisions

| Feature | Western astrology | Vedic astrology | Classification | Note |
|---|---|---|---|---|
| Sign and degree | Applicable: Sign and degree | Applicable: Sign (Rashi) of each graha | Common to both (different method or name) |  |
| Sign ingress | Applicable: Sign ingress | Applicable: Sign ingress, Sankranti | Common to both (different method or name) |  |
| Sign lord and star lord | Applicable with a different method or name: sign rulers used inside dignity and house-ruler features | Applicable: Sign lord and star lord | Common to both (different method or name) |  |
| Nakshatra and pada (lunar mansions) | Applicable with a different method or name: Lunar mansions (the 28 Arabic mansions) | Applicable: Nakshatra and Pada | Common to both (different method or name) | The Western mansions are an esoteric system; the nakshatras are central to Vedic astrology. |
| Nakshatra ingress | Not applicable | Applicable: Nakshatra ingress | Vedic only |  |
| Sun's nakshatra (including monsoon nakshatras) | Not applicable | Applicable: Sun's nakshatra | Vedic only |  |
| Decans | Applicable: Decans (faces) | Applicable with a different method or name: Drekkana (third divisional chart) | Common to both (different method or name) |  |
| Terms (bounds) | Applicable: Terms (bounds) | Not applicable | Western only |  |
| Dodecatemoria (twelfth-parts) | Applicable: Dodecatemoria | Applicable with a different method or name: Dwadashamsha (twelfth divisional chart) | Common to both (different method or name) |  |
| Harmonic positions | Applicable: Harmonic positions | Applicable with a different method or name: divisional charts divide a sign instead of multiplying the longitude | Common to both (different method or name) |  |
| Critical degrees | Applicable: Critical degrees | Applicable with a different method or name: Gandanta, Mrityu bhaga, Pushkara zones | Common to both (different method or name) |  |
| Out of bounds | Applicable: Out of bounds | Not applicable | Western only |  |
| Element and modality balance | Applicable: Element and modality balance | Not applicable | Western only |  |
| Hemisphere and quadrant emphasis | Applicable: Hemisphere and quadrant emphasis | Not applicable | Western only |  |
| Sect (day or night chart) | Applicable: Sect | Not applicable as a stand-alone feature (day and night strength is inside Shadbala) | Western only |  |
| Divisional charts (Shodashavarga and extended vargas) | Not applicable | Applicable: Shodashavarga: sixteen divisional charts, Extended vargas | Vedic only |  |
| Vargottama and Pushkara zones | Not applicable | Applicable: Vargottama, Pushkara navamsha and bhaga | Vedic only |  |
| Varga sign changes | Not applicable | Applicable: Varga sign changes | Vedic only |  |
| Moon and Sun as the reference point | Not applicable | Applicable: Moon and Sun as lagna | Vedic only |  |
| Seasons and half-years | Applicable with a different method or name: Cardinal points | Applicable: Ritu and Ayana | Common to both (different method or name) |  |

## Dignity, condition and strength

| Feature | Western astrology | Vedic astrology | Classification | Note |
|---|---|---|---|---|
| Essential dignity (exaltation, debilitation, own sign and similar) | Applicable: Essential dignities, Detriment, fall, peregrine | Applicable: Dignity state | Common to both (different method or name) | The tables of dignities differ between the traditions. |
| Planetary friendship | Not applicable: Western astrology uses reception instead | Applicable: Planetary friendship | Vedic only |  |
| Mutual reception (exchange of signs) | Applicable: Mutual reception | Applicable: Parivartana | Common to both (different method or name) |  |
| Combustion | Applicable: Combust, cazimi, under the beams | Applicable: Combustion and rising or setting | Common to both (different method or name) |  |
| Oriental and occidental position | Applicable: Oriental and occidental | Applicable with a different method or name: rising and setting states (Udaya, Ast) | Common to both (different method or name) |  |
| Retrograde, direct and stationary | Applicable: Retrograde and direct | Applicable: Retrograde and direct | Common to both (same method) |  |
| Retrograde periods | Applicable: Retrograde periods and shadows | Applicable: retrograde periods (shadow periods are not used) | Common to both (different method or name) |  |
| Speed class | Applicable: Speed class | Applicable: Speed and fast transits | Common to both (different method or name) |  |
| Accidental dignity | Applicable: Accidental dignities | Applicable with a different method or name: Avasthas and Shadbala | Common to both (different method or name) |  |
| Almuten and time lords of the hour or year | Applicable: Almuten and lords | Not applicable | Western only |  |
| Planetary war | Not applicable | Applicable: Planetary war | Vedic only |  |
| Planetary states (Avasthas) | Not applicable | Applicable: Avasthas | Vedic only |  |
| Strength measures | Not applicable | Applicable: Shadbala, Ishta and Kashta phala, Bhava bala, Vimshopaka bala | Vedic only |  |
| Ashtakavarga | Not applicable | Applicable: Ashtakavarga | Vedic only |  |
| Chara karakas | Not applicable | Applicable: Chara karakas | Vedic only |  |
| Rahu-Ketu hemming | Not applicable | Applicable: Rahu-Ketu hemming | Vedic only |  |

## Aspects and geometry

| Feature | Western astrology | Vedic astrology | Classification | Note |
|---|---|---|---|---|
| Angle-based aspects (major and minor) | Applicable: Major aspects, Minor aspects | Applicable with a different method or name: Geometric aspects in the sidereal zodiac (optional), and the sign-based Graha drishti | Common to both (different method or name) |  |
| Conjunction | Applicable: part of Major aspects | Applicable: Conjunction | Common to both (same method) |  |
| Exact aspect moments and windows | Applicable: Exact aspect times, Aspect windows | Applicable: for the geometric aspects | Common to both (different method or name) |  |
| Aspects to angles and cusps | Applicable: Aspects to angles and cusps | Applicable with a different method or name: drishti on houses | Common to both (different method or name) |  |
| Graha drishti (Parashari aspects) | Not applicable | Applicable: Graha drishti | Vedic only |  |
| Rashi drishti (Jaimini sign aspects) | Not applicable | Applicable: Rashi drishti | Vedic only |  |
| Argala | Not applicable | Applicable: Argala | Vedic only |  |
| Parallels and contra-parallels | Applicable: Parallels and contra-parallels | Not applicable | Western only |  |
| Antiscia and contra-antiscia | Applicable: Antiscia and contra-antiscia | Not applicable | Western only |  |
| Midpoints, midpoint trees and the 90-degree dial | Applicable: Midpoints, Midpoint trees and 90-degree dial | Not applicable | Western only |  |
| Aspect patterns | Applicable: Aspect patterns | Applicable with a different method or name: yogas | Common to both (different method or name) |  |
| Heliocentric aspects and ingresses | Applicable: Heliocentric aspects and ingresses | Not applicable | Western only |  |
| Composite aspect indices | Applicable: Composite aspect indices | Not applicable | Western only |  |
| Hemming of a planet between two others | Applicable with a different method or name: besieged (part of Accidental dignities) | Applicable: Kartari | Common to both (different method or name) |  |

## Moon, eclipses and planetary cycles

| Feature | Western astrology | Vedic astrology | Classification | Note |
|---|---|---|---|---|
| Moon phase and illumination | Applicable: Moon phase | Applicable with a different method or name: Tithi and Paksha | Common to both (different method or name) |  |
| Principal lunar phases (new, full) | Applicable: Principal lunar phases | Applicable with a different method or name: Amavasya and Purnima (tithi moments) | Common to both (different method or name) |  |
| Lunation cycle phase | Applicable: Lunation cycle phase | Applicable with a different method or name: Tithi (thirty phases) | Common to both (different method or name) |  |
| Void-of-course Moon | Applicable: Void-of-course Moon | Not applicable | Western only |  |
| Lunar declination extremes | Applicable: Lunar declination extremes | Not applicable | Western only |  |
| Eclipses | Applicable: Solar eclipses, Lunar eclipses | Applicable: Eclipses | Common to both (same method) | Vedic astrology adds the Sutak period. |
| Eclipse seasons and series | Applicable: Eclipse seasons and series | Not applicable | Western only |  |
| Occultations | Applicable: Occultations | Not applicable | Western only |  |
| Planetary transits of the Sun (Mercury, Venus) | Applicable: Planetary transits of the Sun | Not applicable | Western only |  |
| Planetary phenomena (phase angle, elongation, magnitude) | Applicable: Planetary phenomena | Not applicable | Western only |  |
| Heliacal events and greatest elongations | Applicable: Greatest elongations and heliacal events | Applicable with a different method or name: Udaya and Ast | Common to both (different method or name) |  |
| Synodic cycles and Great Conjunction series | Applicable: Synodic cycles of body pairs, Great Conjunction series | Not applicable as a separate feature (conjunction is covered by Yuti) | Western only |  |
| Planet-Sun relations (conjunction, opposition, quadrature with the Sun) | Applicable: Planet-Sun relations | Not applicable as a separate feature (Ast covers combustion) | Western only |  |
| Cardinal points (equinoxes, solstices) | Applicable: Cardinal points | Applicable with a different method or name: Sankranti and Ayana | Common to both (different method or name) |  |

## Panchang and the Vedic calendar

| Feature | Western astrology | Vedic astrology | Classification | Note |
|---|---|---|---|---|
| Tithi and Paksha | Not applicable: see Moon phase | Applicable: Tithi, Tithi spans, Paksha | Vedic only |  |
| Nitya Yoga | Not applicable | Applicable: Yoga (Nitya yoga) | Vedic only |  |
| Karana | Not applicable | Applicable: Karana | Vedic only |  |
| Nakshatra spans | Not applicable | Applicable: Nakshatra spans | Vedic only |  |
| Weekday (Vara) | Applicable with a different method or name: planetary day rulers, starting at midnight | Applicable: Vara (starting at sunrise) | Common to both (different method or name) |  |
| Lunar month, Samvatsara and eras | Not applicable | Applicable: Lunar month, Samvatsara and eras | Vedic only |  |
| Festivals and vrata days | Not applicable | Applicable: Festivals and vrata days | Vedic only |  |
| Bhadra, Panchaka and Gand Mool | Not applicable | Applicable: Bhadra (Vishti), Panchaka and Gand Mool | Vedic only |  |
| Muhurta yogas and inauspicious panchang combinations | Not applicable | Applicable: Muhurta yogas, Inauspicious panchang combinations | Vedic only |  |
| Visha Ghati, Lattaa and Pata | Not applicable | Applicable: Visha Ghati, Lattaa and Pata | Vedic only |  |
| Disha Shoola | Not applicable | Applicable: Disha Shoola | Vedic only |  |
| Sutak | Not applicable | Applicable: Sutak | Vedic only |  |
| Chandra Bala, Tara Bala, Chandrashtama | Not applicable | Applicable: Chandra Bala, Tara Bala, Chandrashtama | Vedic only |  |

## Special points and lots

| Feature | Western astrology | Vedic astrology | Classification | Note |
|---|---|---|---|---|
| Lots (Arabic parts) and Sahams | Applicable: Lots and Arabic parts | Applicable: Sahams | Common to both (different method or name) |  |
| Special lagnas | Not applicable | Applicable: Special lagnas | Vedic only |  |
| Arudha padas | Not applicable | Applicable: Arudha padas | Vedic only |  |
| Upagrahas (Gulika, Mandi and others) | Not applicable | Applicable: Upagrahas | Vedic only |  |
| Sensitive points (Bhrigu Bindu, Yogi, Avayogi, Pranapada) | Not applicable | Applicable: Sensitive points | Vedic only |  |
| KP lords (star, sub, sub-sub), cusp sub lords, significators, ruling planets | Not applicable | Applicable: Star lord, sub lord, sub-sub lord, Cusp sub lords, Significators, Ruling planets | Vedic only |  |
| Sub-lord changes | Not applicable | Applicable: Sub-lord changes | Vedic only |  |

## Time-lord and predictive systems (need a birth or inception chart)

| Feature | Western astrology | Vedic astrology | Classification | Note |
|---|---|---|---|---|
| Time-lord period systems | Applicable: Annual and monthly profections, Firdaria, Zodiacal releasing, Decennials | Applicable: Vimshottari dasha, Ashtottari, Yogini, Chara, Kalachakra, other dasha systems | Common to both (different method or name) |  |
| Dasha lord changes, dasha balance and KP periods | Not applicable | Applicable: Dasha lord changes, Dasha balance, KP dasha-bhukti-antara | Vedic only |  |
| Maraka and Badhaka periods, longevity | Not applicable | Applicable: Maraka lords and periods, Badhaka lord and periods, Longevity calculation | Vedic only |  |
| Progressions and directions | Applicable: Secondary progressions, Solar arc directions, Primary directions, Tertiary and minor progressions | Not applicable | Western only |  |
| Returns | Applicable: Returns | Applicable with a different method or name: Varsha Pravesh | Common to both (different method or name) |  |
| Draconic positions | Applicable: Draconic positions | Not applicable | Western only |  |
| Annual chart techniques | Not applicable | Applicable: Muntha and Varshesha, Mudda and Patyayini dasha, Tajika sahams, Tajika aspects | Vedic only |  |
| Karakamsha and Swamsha | Not applicable | Applicable: Karakamsha and Swamsha | Vedic only |  |

## Charts at moments and comparison with a birth or inception chart

| Feature | Western astrology | Vedic astrology | Classification | Note |
|---|---|---|---|---|
| Charts at event moments | Applicable: Charts at event instants | Applicable: Sankranti charts, Lunation and new-year charts, Chart at an instant | Common to both (different method or name) |  |
| Transits against a birth or inception chart | Applicable: Transits to a birth or inception chart | Applicable: Gochar from Moon, Lagna or Sun | Common to both (different method or name) | Vedic astrology counts houses from the Moon as well as from the Lagna. |
| Slow-planet transit periods (Sade Sati, Dhaiyya, Kantaka Shani, Guru and Rahu-Ketu gochar) | Not applicable as separate features | Applicable: Sade Sati, Dhaiyya and Kantaka Shani, Guru and Rahu-Ketu gochar | Vedic only |  |
| Vedha, Ashtakavarga gochar and Kakshya gochar | Not applicable | Applicable: Vedha, Ashtakavarga gochar, Kakshya gochar | Vedic only |  |
| Comparison of two charts | Applicable: Synastry aspects, Composite chart, Davison relationship chart | Applicable: Compatibility score between two charts | Common to both (different method or name) |  |

## Yogas, doshas and rule libraries

| Feature | Western astrology | Vedic astrology | Classification | Note |
|---|---|---|---|---|
| Yogas (planetary combinations) | Not applicable: Western astrology uses aspect patterns | Applicable: Pancha Mahapurusha yogas, Raja, Dhana and cancellation yogas, Moon-based yogas, Sun-based yogas, Nabhasa yogas, Other classical yogas | Vedic only |  |
| Dosha-type combinations | Not applicable | Applicable: Dosha-type combinations | Vedic only |  |
| Mangal Dosha | Not applicable | Applicable: Mangal Dosha in a chart, Mangal Dosha by transit, Mangal Dosha cancellation and strength | Vedic only |  |
| Kala Sarpa and Pitru Dosha | Not applicable | Applicable: Kala Sarpa Dosha and its twelve types, Pitru Dosha | Vedic only |  |
| Chakras (Sarvatobhadra, Sapta Shalaka and others) | Not applicable | Applicable: Sarvatobhadra Chakra, Other chakras | Vedic only |  |
| Teji-Mandi rules | Not applicable | Applicable: Teji-Mandi rules | Vedic only |  |

## Fixed reference data

| Feature | Western astrology | Vedic astrology | Classification | Note |
|---|---|---|---|---|
| Natural significations, nakshatra attributes and static tables | Not applicable as a separate feature (the Western tables are built into the dignity features) | Applicable: Natural significations, Nakshatra attributes, Static lookup tables | Vedic only |  |

