# Leakage-Controlled Blending Ensemble for Market Direction Forecasting

## Overview

This project investigates whether engineered market features can provide a reliable out-of-sample signal for short-horizon market-direction forecasting.

The analysis uses daily SPY market data and a deliberately conservative machine-learning workflow built around chronological validation, fold-local preprocessing, leakage controls, model diversity, locked ensemble construction, one-time final-label release, economic benchmarking, and block-bootstrap uncertainty analysis.

The project is designed not only to search for predictive performance, but also to test whether apparent development-stage improvements survive a genuinely unseen final holdout period.

## Research Question

Can a leakage-controlled ensemble of linear, kernel-based, bagging, and boosting classifiers forecast next-day SPY return direction more reliably than random ranking and a passive buy-and-hold benchmark?

## Methodology

### Data and target

- **Asset:** SPY
- **Frequency:** Daily
- **Sample period:** 2014–2025
- **Target:** Indicator for a positive next-day return
- **Candidate features:** Returns and reversals, trend, momentum, volatility, volume and liquidity, intraday structure, and calendar effects

### Leakage and redundancy controls

The workflow includes:

- adjusted-price validation;
- chronological train/validation/test partitions;
- future-append invariance checks;
- structural-identity screening;
- correlation-based feature filtering;
- fold-local preprocessing and feature selection;
- frozen model, ensemble, and threshold decisions before final-label release;
- alignment and target-hash audits.

### Base models

Four model families are evaluated:

1. Elastic-net logistic regression
2. Calibrated radial-basis-function support-vector machine
3. Random forest
4. XGBoost

### Ensemble candidates

The project compares:

- equal-weight soft voting;
- development-skill-weighted voting;
- regularised logistic blending;
- XGBoost as a standalone benchmark.

### Validation design

Model development uses chronological walk-forward validation. Hyperparameters are selected with Optuna using development-stage data only.

A locked 2024–2025 final holdout is evaluated once after all modelling, ensemble, and classification-threshold decisions have been frozen.

## Main Findings

Development-stage optimisation improved the mean walk-forward ROC-AUC of several nonlinear models. The strongest development-stage result was obtained by XGBoost, with a mean ROC-AUC of approximately **0.545**.

The primary locked ensemble did not preserve this apparent advantage in the final holdout:

| Metric | Primary locked ensemble |
|---|---:|
| Final-test ROC-AUC | 0.489 |
| 95% block-bootstrap ROC-AUC interval | 0.442–0.533 |
| Balanced accuracy | 0.506 |
| Predicted positive rate | 0.974 |
| Annualised strategy return | 21.32% |
| Buy-and-hold annualised return | 21.70% |
| Estimated probability of beating buy-and-hold | 41.8% |

The final-test ROC-AUC confidence interval crosses 0.50, and the strategy's estimated excess return relative to buy-and-hold is close to zero. The evidence therefore does **not** support a reliable incremental forecasting edge.

The central result is methodological: development-stage gains can disappear under a locked final test, especially when financial signals are weak, non-stationary, and sensitive to validation design.

## Repository Structure

```text
market-direction-blending-ensemble/
├── README.md
├── market_direction_blending_ensemble.ipynb
├── requirements.txt
├── figures/
│   ├── final_test_candidate_roc_curves.png
│   ├── final_test_auc_bootstrap_intervals.png
│   ├── final_test_locked_strategy_wealth.png
│   └── final_test_excess_return_bootstrap_intervals.png
└── tables/
    └── selected_summary_outputs.csv
```

Raw and processed datasets, fitted model binaries, logs, temporary notebook files, and submission-specific documents are intentionally excluded from the public repository.

## Running the Notebook

Create a clean Python environment and install the dependencies:

```bash
pip install -r requirements.txt
```

Then launch Jupyter:

```bash
jupyter notebook market_direction_blending_ensemble.ipynb
```

The notebook should be executed sequentially from top to bottom. It creates the required project directories, retrieves the public market data, reconstructs the features and models, and writes generated outputs locally.

## Reproducibility Notes

- Random seeds are fixed where supported.
- Chronological partitions are deterministic.
- Feature screening, model selection, ensemble construction, and threshold selection are performed without access to final-test labels.
- Small numerical differences may occur across Python, operating-system, and package versions.
- The final holdout is not used for retuning or model replacement.

## Limitations

- The analysis focuses on one highly liquid US equity-market ETF.
- Daily observations provide a limited effective sample after chronological splitting.
- Financial return direction is noisy and potentially non-stationary.
- Trading results depend on the chosen position rule and transaction-cost assumptions.
- The study is an empirical research and portfolio project, not an investment recommendation.

## Disclaimer

This repository contains an independent implementation prepared for learning, research, and portfolio demonstration. It does not include proprietary assessment prompts, official solutions, lecture materials, declarations, restricted datasets, or personal submission records.

Nothing in this repository constitutes financial advice.
