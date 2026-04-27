---
layout: default
title: Energy Poverty Project
description: "In progress: Investigating which households will be at risk of falling into energy poverty as the climate changes."
permalink: /energy
---

**Type:** Faculty-Supervised Research Project &nbsp;|&nbsp; **Tools:** Python (polars) &nbsp;|&nbsp; **Year:** 2026

---

## Overview

I would like to see which households are going to be at risk of falling into energy poverty as global climates shift and change. I am using NOAA data for current climate data and CMIP6 LOCA2 data at SSP4.5-7 for climate projections. I will merge this data with the American Housing Survey.

## Background

While this is mostly descriptive, it is quite important for policy because it will answer which households need more attention as temperatures change. 

## Methods

Train LightGBM and XGBoost model using AHS + current climate data. I am doing both trees as a simple sanity check as they should return about the same results. Then predict energy poverty using these models and projected climate.

## Key Findings

TBD

## Policy Implications

TBD

## Code

Full code will be available on [GitHub](https://github.com/teo-richard).
