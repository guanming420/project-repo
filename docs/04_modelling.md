# 04 Modelling

This notebook trains and evaluates models that predict `award_share` using the
engineered feature set. It compares a baseline ElasticNet model against an
XGBoost regressor, evaluates performance overall and on MVP candidates, and
uses SHAP to identify key drivers of vote share.

## Overview

- Input data: `../data/features.parquet`
- Target: `award_share`
- Models: ElasticNet (baseline), XGBoost (primary)
- Split strategy: season-based train/validation/test

## Steps

### 1) Imports and data load

- Import scikit-learn utilities, XGBoost, metrics, and SHAP.
- Read the feature set into `df_clean` and copy to `modelling_df`.
- Create separate copies for ElasticNet and XGBoost.

### 2) Feature selection and drops

- Define common drops for both models: identifiers and `is_mvp`.
- Define era-sensitive raw stats to remove for ElasticNet to avoid duplicates
  with z-scores and ranks.
- Drop season rank features for ElasticNet.
- For XGBoost, keep most features and drop only IDs and `is_mvp`.

### 3) Season-based train/validation/test split

- Split seasons into 70/15/15 buckets based on chronological order.
- Build boolean indices for train/val/test.

### 4) Build training matrices

- Set `target = "award_share"`.
- Create train/val/test feature matrices and target vectors for both models.

### 5) Train models

- ElasticNet: standardize features and fit `ElasticNetCV` with 5-fold CV.
- XGBoost: train a regressor with early stopping using a validation set.

### 6) Overall evaluation

- Compute RMSE, MAE, and R2 on the test set for both models.
- Report train-set metrics for overfitting checks.

### 7) MVP-candidate evaluation

- Evaluate model performance on non-zero `award_share` rows.
- Compare ElasticNet vs XGBoost on this subset.

### 8) Season ranking metrics

- Compute top-1 MVP hit rate by season.
- Compute mean Spearman correlation of predicted vs true ranks by season.

### 9) Insight generation

- Identify seasons where the top-1 prediction was incorrect.
- Inspect a failed season (2017) by comparing top predicted vs top true players.
- Use SHAP values on non-zero test cases to rank key feature drivers.
