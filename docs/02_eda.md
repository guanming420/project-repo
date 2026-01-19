# 02 Exploratory Data Analysis (EDA)

This notebook explores the cleaned NBA dataset to understand the target
(`award_share`), inspect distributions, and identify correlated features that
may affect modeling.

## Overview

- Input data: `../data/cleaned.parquet`
- Target: `award_share`
- Goal: assess feature sets, target behavior, and correlation structure

## Steps

### 1) Imports and data load

- Import core analysis and plotting libraries.
- Read the cleaned parquet file into `df_clean` and copy to `eda_df`.

### 2) Layer 0: Data sanity

- Print the dataset shape.
- Preview the first five rows to confirm expected schema and values.
- Inspect dtypes for all columns.

### 3) Define analysis columns

- Set `TARGET = "award_share"`.
- Identify identifier columns: `season`, `player`, `team_id`, `pos`.
- Identify team context columns (soft leakage risk): `mov`, `mov_adj`,
  `win_loss_pct`.
- Build numeric feature lists:
  - All numeric features excluding the target.
  - A reduced numeric list that excludes team context features.

### 4) Layer 1: Target understanding

- Summarize `award_share` distribution.
- Visualize the target to understand its skew and spread.

### 5) Layer 2: Feature-to-target relationships

- Compute Pearson correlations between numeric features and `award_share`.
- Sort by absolute correlation to highlight dominant signals.
- Plot a horizontal bar chart of correlations.

### 6) Layer 3: Feature-to-feature relationships

- Compute the full numeric correlation matrix (excluding the target).
- Extract high-correlation pairs to identify redundancy and multicollinearity.

### 7) Season-level target coverage

- Count the number of players with `award_share > 0` per season.
- Describe the distribution across seasons.
