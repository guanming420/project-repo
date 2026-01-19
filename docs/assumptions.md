# Assumptions

This project relies on the following assumptions based on observed patterns in
the dataset and common MVP voting logic.

## Data and scope

- Regular-season performance is the primary basis for MVP consideration.
- Traded-player stats are already aggregated to season totals when `team_id` is
  `TOT`, so additional aggregation is unnecessary.
- The dataset captures a consistent snapshot of player/team context per season.
- Historical seasons are comparable once standardized features (ranks, z-scores)
  are used to normalize across eras.
- The key unit of analysis is player-season-age to disambiguate duplicate
  player-season rows that actually represent different players with the same
  name in the same season.

## MVP voting dynamics

- Team success materially influences MVP voting, not just individual stats.
- Historical `award_share` directly encodes MVP voting outcomes and is the
  target signal for MVP candidacy strength.
- Narrative effects exist but are indirectly reflected through observable
  performance and context features.

## Modeling implications

- Relationships learned from past seasons generalize to nearby seasons under
  similar league conditions.
- Feature engineering captures most of the signal needed to explain vote share,
  even if some qualitative factors are missing.
