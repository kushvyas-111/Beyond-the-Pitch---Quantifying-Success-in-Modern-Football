# Beyond-the-Pitch---Quantifying-Success-in-Modern-Football
# TEAM 10 - Kush Vyas, Gurveen Rekhi, Shi Qiu, Yu-Chien Chen, Yashaswini Reddy, Xiaoxuan Zhu

Overview

This project investigates what drives football club success by integrating financial, tactical, and disciplinary data into a unified analytical framework. Using BigQuery, SQL, and multi-table datasets sourced from the Transfermarkt repository (via Kaggle), we examine whether clubs win more because they spend more, build balanced squads, or maintain superior discipline on the pitch.

The workflow includes extensive data cleaning, entity consolidation, season-level aggregation, and exploratory analysis across millions of match, player, and valuation records.

Objectives

The project focuses on three core pillars:

1. Financial Strength

Squad market value by club × season

Transfer expenditure influence

Correlation between valuation and win percentage

Identification of financially efficient overperformers

2. Squad Composition

Age structure of squads (minutes-weighted and unweighted)

Positional distribution of minutes and goals

Tactical dependencies (e.g., midfield-heavy vs forward-driven offenses)

3. Discipline & Competition Context

Yellow/red card accumulation by season and competition

League-level disciplinary intensity

Relationship between cards and win rates

Data Sources

Primary dataset:
Transfermarkt Global Player and Match Data
Kaggle link: https://www.kaggle.com/datasets/davidcariboo/player-scores

Dataset Characteristics:

555 MB, 100k+ records, 133 columns across 10 source files

Match-level, player-level, club-level, and event-level tables

Numerous missing values requiring extensive cleaning and reconstruction

Repository Structure
.
├── data/
│   ├── raw/                      # Original Kaggle-sourced CSVs
│   ├── cleaned/                  # Cleaned BigQuery tables (games, clubs, players)
│
├── sql/
│   ├── cleaning/
│   │   ├── clean_games.sql
│   │   ├── clean_clubs.sql
│   │   ├── clean_players.sql
│   │   └── clean_club_games.sql
│   ├── transformations/
│   │   ├── v_season_ranges.sql
│   │   ├── v_player_valuation_latest.sql
│   │   ├── v_club_season_performance.sql
│   │   ├── v_club_squad_value.sql
│   │   └── views_age_position_discipline.sql
│   └── analysis/
│       ├── finance_vs_performance.sql
│       ├── squad_age_vs_winpct.sql
│       ├── discipline_vs_results.sql
│
├── notebooks/
│   └── A10-Beyond-the-Pitch.ipynb   # Full pipeline and analysis
│
├── visuals/
│   ├── EDA_plots/
│   ├── Tableau_screenshots/
│
└── README.md

Data Cleaning Summary

Extensive preprocessing was required due to high missingness, redundancy, and schema inconsistencies across tables.

Games Table

Dropped: match-day positions, attendance, formations, referees, URLs

Removed rows with missing identifiers (game_id, clubs, goals)

Result: 74,014 validated match records

Clubs Table

Recomputed foreigners_percentage from available fields

Removed rows with missing primary identifiers

Result: 439 clubs with complete attributes

Club Games Table

Removed rows missing club_ids or goal data

Result: 148,028 records

Players Table

Removed metadata (first_name/last_name, URLs, images, contracts)

Imputed: height, market values, date of birth

Standardized unknown position/foot to categorical "Unknown"

Result: 32,601 players cleaned

Key Analytical Views

v_season_date_ranges: Season start/end boundaries

v_player_season_latest_value: Latest valuation per player × season

v_club_squad_value_by_season: Aggregated squad market values

v_club_season_performance: Win rate, goals, matches by season

club_season_age_stats: Minutes-weighted age composition

club_season_pos_stats: Positional minutes and goal shares

club_season_card_metrics: Season-level discipline summaries

These views feed all downstream insight generation.

Major Findings
1. Financial Strength Matters—but Weakly

Overall correlation between squad value and win percentage ≈ 0.23

High-value clubs typically win more, but variance is large

Several clubs outperform their spending dramatically (win_pct ≈ 0.85 with < €5M squads)

Insight: Financial power offers an advantage, but tactical efficiency and development can rival spending.

2. Squad Composition Drives Tactical Outcomes

Minutes-weighted age around 23–31 correlates with stronger results

U23-heavy squads underperform unless minutes are well balanced

When forwards contribute fewer goals, win percentages flatten even if overall goal differences remain positive

Insight: Balanced positional output—particularly from forwards—is more impactful than average age alone.

3. Discipline Influences Club Outcomes

High yellow/red card counts correlate with lower win rates

Aggressive teams often face momentum loss due to red cards

League-level averages show significant variation in competitiveness and officiating intensity

Insight: Clubs that maintain discipline tend to outperform those with high card accumulation.

Visualization Dashboard

Tableau Story Link:
https://public.tableau.com/app/profile/gurveen.rekhi/viz/A10Assignment2/Story1?publish=yes

Dashboards include:

EDA snapshots

Positional market value differences

Squad composition vs performance

Discipline metrics across seasons

Technologies Used

Google BigQuery for SQL transformations and large-scale processing

Colab / Python for orchestration and documentation

Tableau Public for visualization

Kaggle datasets as raw input

How to Reproduce

Clone this repository

Create a BigQuery project and dataset

Upload raw CSVs to BigQuery

Run SQL scripts in the /sql/cleaning folder in the following order:

clean_games.sql

clean_clubs.sql

clean_players.sql

clean_club_games.sql

Execute transformation and analysis views

Run the notebook A10-Beyond-the-Pitch.ipynb

Optionally import clean tables into Tableau for visualization

Limitations

Missing or inconsistent Transfermarkt data imposes structural bias

Market values fluctuate mid-season and may not fully represent player contributions

Red/yellow card interpretation may vary by league and referee

Dataset does not include tactical formation-level events

Future Improvements

Incorporate player-level event data (pressure, shots, xG, xA)

Add financial expenditures and wage-bill analysis

Model team efficiency using regression or ML-based approaches

Introduce league-adjusted normalization for cross-region comparability
