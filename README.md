# NBA MVP Modeling (Historical + Future Seasons)

This project builds an explainable, data-driven framework for modeling NBA MVP
candidacy using historical player performance, team context, and season-specific
signals, with the goal of evaluating and extending the approach to future seasons.

## Project Status

Finished (Learning and Research Project)

This repository is complete and no longer under active development. It is
maintained as a reference for the final analysis and results.

Last evaluated: 2026-01-20

## Repository Layout

- `NBA_Dataset.csv`: Raw player-season dataset used as the source input.
- `notebooks/01_data_cleaning.ipynb`: Data cleaning and validation.
- `notebooks/02_eda.ipynb`: Exploratory analysis.
- `notebooks/03_feature_engineering.ipynb`: Feature creation.
- `notebooks/04_modelling.ipynb`: Modeling and evaluation.
- `docs/`: Step-by-step notes that mirror the notebook pipeline.

## Pipeline Outputs

- `data/cleaned.parquet`: Cleaned, validated dataset.
- `data/features.parquet`: Feature-engineered dataset for modeling.

## Results (Latest Run)

Metrics from `notebooks/04_modelling.ipynb`:

- ElasticNet (test): RMSE 0.0487, MAE 0.0231, R2 0.2305
- XGBoost (test): RMSE 0.0289, MAE 0.0039, R2 0.7277
- MVP candidates (non-zero `award_share`, test):
  - XGBoost: RMSE 0.1864, MAE 0.1293, R2 0.6152
  - ElasticNet: RMSE 0.2556, MAE 0.1905, R2 0.2764
- Top-1 MVP hit rate: 0.8333
- Mean Spearman rank correlation by season: 0.5226

Re-run the modelling notebook to refresh these metrics when the dataset changes.

## Getting Started

### Requirements

- Python 3.10+ (or compatible)
- `pip`

### Setup

```bash
python -m venv .venv
.\.venv\Scripts\activate
pip install -r requirements.txt
```

### Run the Pipeline

Run the notebooks in order:

1. `notebooks/01_data_cleaning.ipynb`
2. `notebooks/02_eda.ipynb`
3. `notebooks/03_feature_engineering.ipynb`
4. `notebooks/04_modelling.ipynb`

The docs folder provides concise descriptions of each step:

- `docs/01_data_cleaning.md`
- `docs/02_eda.md`
- `docs/03_feature_engineering.md`
- `docs/04_modelling.md`

## Reproducibility Notes

To reproduce results across time, keep fixed snapshots of `NBA_Dataset.csv`
instead of overwriting the file. For example, store dated copies in a
`data/raw/` folder and rerun the pipeline against a specific snapshot.

## Assumptions and Checks

- `docs/assumptions.md`
- `docs/data_leakage_checks.md`

## License

See `LICENSE`.
