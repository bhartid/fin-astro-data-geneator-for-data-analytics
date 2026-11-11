# Time, Location and Coordinate Semantics

## 1. Time model

The project must distinguish:
- user-supplied civil datetime;
- timezone and daylight-saving interpretation;
- normalized UTC instant;
- Julian day in UT and/or ET/TT as required by the API;
- delta-T and other time-scale conversion metadata;
- local apparent solar time, local mean solar time and civil clock time where relevant.

Do not assume a naive datetime is UTC. Require an explicit interpretation or reject ambiguous input. Use Python `datetime`/`zoneinfo` where appropriate, but verify precision and time-scale conversion requirements against Swiss Ephemeris.

## 2. Sampling and market intervals

A requested timeframe (for example 1 minute, 5 minutes, 1 day or 1 week) defines a sampling grid, not necessarily the exact event time. Exact ingresses, aspects and transitions require event-search logic. A sampled series can miss short-lived events or misstate the boundary.

The market alignment specification must later define:
- candle open timestamp versus close timestamp;
- inclusive/exclusive interval boundaries;
- exchange timezone and trading calendar;
- overnight sessions and daylight-saving transitions;
- treatment of weekends/holidays;
- event-to-candle mapping (containing bar, nearest bar, before/after bar);
- missing market bars and out-of-session events.

## 3. Location model

Do not represent every kind of location with one generic field. Distinguish:
- observer location for topocentric/horizontal/rise-set calculations;
- chart-origin location for natal/company/instrument inception chart features;
- market/exchange location and timezone for market-data alignment;
- regional-calendar jurisdiction for festivals and observances.

For observer coordinates, preserve latitude, longitude, altitude, datum/source and sign conventions. A city lookup is a convenience; exact coordinates and timezone should remain inspectable.

## 4. Coordinate model

Every coordinate must declare:
- origin/reference frame (geocentric, topocentric, heliocentric, barycentric);
- coordinate system (ecliptic, equatorial, horizontal, etc.);
- reference plane and epoch/equinox when relevant;
- zodiac transformation (tropical/sidereal) and ayanamsha when relevant;
- units and angular normalisation;
- apparent/true/astrometric semantics as defined by the API.

Never store a bare field called `longitude` without enough metadata to interpret it.

## 5. Local-day and sunrise semantics

Civil midnight, local apparent midnight and sunrise-based Vedic day boundaries are not interchangeable. Vara and sunrise-relative periods need a declared sunrise convention, timezone, location and polar/no-sunrise fallback policy.

## 6. Event boundary precision

Every event or interval feature must define:
- exact mathematical condition;
- start/end boundary convention;
- search interval and bracketing;
- numerical tolerance;
- whether boundary time is a point instant or an interval estimate;
- handling of repeated crossings, retrograde loops and tangent contacts;
- local-time rendering versus canonical UTC storage.
