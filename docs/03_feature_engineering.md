# 03 Feature Engineering

This notebook creates modeling features from the cleaned NBA dataset, focusing
on balanced impact, era-normalized metrics, seasonal rankings, and contextual
signals such as prior MVP wins.

## Overview

- Input data: `../data/cleaned.parquet`
- Output data: `../data/features.parquet`
- Unit of analysis: player-season-age

## Steps

### 1) Imports and data load

- Import numpy and pandas.
- Read the cleaned parquet file into `df_clean` and copy to `fe_df`.
- Define the key columns as `["player", "season", "age"]`.

### 2) Two-way impact balance

- Create offensive vs defensive balance metrics:
  - `two_way_ws_balance = ows - dws` (positive favors offense).
  - `two_way_bpm_balance = obpm - dbpm`.

### 3) Era normalization (season z-scores)

- Define a set of era-sensitive columns (scoring, efficiency, rates, advanced
  impact, team context, and shot mix).
- For each selected column, compute a z-score within each season and append
  a new `{column}_z_season` feature.

### 4) Season rankings

- Rank players within each season for key metrics:
  - `pts_per_g`, `bpm`, `vorp`, `ws`, `ts_pct`, `win_loss_pct`.
- Add `{column}_rank_season` features using descending rank.

### 5) Usage efficiency

- Create `usage_efficiency = usg_pct * ts_pct` to combine usage with efficiency.

### 6) Contextual MVP history

- Identify MVPs by selecting the maximum `award_share` each season.
- Add `is_mvp` (1 if season MVP, else 0).
- Compute `prev_mvp_wins` as the cumulative count of prior MVP wins for each
  player-season-age key.

### 7) Export features

- Save the engineered dataset to `../data/features.parquet`.
