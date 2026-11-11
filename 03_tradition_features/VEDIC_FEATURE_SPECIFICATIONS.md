# Vedic Feature Specifications — Working Register

**Status:** Feature family specifications not yet researched. Use `FEATURE_SPECIFICATION_TEMPLATE.md` for each feature or family. The complete source inventory, including Marathi names, is in `01_inventory/VEDIC_FEATURE_INVENTORY.md`.

## Family map from the source catalogue

- V1 — Grahas and their positions.
- V2 — Panchang and time divisions.
- V3 — Lagna, Bhava and special points.
- V4 — Drishti and relationships.
- V5 — Varga / divisional charts.
- V6 — Dasha systems.
- V7 — Gochar / transits.
- V8 — Bala, Ashtakavarga and chakras.
- V9 — Yogas and planetary combinations.
- V10 — Eclipses and mundane astrology.
- V11 — Tajika annual charts.
- V12 — KP.
- V13 — Reference data and other Vedic items.
- V14 — Doshas, adverse conditions and chart-comparison scores.

## Required approach

1. Preserve all source V-* IDs and Marathi labels.
2. Do not treat Vedic astrology as one uniform rule system. Record school, lineage, regional practice and calculation convention where relevant.
3. Keep Parashari, Jaimini, KP, Tajika and other systems distinguishable; do not merge their rules.
4. For each Panchanga element, specify formula, boundary convention, local-day assumptions and whether the result is location-dependent.
5. For divisional charts, specify sign division, mapping rule, dignity/interpretation rules and the exact varga set.
6. For dashas, specify system, sequence, duration model, year length, balance at birth/inception, eligibility and boundary semantics.
7. For strength, yoga, dosha and friendship features, specify all recognised variants and source provenance.
8. Keep external festival/vrata calendars separate from purely astronomical calculation.
9. Map every feature to shared raw astronomy, reference tables, location/time and chart dependencies.

## Family status

All families: `NOT_REVIEWED` beyond source-catalogue import.
