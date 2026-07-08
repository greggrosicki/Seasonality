# Seasonal Variation in Cardiac Autonomic Function

Analysis code for the manuscript:

> **Age Moderates Seasonal Variation in Cardiac Autonomic Function: A Wearable Study of 16,415 Adults.**

This repository contains the analysis script used to characterize seasonal variation in
resting heart rate (RHR) and heart rate variability (HRV) in a cohort of U.S. adults using
one year of continuous wearable data, and to evaluate behavioral (physical activity, sleep)
and individual (age, sex, BMI, habitual physical activity) moderators of seasonal amplitude.

## Contents

| File | Description |
|------|-------------|
| `Seasonality_24_June_2026.Rmd` | Full analysis: data preparation, seasonal modeling (GAM/GAMM), individual- and mixed-effects analyses, behavioral and photoperiod adjustment, moderation analyses, and figure generation. |

## Data availability

The participant data are **not** included in this repository due to intellectual property
considerations of WHOOP, Inc. Deidentified participant data and a data dictionary may be made
available upon reasonable request to WHOOP (research@whoop.com), subject to a methodologically
sound proposal approved by WHOOP's research team and a signed data use agreement. The code is
provided for transparency and reproducibility of the analytical methods.

## Methods overview

- **Outcomes:** monthly aggregated RHR and HRV, person-mean centered.
- **Seasonal models:** generalized additive models (GAMs) with cyclic cubic splines across
  calendar months; generalized additive mixed-effects models (GAMMs) with participant random
  intercepts on a stratified subsample; individual-level August−December amplitude; and linear
  mixed-effects models of raw values for group × month interactions.
- **Inference:** 1,000 participant-level bootstrap resamples for amplitude differences;
  estimated marginal means with Holm-adjusted pairwise contrasts.
- **Behavioral / environmental adjustment:** between- and within-person components of physical
  activity and sleep; photoperiod (annual daylight amplitude by state-centroid latitude) with
  standard errors clustered by state.

## Requirements

- R (version 4.4.2)

Install the required packages:

```r
install.packages(c(
  "broom", "car", "dplyr", "emmeans", "ggbeeswarm", "ggfortify", "ggpattern",
  "ggplot2", "ggpp", "ggpubr", "ggsignif", "glue", "gratia", "haven", "hms",
  "itsadug", "lme4", "lmerTest", "lmtest", "lubridate", "metR", "mgcv",
  "patchwork", "purrr", "readr", "sandwich", "scales", "sjstats", "stringr",
  "tidyr", "visreg"
))
```

## Usage

The analysis is an R Markdown document. With the source data available locally, render it with:

```r
rmarkdown::render("Seasonality_24_June_2026.Rmd")
```

or open it in RStudio and knit. File paths to the source data must be set to your local
environment.

## Citation

If you use this code, please cite the associated manuscript (citation to be updated upon
publication).
