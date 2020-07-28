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

*Predicted performance* refers to PV system energy output using the same modeling assumptions
 and weather data as were used in pre-operational performance projections.
*Expected performance* refers to PV system energy output by the SPI Performance Model using
user supplied modeling assumptions and actual weather data.
*Actual performance* refers to the observed energy output of the PV system over a specific period of time.

## Use Cases {#usecases}

### 1. Calculate Performance {#calculateperformance}

#### 1.A. Calculate predicted performance {#uc1a}

**Use case narrative**: Using an SPI Performance Model (5.0) with user-provided modeling assumptions,
user input system metadata (6.0), and user supplied weather data (7.0), calculate system output.

**Requirements**:

- User can upload original modeling assumptions (5.0).
- User can upload system metadata (6.0).
- User can upload original weather data (7.A).
- Framework executes the performance model.
- Framework provides a report for download, or returns model output via the API.

#### 1.B. Calculate expected performance {#uc1b}

**Use case narrative**: Using the SPI Performance Model (5.0) with user-provided modeling assumptions,
user input system metadata (6.0), user-uploaded actual weather data (7.C) and user-selected data quality checks (X.0),
calculate system output.

**Requirements**:
- User can upload modeling assumptions (5.0)
- User can upload system metadata (6.0)
- User can upload actual weather data (7.C).
- User can select data quality checks to be applied to uploaded weather data.
- Framework applies data quality checks.
- Framework executes the performance model.
- Framework provides a report for download, or returns model output via the API.

#### 1.C. Account for snow and soiling {#uc1c}

**Use case narrative**: Snow and soiling are two key, user-identified external factors that affect
 actual performance and should be accounted for by SPI performance models. The platform should be
 able to accept snow or soiling data, or data from which quantities for modeling snow
 and soiling effects can be inferred (8.0)

**Requirements**:
- User uploads snow/soiling data.
- Framework translates user data to factors affecting modeled performance.


## 2. Compare Performance {#compareperformance}

## 3. Analyze Performance {#analyzeperformance}

## 4. Evaluate Sensors {#evaluatesensors}

