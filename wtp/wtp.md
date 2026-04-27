---
layout: default
title: Air Quality Forecasting WTP
description: Which variables predict demand for air quality forecasting? Households in Lahore, Pakistan are exposed to forecasts attributed to either a government or citizen-run source, and their willingness to pay for each is measured.
permalink: /aq-wtp
---

**Type:** Faculty-Supervised Research Project &nbsp;|&nbsp; **Tools:** R &nbsp;|&nbsp; **Year:** 2025–2026

---

## Overview

Air pollution is a severe public health crisis in Lahore, Pakistan, with documented negative effects on health and education. This project analyzes data from a randomized controlled trial studying household willingness to pay (WTP) for air quality forecasting services. The central question: **which variables predict WTP, and how much does the source of a forecast matter?**

Households were randomly assigned to receive identical air quality forecasting SMS texts attributed to one of two sources:
- **EPD** (Environmental Protection Department) — a government agency
- **PAQI** (Pakistan Air Quality Initiative) — a citizen-run organization

Because the forecast content was identical, any difference in WTP between groups can be attributed entirely to the source attribution. The analysis covered 929 households across two geographic areas (Shalamar and City Center tehsils).

This project began as a broad, exploratory effort to identify predictors of WTP. It evolved into an investigation of treatment effects after the data made clear that source attribution was the dominant driver of relative preferences.

---

## Methods

The analysis used multiple complementary statistical approaches to let the data guide findings rather than testing pre-specified hypotheses.

**Data Cleaning**
Before modeling, the data underwent a careful cleaning pipeline: outlier removal (Z-score threshold of 4), dropping variables with near-zero variation, median/mode imputation for missing data, VIF-based multicollinearity checks, and leverage-based observation removal (hat values ≥ 0.99) to ensure numerical stability in robust standard error estimation.

**Exploratory Variable Selection**
Three approaches were applied in parallel to identify predictors of absolute WTP:
- **OLS regression** with Benjamini-Hochberg multiple-comparison correction
- **Lasso** with 10-fold cross-validation and a 70/30 train-test split
- **Bayesian Spike-and-Slab** (10,000 MCMC iterations) for probabilistic variable selection

**Treatment Effect Analysis**
After the exploratory phase revealed that relative WTP (WTP for PAQI minus WTP for EPD) was far more predictable than absolute WTP, the focus shifted to quantifying the treatment effect. OLS models used standard errors clustered by geographic grid cell (`grid_id`) to account for within-neighborhood correlation. Logistic regression was used to analyze binary preference outcomes.

**Heterogeneous Treatment Effects**
Causal forests (via the `grf` package, 4,000 trees with honest splitting) were used to identify which household characteristics moderate the treatment effect. Best linear projection provided interpretable summaries of continuous moderators.

<img src="/wtp/wtp_by_treatment.png" alt="WTP by Treatment Group" style="max-width:100%;">
<p><em>Violin plots of WTP by treatment group. The relative WTP panel (left) shows clear separation between groups; absolute WTP panels show substantial overlap — consistent with treatment shifting preferences between services rather than overall spending.</em></p>

---

## Key Findings

**Source attribution dominates relative preferences — and the effect is very large.**

The treatment (EPD vs. PAQI attribution) alone explains **42.4% of variance** in relative WTP. All demographic, behavioral, and household variables combined explain only **7.1%** — roughly 6× less. Adding those covariates to the treatment model raises R² by only 3.6 percentage points.

The treatment coefficient is approximately **−32 PKR**: households assigned to EPD attribution are willing to pay 32 PKR more for EPD relative to PAQI than households assigned to PAQI attribution. Standardized, this is a **Cohen's d of 1.71** (95% CI: [1.56, 1.86]) — more than twice the conventional threshold of 0.8 for a "large" effect, and stable across 1,000 bootstrap samples (mean −32.2 ± 1.6 PKR).

<img src="/wtp/treatment_effect_distr.png" alt="Treatment Effect Distributions" style="max-width:100%;">
<p><em>Density distributions of relative WTP shifted by the estimated treatment effect. The clear separation illustrates that the treatment-induced preference gap exceeds the natural variation in preferences across the population.</em></p>

**Treatment does not affect absolute or total WTP.**

Treatment explains less than 2% of variance in absolute WTP for either service, and essentially zero variance in total WTP (R² ≈ 0, p = 0.831). Source attribution shifts *which* service households prefer, but not how much they are willing to spend overall on air quality forecasting.

**Few variables consistently predict absolute WTP.**

No demographic, economic, or behavioral variable robustly predicts absolute WTP across treatment groups. This negative finding is consistent across OLS, Lasso, and Spike-and-Slab, strengthening confidence that it is not a modeling artifact.

**Machine learning variable selection did not outperform OLS.**

Lasso either matched or underperformed standard OLS. For relative WTP, OLS achieved R² = 0.609–0.669 versus Lasso's 0.558–0.648. Regularization and automated variable selection offered no advantage here.

**Treatment effects vary systematically by income, location, and prior attitudes.**

Causal forests revealed meaningful heterogeneity. The top moderators and their share of treatment effect variation:

| Variable | Importance | Interpretation |
|:---------|:----------:|:---------------|
| Work hours (income proxy) | 35.6–36.1% | Higher income → stronger EPD preference when treated with EPD |
| Geographic location (tehsil) | 12.4–13.7% | Shalamar shows larger effects than City Center |
| Baseline government approval | 5.8–8.1% | Prior trust moderates receptiveness to EPD attribution |

Together, these three variables explain approximately **54–58% of treatment effect variation**.

<img src="/wtp/var_importance_vertical.png" alt="Variable Importance — Causal Forest" style="max-width:100%;">
<p><em>Variable importance rankings from causal forest analysis. Work hours is the dominant moderator, consistent with its role as an income proxy and domain knowledge linking lower income to lower government trust in Pakistan.</em></p>

<img src="/wtp/work_hrs_whitebg.png" alt="Treatment Effect by Work Hours" style="max-width:100%;">
<p><em>Treatment effect by work hours quartile. Households working more hours (higher income) show larger preference shifts toward EPD when exposed to EPD forecasting. Error bars are 95% confidence intervals.</em></p>

**Binary preferences show near-perfect separation.**

Logistic regression predicting binary EPD vs. PAQI preference found near-complete separation: EPD-treated households have approximately a 97% probability of preferring EPD; PAQI-treated households have approximately a 5% probability of preferring EPD.

<img src="/wtp/log_odds_plot.png" alt="Log-Odds Plot" style="max-width:100%;">
<p><em>Predicted probability of preferring EPD over PAQI by treatment group, with 95% confidence intervals.</em></p>

---

## Policy Implications

- **Expanding access to government air quality forecasting may be more effective than expected.** Source attribution alone — with identical content — generates a preference shift with a Cohen's d of 1.71. Free trials or subsidized access to EPD forecasting could durably shift household preferences toward the government service, potentially at low cost.

- **The mechanism appears to be preference formation, not demand creation.** Because treatment does not increase total WTP, the implication is that people already have a budget for this type of service; exposure changes which provider they allocate it to. Communication campaigns focused on awareness may be sufficient to redirect preferences.

- **Targeting strategies should account for heterogeneity.** Higher-income households (proxied by work hours) and those with positive baseline government approval respond most strongly to EPD-attributed forecasting. Lower-income households and those with lower government trust may require different messaging — or may be better served by a citizen-run provider like PAQI that does not rely on government credibility.

- **Geographic variation warrants attention.** Shalamar and City Center show meaningfully different treatment effect magnitudes, suggesting that uniform communication strategies may not be optimal across different urban sub-areas.

---

## Limitations

- **No direct income variable.** Work hours is used as an income proxy. The relationship between hours worked and income is imperfect, and the work hours variable may capture factors beyond income (e.g., time constraints, sector of employment).

- **Stated WTP may not reflect actual behavior.** The BDM (Becker-DeGroot-Marschak) elicitation mechanism is designed to be incentive-compatible, but respondents' stated valuations in a survey context may still deviate from real purchasing decisions.

- **Large treatment effect warrants scrutiny.** An effect of this magnitude is rare in social science. A plausible concern is that respondents without strong prior preferences may anchor their WTP responses almost entirely to the most salient cue available — source attribution — rather than reflecting stable underlying preferences. If so, the effect may reflect anchoring rather than genuine preference formation, which could limit its persistence over time.

- **Limited external validity.** The study is conducted in two tehsils of Lahore — a large, heavily polluted urban center. Findings may not generalize to smaller cities, rural areas, or different national contexts.

- **Selective inference was not feasible.** Post-selection inference via the Fixed Lasso method could not be included because package assumptions were not met and the package is no longer actively maintained.

- **Self-reported data.** Attitudinal measures (government approval, air pollution concern) are self-reported and subject to social desirability bias.

---

## Code

Full code available on [GitHub](https://github.com/teo-richard/ucd_aq_proj).

*Data access: The underlying survey data is private. The code in this repository will not run without access to the original data, which was provided by Professor Arman Rezaee (Department of Economics, UC Davis).*
