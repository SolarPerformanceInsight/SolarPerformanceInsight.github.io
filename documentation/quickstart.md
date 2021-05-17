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

1. Define or select the [system](#definesystem)
2. Choose a workflow:
   - [Calculate performance](#calculateperformance)
   - [Compare performance](#compareperformance)

## Systems {#system}
{: .anchor}

A PV system is defined by four sets of data:

1. The [performance model](#performancemodel) defines the sequence of models to be used to calculate output of the system. Options are [pvsyst-like](#pvsyst), [pvwatts](#pvwatts) and [SAM](#SAM).
2. System metadata, including:
   - name
   - latitude and longitude. Use decimal degress (e.g., 35.5) without a direction character (e.g. N, E) and use negative longitude for locations west of the prime meridian.
   - elevation above mean sea level in meters
3. [Inverters] (#inverter). A system can have one or more inverters. The options for inverter parameters depend on the performance model.
4. [Arrays] (#array). An array is a collection of modules with the same fixed or tracking orientation. One or more arrays can be associated with each inverter. Array parameters depend on the performance model.


## System performance models {#performancemodel}
{: .anchor}

Solar Performance Insight uses functions from [pvlib](https://github.com/pvlib/pvlib-python.git) to calculate system output consistent with the selected performance model: [pvsyst-like](#pvsyst), [pvwatts](#pvwatts) and [SAM](#SAM).

### Pvsyst-like model {#pvsyst}
{: .anchor}

Calculate system output consistent with the [Pvsyst](https://www.pvsyst.com) software package. The 'pvsyst-like' model includes only those steps in a Pvsyst which are fully and publicly documented. Some differences between Solar Performance Insight and Pvsyst output are to be expected. Users must provide parameters for the module model. Because the Pvsyst inverter model is not fully and publicly documented, Solar Performance Insight substitutes the Sandia Inverter Model that is used in [SAM](#SAM), giving users the option to select inverter parameters from a database.

### PVWatts {#pvwatts}
{: .anchor}

Calculate system output consistent with the [PVWatts](https://pvwatts.nrel.gov) application. With the exception of the module temperature model, the 'pvwatts' model calculates system output using the same methods as does the PVWatts website. For the module temperature model, Solar Performance Insight uses the Sandia temperature model in place of a more complex calculation used by PVWatts.

### SAM {#SAM}
{: .anchor}

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

This workflow runs the performance model for the system using the weather you upload. Weather includes irradiance and temperature data, and can be uploaded once for the full system, by inverter, or by array.

### Upload Weather Data {#weatherdataupload}
{: .anchor}

Irradiance data must contain one of the following combinations:
- global horizontal (GHI), direct normal (DNI) and diffuse horizontal (DHI) irradiance. If your data includes only GHI and DHI, you can estimate DNI using a model; see pvlib's [dni](https://github.com/pvlib/pvlib-python/blob/master/pvlib/irradiance.py#L2844) function for example.
- global plane-of-array (POA), direct POA, and diffuse POA irradiance. If your data includes only global POA, consider using the option below instead.
- global POA (not adjusted for reflections or spectral content) or effective irradiance (adjusted for reflections and spectral content). Typically, global POA is measured with a pyranometer mounted in the array plane, and effective irradiance is measured with a reference cell.

_Cell temperature_ is the temperature of the cells inside the array's modules. This quantity is rarely measured, but if it has been determined, you can upload it with your weather data.

_Module temperature_ is the temperature on the outside module surface, and is often measured with an attached temperature sensor. 

If your data doesn't include _module temperature_, you can upload _air temperature_ (and optionally, _wind speed_) and Solar Performance Insight will calculate cell temperature using a model.

Weather data must include a _datetime index_ that is localized to the timezone. Localizing the index to the timezone avoids common pitfalls such as daylight savings hour shifts. Solar Performance Insight assumes that the datetime index has a fixed time spacing, in whole minutes.

After you choose the file containing weather data for upload, Solar Performance Insight guides you through matching the columns in the data to the weather variables expected for the calculation.

When matching is complete, the **Upload Data** button completes the data upload and queues the model calculation.

### Calculation Results

Results are summarized by month. Summary results include:
- _Total Energy_ is total electrical energy.
- _Plane of Array Insolation_ is total broadband solar insolation summed over all arrays.
- _Effective Insolation_ is total solar insolation, adjusted for reflections and spectral content, summed over all arrays.
- _Average Daytime Cell Temperature_ is averaged over all arrays and times when the sun is above the earth's horizon.

Detailed output can be downloaded in CSV or Arrow formats.

Solar Performance Insight can make plots of time series of uploaded data and/or model results - click the **New Plot** button.  


## Compare Performance {#compareperformance}
{: .anchor}

This workflow compares actual power (which you upload) to _reference_ or _modeled_ power. _Reference_ power is a record of modeled output from the system, usually done as part of the system design. _Modeled_ power is calculated by Solar Performance Insight from the weather data which you upload; see the [Calculate Performance](#calculateperformance) workflow for details.

### Compare Actual to Reference Performance

Comparison calculates the ratio and difference between monthly actual energy and monthly reference energy that is adjusted for the differences between actual and reference weather. The comparison can be done with data at hourly or better resolution, or using monthly totals.

#### Comparing actual and reference with hourly data

The adjustment of reference power accounts for the differences in irradiance and temperature at each timestemp.

Case 1. When reference data includes DC power and weather, the adjusted reference AC power is calculated as

P<sub>AC, adj</sub> = min {P<sub>AC0</sub>, 0.985 P<sub>DC, adj</sub>}
P<sub>DC, adj</sub> = P<sub>DC, ref</sub> (POA<sub>actual</sub> / POA<sub>ref</sub>) F<sub>tem</sub>
F<sub>tem</sub> = (1 - &gamma; (T<sub>cell, actual</sub> - 25)) / (1 - &gamma; (T<sub>cell, ref</sub> - 25))

P<sub>AC0</sub> is the total AC capacity of the PV and &gamma; is the temperature coefficient of power provided in the PV system metadata. The factor of 0.985 accounts for the DC to AC conversion efficiency.

Case 2. When reference data includes AC power and weather (DC power is not available), the adjusted reference AC power is calculated as

P<sub>AC, adj</sub> = min {P<sub>AC0</sub>, P<sub>AC, ref</sub> (POA<sub>actual</sub> / POA<sub>ref</sub>) F<sub>tem</sub>}
F<sub>tem</sub> = (1 - &gamma; (T<sub>cell, actual</sub> - 25)) / (1 - &gamma; (T<sub>cell, ref</sub> - 25))

Case 3. When reference data includes only weather, Solar Performance Insight first runs the PV system performance model (provided with the system metadata) to estimate P<sub>DC, ref</sub>. Then, adjusted reference AC power is calculated as described above for Case 1.

#### Comparing actual and reference with monthly data

When reference data are at monthly resolution, the weather data must include plane-of-array (POA) insolation POA<sub>ref</sub>, average daytime cell or module temperature T<sub>avg, ref</sub>, and total AC energy E<sub>AC, ref</sub>. The adjusted reference AC energy for each month is calculated by

E<sub>AC, adj</sub> = E<sub>AC, ref</sub> (POA<sub>actual</sub> / POA<sub>ref</sub>) - L<sub>tem</sub>}
L<sub>tem</sub> = (P<sub>AC0</sub> / 1000) POA<sub>act</sub> &gamma; (T<sub>avg, actual</sub> - T<sub>avg, ref</sub>)

The equation above derives from a simple energy performance model:

E = (P<sub>AC0</sub> / 1000) POA (1 - &gamma; (T<sub>avg</sub> - 25)


### Upload Actual and Reference Performance Data

_Actual_ data includes AC power and actual weather data for the entire system or per inverter. Options for _reference_ data include:
- weather data only, in which case Solar Performance Insight runs the performance model to calculate reference power.
- weather and AC power data. In this case, the reference and actual weather data are used to adjust the reference AC power to the actual weather conditions.
- weather, AC and DC power data. In this case, the reference and actual weather data and the reference DC power are used to adjust the reference AC power to the actual weather conditions.

See [Upload Weather Data](#weatherdataupload) for data upload details.


## API {#api}
{: .anchor}
