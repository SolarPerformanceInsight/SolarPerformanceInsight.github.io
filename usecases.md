---
layout: base
permalink: /usecases/
sidebar: usecase_sidebar.html
title: Use Cases
---

{% include to_top.html %}

## Purpose and Summary {#purpose}
{: .anchor }
This document presents use cases and and functional requirements for the Solar Performance
Insight (SPI) platform. A use case describes a sequence of actions to achieve a goal. A functional
requirement is a feature or capability of the platform that supports the use cases.

These cases are derived from User Stories extracted from interviews and communications with solar
O&M industry professionals (system owners, engineers, asset managers, and O&M providers). The SPI
Project Team identified four categories of use cases prioritized by the frequency with which they
appeared in user stories and by consistency with the scope of the award that funds this work.

The use case categories are:

1. [Calculate Performance](#calculateperformance).
2. [Compare Performance](#compareperformance).
3. [Analyze Performance](#analyzeperformance).
4. [Evaluate Sensors](#evaluatesensors).

{:start="5"}
Framework functional capabilities include:
5. Provide performance models
6. Import assumptions used in original modeling
7. Import weather data from various sources
8. Import snow/soiling data
9. Import actual system performance data
10. Import  data from on-site sensors
11. Import irradiance data
12. Administer the framework
13. Archive data

## Definitions

**Predicted performance** refers to PV system energy output using the same modeling assumptions
 and weather data as were used in pre-operational performance projections.

**Expected performance** refers to PV system energy output by the SPI Performance Model using
user supplied modeling assumptions and actual weather data.

**Actual performance** refers to the observed energy output of the PV system over a specific period of time.

## Use Cases {#usecases}

### 1. Calculate Performance {#calculateperformance}
{: .anchor}

#### 1.A. Calculate predicted performance {#uc1a}
{: .anchor}

**Use case narrative**: Using an SPI Performance Model (5.0) with user-provided modeling assumptions,
user input system metadata (6.0), and user supplied weather data (7.0), calculate system output.

**Requirements**:

- User can upload original modeling assumptions (5.0).
- User can upload system metadata (6.0).
- User can upload original weather data (7.A).
- Platform executes the performance model.
- Platform provides a report for download, or returns model output via the API.

#### 1.B. Calculate expected performance {#uc1b}
{: .anchor}

**Use case narrative**: Using the SPI Performance Model (5.0) with user-provided modeling assumptions,
user input system metadata (6.0), user-uploaded actual weather data (7.C) and user-selected data quality checks (X.0),
calculate system output.

**Requirements**:
- User can upload modeling assumptions (5.0)
- User can upload system metadata (6.0)
- User can upload actual weather data (7.C).
- User can select data quality checks to be applied to uploaded weather data.
- Platform applies data quality checks.
- Platform executes the performance model.
- Platform provides a report for download, or returns model output via the API.

#### 1.C. Account for snow and soiling {#uc1c}
{: .anchor}

**Use case narrative**: Snow and soiling are two key, user-identified external factors that affect
 actual performance and should be accounted for by SPI performance models. The platform should be
 able to accept snow or soiling data, or data from which quantities for modeling snow
 and soiling effects can be inferred (8.0)

**Requirements**:
- User uploads snow/soiling data.
- Platform translates user data to factors affecting modeled performance.

### 2. Compare Performance {#compareperformance}
{: .anchor}

#### 2.A Compare Predicted and Actual Performance {#uc2A}

**Use case narrative**: This use case assumes that the user has the original weather data
used to predict performance, and has the predicted performance retained from the original simulations
or has used an SPI model to calculate predicted performance (1.A) from the original weather data.
Comparing actual performance to predicted performance requires adjusting the actual performance for
the differences between actual weather and the weather conditions assumed for the predicted performance.

**Requirements**:
- User uploads weather data used for original performance predictions.
- User uploads recorded predicted performance or selects results of a Predicted Performance run (1.A).
- User uploads actual weather and actual performance.
- Platform adjusts actual performance to the irradiance and temperature of the predicted performance.
- Platform provides a report for download, or returns model output via the API.

#### 2.B. Compare Expected and Predicted Performance {#uc2B}

**Use case narrative**: This use case assumes that the user has the original weather data
used to predict performance, and has the predicted performance retained from the original simulations
or has used an SPI model to calculate predicted performance (1.A) from the original weather data.
The framework calculates expected performance from the actual weather. Comparing expected performance
to predicted performance requires adjusting the expected performance for the differences between
actual weather and the weather conditions assumed for the predicted performance.

**Requirements**:
- User uploads weather data used for original performance predictions.
- User uploads recorded predicted performance or selects results of a Predicted Performance run (1.A).
- User uploads actual weather.
- Platform calculates expected performance from actual weather and user-uploaded system metadata.
- Platform adjusts expected performance to the irradiance and temperature of the predicted performance.
- Platform provides a report for download, or returns model output via the API.

#### 2.C. Compare Actual and Expected Performance {#uc2C}

**Use case narrative**: This use case assumes that the user is able to upload actual performance and actual
weather data. The framework calculates expected performance from the actual weather. Calculated expected performance
provides a consistent reference for comparison with actual performance to help identify causes of under- or
over-performance in the actual weather conditions.

**Requirements**:
- User uploads actual weather and actual performance data.
- Platform calculates expected performance from actual weather and user-uploaded system metadata.
- Platform provides a report for download, or returns model output via the API.

#### 2.D. Calculate weather-adjusted performance ratio {#uc2D}

**Use case narrative**: An important metric of performance is the weather-adjusted performance ratio,
which is the ratio of actual to modeled energy accounting for irradiance and temperature. The model for energy
can vary in complexity from a simple linear model as described in [1], to PVWatts™ or PVsyst.

**Requirements**:
- User uploads actual performance (9.0).
- User uploads modeled performance, or uploads actual weather and selects an SPI performance model.
- If an SPI performance model is selected, platform calculates modeled performance from actual weather
  and user-uploaded system metadata.
- Platform calculates ratio of actual to modeled performance.

[1] Weather-Corrected Performance Ratio, T. Dierauf et al, NREL/TP-5200-57991, April 2013.

### 3. Analyze Performance {#analyzeperformance}
{: .anchor}

### 4. Evaluate Sensors {#evaluatesensors}
{: .anchor}

