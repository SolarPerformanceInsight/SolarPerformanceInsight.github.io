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
1. The performance model defines the sequence of models to be used to calculate output of the system. Options are [pvsyst-like](#pvsyst), [pvwatts](#pvwatts) and [SAM](#SAM).
2. System metadata, including:
   - name
   - latitude and longitude. Use decimal degress (e.g., 35.5) without a direction character (e.g. N, E) and use negative longitude for locations west of the prime meridian.
   - elevation above mean sea level in meters
3. [Inverters] (#inverter). A system can have one or more inverters. The options for inverter parameters depend on the performance model.
4. [Arrays] (#array). An array is a collection of modules with the same fixed or tracking orientation. One or more arrays can be associated with each inverter. Array parameters depend on the performance model.


## System performance models

Solar Performance Insight uses functions from [pvlib](https://github.com/pvlib/pvlib-python.git) to calculate system output consistent with the selected performance model: [pvsyst-like](#pvsyst), [pvwatts](#pvwatts) and [SAM](#SAM).

### Pvsyst {#pvsyst}

Calculate system output consistent with the (Pvsyst)[https://www.pvsyst.com] software package. The 'pvsyst-like' model includes only those steps in a Pvsyst which are fully and publicly documented. Some differences between Solar Performance Insight and Pvsyst output are to be expected. Users must provide parameters for the module model. Because the Pvsyst inverter model is not fully and publicly documented, Solar Performance Insight substitutes the Sandia Inverter Model that is used in [SAM](#SAM), giving users the option to select inverter parameters from a database.

### PVWatts {#pvwatts}

Cacluate system output consistent with the (PVWatts)[https://pvwatts.nrel.gov] application. With the exception of the module temperature model, the 'pvwatts' model calculates system output using the same methods as does the PVWatts website. For the module temperature model, Solar Performance Insight uses the Sandia temperature model in place of a more complex calculation used by PVWatts.

### SAM {#SAM}

Calculate system output consistent with the PV performance model in the [System Advisor Model (SAM)](https://sam.nrel.gov). The 'SAM' model calculates system output using many, but not all, of the steps implemented in the SAM application. Users have access to databases of module and inverter model parameters that support the models implemented in SAM.

## System components

A system is represented by one or more [inverters](#inverter), each with one or more [arrays](#array).

### Inverters {#inverter}

Each inverter is assigned a unique name and (optionally) a make and model.

Inverter Parameters are the values needed for the function that calculates output AC power from input DC power and DC voltage. For the 'pvsyst-like' and 'SAM' performance models, the Sandia Inverter Model is used and users have the option to select inverter parameters from a database. For the 'pvwatts' performance model, Solar Performance Insight offers the PVWatts inverter model parameters as default values.

For the 'pvwatts' performance model only, a set of Loss Parameters may be entered. Each parameter is a percentage of AC power lost due to a category of effects (e.g., soiling, snow, mismatch). Solar Performance Insight offers the PVWatts loss factors as default values.

### Arrays {#array}

Each array is assigned a unique name.

Arrays can be Fixed, at constant Tilt and Azimuth, or on Single Axis trackers. Single axis trackers are defined by the tilt and azimuth of the tracker axis. All modules in an array are at the same orientation.

The modules in an array are considered to be arranged in series-connected strings, each string containing the same number of modules. The albedo of the ground surface can be selected from a list of representative values or manually entered.

Module parameters are required for the model that calculates module output. For the [SAM](#SAM) performance model only, a database of module parameters is available.

Temperature model parameters are required for the model that calculates module temperature from weather data. The temperature model is specific to each performance model:

- for 'pvsyst-like', the temperature model is the same as used in Pvsyst.
- for 'pvwatts', the temperature model is the Sandia model, rather than the more complex calculation used in PVWatts.
- for 'SAM', the temperature model is the default temperature model in SAM.


## Calculate performance {#calculateperformance}
{: .anchor}

## Compare performance {#calculateperformance}
{: .anchor}

## API {#api}
{: .anchor}
