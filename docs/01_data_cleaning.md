# 01 Data Cleaning

This notebook prepares the raw NBA dataset for downstream analysis by standardizing
columns, handling missing values, validating key constraints, and exporting a
cleaned artifact.

## Overview

- Source data: `../NBA_Dataset.csv`
- Output artifact: `../data/cleaned.parquet`
- Unit of analysis: player-season-age

## Steps

### 1) Imports

- Load pandas for data manipulation.

### 2) Load the dataset

- Read the CSV into `df`.
- Display the full DataFrame to verify the load succeeded and inspect the schema.

### 3) Define unit of analysis + key

- Set the key columns to `["player", "season", "age"]` to validate uniqueness at
  the player-season-age level.

### 4) Structural checks

- Normalize column names by stripping whitespace and lowercasing.
- Review column names, count of columns, index range, dtypes, and shape.

### 5) Missing value handling

- Remove rows where `g == 0` (players with no games).
- Inspect missingness across columns.
- Check whether missing shooting percentages coincide with zero attempts:
  - `fg_pct` vs `fga_per_g`
  - `fg3_pct` vs `fg3a_per_g`
  - `ft_pct` vs `fta_per_g`
  - `fg2_pct` vs `fg2a_per_g`
- Fill missing shooting percentages with 0, since missingness aligns with zero
  attempts.
- Fill missing advanced metrics with 0 for consistency:
  - `per`, `ts_pct`, `efg_pct`, `usg_pct`
  - `orb_pct`, `drb_pct`, `trb_pct`
  - `ast_pct`, `stl_pct`, `blk_pct`
  - `tov_pct`, `ws_per_48`, `fg3a_per_fga_pct`, `fta_per_fga_pct`
- Drop any remaining rows with missing values (clears the single missing `age`).

### 6) Duplicate checks

- Normalize `player` names to lowercase for consistent matching.
- Verify no duplicate rows exist for the key columns.
- Ensure no player-season-age appears across multiple teams.

### 7) Validate games per season

- Review the distribution of games played.
- Filter to keep rows with `g <= 82` to enforce season constraints.

### 8) Export cleaned data

- Save the cleaned DataFrame to `../data/cleaned.parquet` for downstream use.
