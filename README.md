# Seasonal Variation in Cardiac Autonomic Function

Analysis code for the manuscript:

> **Seasonal Variation in Resting Heart Rate and Heart Rate Variability Is Attenuated With Advancing Age: A Year-Long Wearable Study of 16,415 U.S. Adults.**

This repository contains the analysis script used to characterize seasonal variation in
resting heart rate (RHR) and heart rate variability (HRV) in a cohort of U.S. adults using
one year of continuous wearable data, and to evaluate behavioral (physical activity, sleep
duration, sleep consistency, sleep efficiency), physiological (nocturnal respiratory rate),
environmental (photoperiod, temperature), and individual (age, sex, BMI, habitual physical
activity) contributors to and moderators of seasonal amplitude.

## Contents

| File | Description |
|------|-------------|
| `Seasonality_21_Aug_2026.Rmd` | Full analysis: data preparation, seasonal modeling (GAM/GAMM), individual- and mixed-effects analyses, behavioral and physiological attenuation, geographic photoperiod and temperature analyses (state and city level), moderation and sensitivity analyses, and figure generation. |

External environmental inputs are not distributed here and can be obtained from their public
sources: statewide monthly mean temperature from [NOAA nClimDiv](https://www.ncei.noaa.gov/access/monitoring/climate-at-a-glance/statewide/mapping)
(public domain); U.S. city geocodes from [kelvins/US-Cities-Database](https://github.com/kelvins/US-Cities-Database)
(MIT license); and city-level temperature exposures regenerated from the ERA5-based
[Open-Meteo Historical Weather API](https://open-meteo.com) (CC BY 4.0) using the
non-evaluated fetch chunk included in the Rmd.

## Data availability

The participant data are **not** included in this repository due to intellectual property
considerations of WHOOP, Inc. Deidentified participant data and a data dictionary may be made
available upon reasonable request to WHOOP (science@whoop.com), subject to a methodologically
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
- **Behavioral / physiological adjustment:** between- and within-person components of physical
  activity, sleep duration, sleep consistency, sleep efficiency, and nocturnal respiratory rate.
- **Geographic analyses:** annual photoperiod amplitude (state-centroid latitude), statewide
  temperature amplitude and August mean temperature (NOAA nClimDiv), and a city-level
  sensitivity analysis using geocoded city of residence with ERA5-based exposures; standard
  errors clustered by state (conservative) and, for city-level models, also by city.
- **Sensitivity analyses:** 10-year age bands, sex-by-age interactions, December−January
  winter reference, and age-stratified moderation models.

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

The analysis is an R Markdown document. Set `BASE_DIR` (defined near the top of the setup
chunk) to your local project directory containing the source data and the external input
files described above, then render:

```r
rmarkdown::render("Seasonality_21_Aug_2026.Rmd")
```

or open it in RStudio and knit. Note that the attenuation and moderation analyses use
1,000 participant-level bootstrap resamples; a full render takes several hours.

## Citation

If you use this code, please cite the associated manuscript (citation to be updated upon
publication).
