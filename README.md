# Illiquid-to-Liquid Signal Projection

This repository presents a quantitative research project inspired by a challenge
proposed by Qube Research & Technologies (QRT). The objective is to transfer predictive
signals from illiquid assets to liquid instruments by learning cross-asset relationships.

## Problem Overview
In systematic trading, predictive signals are often generated on assets that may be
difficult or impossible to trade due to liquidity constraints. To overcome this issue,
we seek to project signals from illiquid assets onto liquid ones by exploiting their
statistical and sectoral relationships.

The task is formulated as a classification problem: predicting the **sign** of liquid
asset returns using information derived from illiquid asset returns.

## Data Description
- 100 illiquid assets (input features)
- 100 liquid assets (prediction targets)
- Observations are indexed by day
- For a given day, illiquid returns are shared across all liquid targets
- Liquid returns are sparsely observed across days and treated as missing labels when
  not available

The original datasets are not included due to competition rules.

## Methodology
The approach follows a structured and interpretable pipeline:

- Day-level reshaping of the dataset
- Sector-based grouping using class level classifications
- Construction of PCA-based illiquid portfolios within each sector
- Adaptive number of components (up to 3) depending on sector size
- Ridge regression models trained independently for each liquid asset
- Custom weighted sign-accuracy metric aligned with trading objectives

## Local Validation
A simple train/test split at the day level is used for local validation as a sanity check.
Using ridge regression with a manually tuned regularization parameter, the model achieves
a mean weighted sign accuracy of approximately **0.71** across the 100 liquid assets.

This local score is not intended as a leaderboard result, but as a consistency check of
the modeling assumptions.

## Inference
Final models are trained on the full training dataset and applied line-by-line to the test
set. For each test observation, the appropriate liquid-asset-specific model is used to
predict the sign of the return.

## Limitations and Future Work
- Explore nonlinear models (e.g. neural approaches)
- Investigate multi-task or hierarchical learning across liquid assets
- Refine sector granularity and factor construction


