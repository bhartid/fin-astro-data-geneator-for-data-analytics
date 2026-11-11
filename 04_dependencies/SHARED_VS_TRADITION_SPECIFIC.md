# Shared Astronomy vs Tradition-Specific Computation

## 1. Governing principle

The low-level astronomy layer should be tradition-neutral. It should answer astronomical questions, not decide what a planet means in a particular astrology school.

Western and Vedic engines consume shared outputs but may request different calculation profiles and apply different definitions, tables and algorithms.

## 2. Shared capability examples

- Time conversion and ephemeris time context.
- Celestial body identity and ephemeris lookup.
- Position, speed, distance and coordinate outputs.
- Reference-frame and coordinate transformations.
- Observer-dependent sky calculations.
- Rise/set and twilight calculations.
- Planetary/lunar phenomena.
- Eclipse and occultation data.
- Event-search primitives.
- Houses/angles as geometric calculations, with careful separation from house interpretation.

## 3. Downstream tradition-specific examples

| Shared input | Western calculation family | Vedic calculation family |
|---|---|---|
| Zodiac longitude | Tropical signs, decans, bounds, harmonics | Sidereal Rashi, Nakshatra, Pada |
| Sun and Moon longitude | Lunar phase, lunation phase | Tithi, Paksha, Nitya Yoga, Karana |
| Planet longitudes | Western aspects and configurations | Graha Drishti and relationship rules |
| Planet speed | Direct/retrograde, stations, speed classifications | Vakri/Margi, Atichari and school-specific motion rules |
| Planet longitude + house geometry | House placement, house rulers, lots | Bhava placement, Bhava Chalit, house lords |
| Position + reference tables | Dignity, sect, bounds, decans | Dignity, friendship, avasthas, yogas |
| Exact event instants | Ingresses, aspects, returns | Rashi/Nakshatra ingress, Sankranti, Panchanga boundaries |

These examples illustrate separation; they are not final feature definitions.

## 4. Configuration is not the same as tradition

Ayanamsha, zodiac, coordinate frame, position semantics and house system are configuration choices. Aspect rules, Drishti, Tithi naming/boundary conventions, dignity systems and dasha algorithms are rule definitions. Some tradition modules may require a particular profile, but the rule itself must remain explicit and versioned.

## 5. Foundation design consequence

Do not create `western_ephemeris_engine` and `vedic_ephemeris_engine` as separate copies of the same low-level engine. Prefer one astronomy adapter/service and separate feature/rule modules. If a tradition requires a distinct astronomical convention, express it as an explicit profile/request and preserve its provenance.
