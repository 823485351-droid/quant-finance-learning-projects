# Quantitative Finance Learning Projects

This repository contains two independent quantitative finance projects developed for learning and portfolio demonstration purposes.

## Project 1: Monte Carlo Option Pricing

This project implements Monte Carlo pricing for European and binary call options under a risk-neutral geometric Brownian motion framework. It includes analytical Black-Scholes benchmarks, Euler-Maruyama and Milstein discretization schemes, sensitivity analysis, and antithetic variates for variance reduction.

## Project 2: Machine Learning for Market Direction Prediction

This project builds a supervised machine learning workflow for short-term market direction prediction using publicly available market data. The workflow includes data collection, exploratory data analysis, data cleaning, feature engineering, model training, evaluation, and signal-based backtesting.

## Project 3: Leakage-Controlled Blending Ensemble for Market Direction Forecasting

This project develops a rigorous machine-learning workflow for next-day SPY
direction forecasting. It combines chronological walk-forward validation,
feature-leakage controls, Optuna hyperparameter optimisation, multiple base
learners, soft-voting and logistic-blending ensembles, a locked final holdout,
economic benchmarking, and block-bootstrap uncertainty analysis.

Although several models improved during development, the advantage did not
survive the locked 2024–2025 final test. The project therefore highlights the
importance of honest out-of-sample evaluation and uncertainty quantification
in financial machine learning.

[View the project](./market-direction-blending-ensemble/)

## Disclaimer

This repository contains independent implementations for learning and portfolio demonstration purposes. It does not include proprietary exam questions, official solutions, lecture slides, or restricted datasets.
