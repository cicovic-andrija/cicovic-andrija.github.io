---
title: "Dive Computer Reference: Smart Air"
date: "2023-03-10T07:10:18Z"
categories: ["diving"]
tags: ["equipment", "references"]
draft: false
---

## Calculation and Operational Parameters

- All calculations are based purely on pressure measurements.
- Ascent calculations assume an ascent rate of 10m/min.
- Depth is shown in 10cm resolution above 100m, after which resolution is 1m.
- Maximum depth is 150m.
- At surface:
  - In pre-dive mode, dive calculations auto-start at depth of 1.2m.
  - In pre-dive mode, if not submerged within 3 minutes the mode reverts back to regular watch.
  - In non pre-dive mode, dive calculations start with up to 20s of delay after reaching 1.2m.
  - After surfacing, dive calculations will resume if submerged again in less than 3 min.

## Dive Parameters (Set Pre-dive)

- ppO2max - The maximum allowed value of ppO2, with max possible value of 1.6 bar (**DANGEROUS**).
  - In AIR mode, ppO2max is set to 1.4 bar.
  - In NITROX mode, set manually.
- O2% - Oxygen concentration used by the dive computer in all calculations.
  - In AIR mode, set to 21% (ppO2 at surface is 0.21 bar).
  - In NITROX mode, set manually.
- P Factor - personalization factor.
  - P0: standard deco algorithm.
  - P1: more conservative alg.
  - P2: the most conservative alg.
  - Shown in logs as (none), p+ and p++.
- Altitude setting.
  - A0: 0-700m
  - A1: 700-1500m
  - A2: 1500-2400m
  - A3: 2400-3700m
  - Diving at altitudes above 3700m is not recommended (**DANGEROUS**).
  - Shown in logs as (none) or a mountain icon + N, where N is 1, 2 or 3.

## Dive Measurements, Calculations and Monitoring

- DEPTH - Current depth [measured].
- MAX - Maximum reached depth [measured].
- AVG - Average depth [calculated] from continuous depth readings [measured].
- MOD - Maximum Operating Depth - the depth at which the ppO2 levels become unsafe [calculated].
- ASC - Total ascent time in a deco dive, including all deco stops [calculated].
- NO DECO - Time remaining at current depth without going into deco [calculated].
- TTR - Time To Reserve - time that can be spent at current depth before reaching the tank reserve
  (if paired with a tank) [calculated].
- DTIME - Total dive time [measured].
- CNS - Central Nervous System - quantifies toxic effects of O2 as result of longer exposures to ppO2 > 0.5 bar;
  [calculated] independently of pre-set ppO2max.
- ppO2 - Partial pressure of oxygen [calculated] based on current depth reading [measured].
- C [degrees] - Water temperature [measured].
- DECO - Depth and duration of the next **MANDATORY** decompression stop in a deco dive [calculated].
- DEEP - Depth of the current **optional** deep stop (can be one 2-min or two 1-min stops near the no deco limit)
  and its duration [calculated].
- SAFE - Duration of the **optional but RECOMMENDED** 3 minute safe stop between 6m and 3m [fixed].

## Post-dive Monitoring

- Dive can be resumed after up to 3 minutes of surface time (TIME OUT).
- DESAT - Desaturation time [calculated].
- NO FLY - Minimum amount of time before taking a plane, dependant on recent dive parameters - 12h or 24h [fixed].
- S.I. - Surface Interval - Time spent since the last dive was completed; remains until both DESAT and NO FLY are spent.

## Alarms

- Ascent rate alarm - when ascent is faster than 10m/min.
- Exceeding a safe ppO2max (or MOD) alarm.
- CNS at 75% (first warning), OR 100% alarm (**DANGEROUS**) - danger of oxygen toxicity.
- Missed deco stop alarm - when ascended more than 0.3m above the deco stop.
- Low tank pressure alarm (if paired with a tank).
- Low battery during the dive alarm - safe for diving but not much battery reserve left.

## Violations

_Violations do not permit repeated dives - the computer acts as a bottom timer only (measures only time,
temp and depth)._

- Fast ascent violation - ascent of 12m/min for more than 2/3 of ascent (starting at depth of first alarm).
- Missed deco stop violation - more than 1m above the deco stop for more than 3 minutes.

## Battery and Light

- Battery: CR2450
- Holding the UP button activates the backlight.
