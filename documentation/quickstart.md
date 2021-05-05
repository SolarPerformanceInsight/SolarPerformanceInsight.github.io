---
layout: base
permalink: /quickstart/
sidebar: quickstart_sidebar.html
title: Quickstart
---

{% include to_top.html %}


The Solar Performance Insight tool provides both a [Dashboard](#dashboard) and an [API](#api).


## Dashboard {#dashboard}
{: .anchor}

After logging in, the Dashboard guides you through the following steps:

1. Define or select the [system] (#definesystem)
2. Choose a workflow:
   - [Calculate performance] (#calculateperformance)
   - [Compare performance] (#compareperformance)

## Systems {#system}
{: .anchor}

A PV system is defined by four sets of data:
1. The performance model associated with the system. Options are [pvsyst-like](#pvsyst), [pvwatts](#pvwatts) and [SAM](#SAM).
2. System metadata, including:
   - name
   - latitude and longitude. Use decimal degress (e.g., 35.5) without a direction character (e.g. N, E) and use negative longitude for locations west of the prime meridian.
   - elevation above mean sea level in meters
3. [Inverters] (#inverter). The options for inverter parameters depend on the performance model.
4. [Arrays] (#array). An array is a collection of modules with the same fixed or tracking orientation. One or more arrays can be associated with each inverter. Array parameters depend on the performance model.

### Pvsyst {#pvsyst}

### PVWatts {#pvwatts}

### SAM {#SAM}


## Calculate performance {#calculateperformance}
{: .anchor}

## Compare performance {#calculateperformance}
{: .anchor}

## API {#api}
{: .anchor}
