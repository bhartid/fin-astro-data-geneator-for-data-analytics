# Architecture and Implementation Gate

## 1. Current rule

Architecture is not frozen. The project is in inventory and dependency discovery. This gate prevents premature implementation based on an incomplete feature list.

## 2. Preconditions for architecture design

All must be true:
- Western and Vedic inventories audited and owner-reviewed.
- Common astronomy capability inventory audited against official Swiss Ephemeris docs.
- Financial astrology and Gann extension domains inventoried to the agreed scope.
- Exclusions reviewed and justified.
- Every feature has provenance and dependency classification.
- Every dependency chain reaches explicit raw inputs, settings, reference data and event-search primitives.
- Configuration compatibility matrix technically verified.
- Time, location, coordinate and market alignment semantics specified.
- API limitations, ephemeris files, binding choice and licensing implications documented.
- Owner approves the foundation requirements.

## 3. Architecture design outputs

After the gate, design:
- package/module boundaries;
- ephemeris adapter boundary;
- body and reference-data registries;
- calculation profile model;
- request validation and compatibility rules;
- time/location/coordinate value objects;
- direct-result and derived-feature contracts;
- event-search framework;
- provenance/metadata contract;
- error/warning model;
- deterministic handling of Swiss Ephemeris state;
- extension interfaces for Western, Vedic and Gann modules;
- test strategy and reference datasets;
- packaging and Windows portability.

## 4. Implementation gate

Do not write implementation code until the owner explicitly moves the project from scoping/design to implementation. Before that point, deliver specifications, architecture diagrams, interface contracts and test plans only.

## 5. Quality gates

A feature is not complete merely because it returns a number. It must have:
- approved definition and convention;
- dependency traceability;
- correct units and coordinate semantics;
- reproducible metadata;
- reference tests and tolerances;
- documented limitations and edge cases.
