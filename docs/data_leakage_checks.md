# Data Leakage Checks

These checks ensure the modeling pipeline does not use information that would
not be available at prediction time or that directly encodes the target.

## 1) Target leakage

- Exclude any direct target encodings from features:
  - `award_share` is the target and must not appear in `X`.
  - `is_mvp` is derived from `award_share` and must be dropped before modeling.

## 2) Post-outcome leakage

- Avoid features that are only known after voting concludes.
- Season-level stats are acceptable because the modeling goal is to explain
  historical vote share using end-of-season performance.

## 3) Feature engineering leakage

- `prev_mvp_wins` must be computed using only prior seasons for each player.
  Sort by season before cumulative counts to prevent peeking at future seasons.
- Season z-scores and season ranks are computed within each season. This is
  acceptable because the task uses full-season context; it does not mix seasons.

## 4) Train/validation/test split leakage

- Ensure splits are season-based with no season overlap across train/val/test.
- Confirm that all rows for a given season fall into exactly one split.

## 5) Identifier leakage

- Drop identifiers from features: `player`, `season`, `team_id`, `pos`.
- Confirm no surrogate identifiers remain (e.g., text labels or encoded IDs).

## 6) Data integrity checks

- Validate the key `player`-`season`-`age` is unique to avoid duplicate leakage
  across splits.
- For traded players, keep only the `team_id = TOT` row so partial stints do not
  leak duplicate season information.
