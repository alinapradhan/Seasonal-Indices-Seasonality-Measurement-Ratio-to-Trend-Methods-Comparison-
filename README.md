
# Seasonal Indices & Seasonality Measurement (Ratio-to-Trend & Methods Comparison)

## Overview
This repo demonstrates how to compute seasonal indices using the Ratio-to-Trend method and how to measure/detect seasonality in a time series using several standard approaches. The provided R script  contains two main parts:

1. Manual computation of seasonal indices for quarterly data using the Ratio-to-Trend method.
2. Seasonality measurement and visualization on the AirPassengers dataset using:
   - Classical decomposition (additive and multiplicative)
   - STL decomposition
   - ACF and PACF plots for seasonality detection

## Files
- prac 5.R
  - Implements the Ratio-to-Trend method for a sample quarterly sales series and demonstrates decomposition and seasonality analysis for the AirPassengers dataset.
- README.md
  - This file: documentation and usage instructions.

## Purpose
The objectives are:
- Teach how to compute seasonal indices manually by fitting a trend, computing ratios to the trend, grouping by period (quarter), and normalizing indices.
- Illustrate and compare seasonality detection and decomposition approaches (classical additive/multiplicative decomposition, STL) and diagnostic tools (ACF/PACF).

## Methods implemented
- Ratio-to-Trend (manual seasonal indices):
  - Fit a linear trend to the series.
  - Compute ratio-to-trend = (observed / trend) * 100 for each observation.
  - Group ratios by quarter and compute average ratios per quarter.
  - Adjust seasonal indices so that their mean equals 100.
  - Plot observed series with fitted trend and a barplot of adjusted seasonal indices.
- Classical decomposition:
  - Use `decompose()` for additive and multiplicative seasonal decompositions on the AirPassengers series and print seasonal components.
- STL decomposition:
  - Use `stl()` with a periodic seasonal window to extract trend, seasonal and remainder components; print the seasonal component.
- ACF & PACF:
  - Plot ACF and PACF (lags up to 48) for the AirPassengers series to help detect periodicity/seasonality.

## How to run

From an R console or RStudio:
- Source the script:
  source

Or from a shell:
- Run with Rscript:
  Rscript 

## Dependencies
The script uses only base R functions and datasets; no additional CRAN packages are required. The example uses the built-in AirPassengers dataset.

If you adapt the script to different smoothing or plotting libraries, you may need packages such as:
- forecast (for additional decomposition/forecasting utilities)
- ggplot2 (for enhanced plotting)

Install any needed packages with:
install.packages(c("forecast", "ggplot2"))

## Expected output
- For the Ratio-to-Trend section:
  - Console output showing fitted trend values, the ratio-to-trend table, and the adjusted seasonal indices (Q1–Q4).
  - Two plots: (1) observed series with fitted trend, (2) barplot of seasonal indices by quarter.
- For the AirPassengers analysis:
  - Plots from `decompose()` for additive and multiplicative decompositions.
  - `stl()` plot showing seasonal, trend and remainder components.
  - Console printing of the seasonal components (vectors).
  - ACF and PACF plots showing autocorrelations and partial autocorrelations up to lag 48.

## Notes and interpretation
- Ratio-to-Trend:
  - Works well when a simple trend captures the underlying non-seasonal movement.
  - Assumes multiplicative seasonal behavior is captured by ratios to trend (hence the multiplication by 100).
  - The adjusted indices are scaled so their mean equals 100 — interpret values above 100 as above-trend seasonal peaks and below 100 as below-trend troughs.
- Classical decomposition:
  - `decompose()` requires an appropriate `ts` frequency. If frequency is incorrect, seasonal estimates will be wrong.
  - Additive vs multiplicative: multiplicative is more appropriate when seasonality magnitude changes with level.
- STL:
  - More robust and flexible than classical decomposition; handles changing seasonality and allows custom seasonal smoothing.
- ACF/PACF:
  - Strong spikes at seasonal lags (e.g., multiples of 12 for monthly series) indicate seasonality.
  - Use these diagnostics together with decomposition plots for a fuller picture.

## Troubleshooting
- If seasonal components from `decompose()` are mostly NA, check that the `ts` object's frequency matches the true seasonal period.
- If linear trend is a poor fit, consider fitting polynomial trends or using a smoother (loess) before computing ratios.
- If plots overlap or appear crowded, increase plotting device size or save to a file using png()/pdf().

## Suggested next steps
- Visualize residuals (remainder) from each decomposition method to check for autocorrelation or heteroskedasticity.
- Compute and compare seasonal indices using alternative approaches (e.g., centered moving averages, STL-based indices) and quantify differences.
- Use the derived indices to seasonally adjust the series and then fit forecasting models (ARIMA, ETS) on the seasonally adjusted data.

## License & Contact
This practical material is provided for educational use. For questions or suggestions, contact the author or the repository maintainer.

```
