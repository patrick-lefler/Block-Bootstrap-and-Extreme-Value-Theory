# Block-Bootstrap-and-Extreme-Value-Theory

The R Quarto output can be found here: https://patrick-lefler.github.io/Block-Bootstrap-and-Extreme-Value-Theory/

![R](https://img.shields.io/badge/Language-R-blue)
![Library](https://img.shields.io/badge/Framework-Boot-orange)
![Framework](https://img.shields.io/badge/Framework-EVD-red)
![Report](https://img.shields.io/badge/Format-Quarto-green)

This project contains the technical framework and narrative summary for "Coding the Tail: Implementing Block Bootstrap and EVT in R." It provides a practical demonstration of how to quantify tail risk in high-volatility assets (specifically Bitcoin) using advanced statistical methods that outperform standard Gaussian models. 

### Summary 

Moving from strategic risk philosophy to hard-coded implementation.
This project argues that standard risk models (Value at Risk based on Normal distribution) are dangerously inadequate for crypto assets due to two structural features:
1. Volatility Clustering: "Bad days" tend to follow other "bad days."
2. Fat Tails: Extreme events occur with far greater frequency than a Bell Curve predicts.

The project guides the reader through two specific R implementations designed to capture these nuances using historical Bitcoin data from 2021 through 2025. It contrasts the comfortable lies of the Normal distribution with the uncomfortable truths revealed by the Block Bootstrap and Extreme Value Theory (EVT).

### Technical Implementation (R Code)
The provided R script performs a dual-track risk analysis on the btc_daily_prices_2021-2025.csv dataset.
1. Data Preprocessing
* Input: Daily closing prices of BTC.
* Transformation: Converts prices to Daily Log Returns to ensure stationarity and additivity.
* Cleaning: Sorts chronologically to preserve time-series integrity.
2. Method A: The Block Bootstrap
* Objective: To estimate the 99% Value at Risk (VaR) while preserving the autocorrelation (volatility clustering) of the time series.
* Technique: Instead of random resampling (which destroys time structure), the script resamples 20-day contiguous blocks of returns.
* Comparison: It calculates the standard Normal VaR versus the Bootstrapped VaR to quantify the "Risk Gap."
3. Method B: Extreme Value Theory (EVT)
* Objective: To model the behavior of the extreme tail and extrapolate potential losses beyond historical maximums.
* Technique: Uses the Peaks Over Threshold (POT) method.
* Threshold: Sets the threshold at the 95th percentile of losses.
* Distribution: Fits a Generalized Pareto Distribution (GPD) to the excesses above this threshold.
* Metric: Calculates the 100-Day Return Level (the magnitude of loss expected to be exceeded once every 100 days).

### Key Findings (Based on 2021-2025 Data)
The analysis reveals a significant underestimation of risk by standard models:
1. The Risk Gap:
* Normal Distribution Prediction (99% VaR): -7.09%
* Block Bootstrap Prediction (99% VaR): -8.77%
* Insight: The standard model underestimates the daily capital requirement by approximately 1.7%, a critical margin for leveraged portfolios.
2. The Tail Shape:
* Shape Parameter ($\xi$): 0.061
* Insight: A positive shape parameter confirms the distribution is heavy-tailed (infinite variance potential), invalidating models that assume exponential decay.

### Dependencies
The analysis utilizes the following R libraries:ggplot2 (Visualization)dplyr (Data manipulation)boot (Bootstrapping functions)evd (Extreme Value Distributions)
