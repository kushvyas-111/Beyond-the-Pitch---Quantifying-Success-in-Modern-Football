# Beyond-the-Pitch---Quantifying-Success-in-Modern-Football
# TEAM 10 - Kush Vyas, Gurveen Rekhi, Shi Qiu, Yu-Chien Chen, Yashaswini Reddy, Xiaoxuan Zhu

This project aims to uncover the key drivers of football club success by analyzing how financial power, squad structure, and on-field discipline shape season-level performance. By integrating global match, player, and valuation data through BigQuery and SQL, we aim to explain why some clubs consistently outperform others.

📌 Overview

This project analyzes what drives football club success by integrating financial metrics, squad composition, and disciplinary behavior into a unified analytical pipeline. Using Google BigQuery, SQL, and Tableau, we transform 100k+ football records from Transfermarkt into actionable season-level insights.

📂 Repository Structure
.
├── data/
│   ├── raw/                     # Kaggle raw files
│   └── cleaned/                 # BigQuery-cleaned tables
│
├── sql/
│   ├── cleaning/                # Data cleaning scripts
│   ├── transformations/         # Views and helper tables
│   └── analysis/                # Analytical SQL queries
│
├── notebooks/
│   └── Beyond-the-Pitch.ipynb   # Full pipeline notebook
│
├── visuals/
│   ├── EDA_plots/
│   └── Tableau_screenshots/
│
└── README.md

🧠 Project Objectives
1. Financial Strength

Build season-level squad market values

Measure correlation between squad value and win percentage

Identify overperforming low-budget clubs

2. Squad Composition

Minutes-weighted age profiles

Positional minutes and goal contribution shares

Tactical effectiveness based on squad balance

3. Discipline & Competition

Yellow/red card accumulation per club per season

League-level disciplinary intensity

Evaluate whether aggressive play hurts win rates

📊 Key Findings
Financials

Overall correlation between squad value and win percentage ≈ 0.23

Strong but not deterministic relationship

Several clubs outperform despite extremely low squad values (< €5M)

Squad Structure

Performance improves when minutes concentrate in the 23–31 age range

Clubs relying on defenders/midfielders for goal scoring have lower win consistency

Discipline

High card accumulation correlates with lower win %

League refereeing intensity varies significantly

🗃️ Data Sources

Primary: Transfermarkt global dataset (Kaggle)
Link: https://www.kaggle.com/datasets/davidcariboo/player-scores

Dataset details:

555 MB

10 files

133 columns, 100k+ rows

Players, clubs, match results, appearances, valuations

🛠️ Technologies

Google BigQuery (core processing)

SQL (Standard SQL)

Python + Colab

Tableau Public

Kaggle Datasets

🔧 Data Cleaning Summary

Extensive preprocessing across four major tables:

Games

Removed irrelevant/empty columns

Removed rows missing core identifiers

Final: 74,014 valid games

Clubs

Rebuilt foreigners_percentage

Dropped irrelevant info

Final: 439 clubs

Club Games

Removed rows missing club IDs or goal data

Final: 148,028 rows

Players

Dropped metadata columns

Imputed height, market value, and birthdates

Standardized missing categorical attributes

Final: 32,601 players

🏗️ Core SQL Views

v_season_date_ranges

v_player_season_latest_value

v_club_squad_value_by_season

v_club_season_performance

club_season_age_stats

club_season_pos_stats

club_season_card_metrics

These views feed all major analysis.

📈 Visualization Dashboard

Tableau Story:
https://public.tableau.com/app/profile/gurveen.rekhi/viz/A10Assignment2/Story1?publish=yes

Includes:

Initial EDA

Market value by position

Squad structure vs win%

Discipline across leagues and seasons

▶️ How to Reproduce
1. Import data

Download from Kaggle and upload raw CSVs into BigQuery.

2. Run cleaning scripts

Execute SQL files in /sql/cleaning using BigQuery.

3. Generate analytical views

Run scripts in /sql/transformations.

4. Execute analysis queries

Run /sql/analysis or open the Colab notebook.

5. Visualize

Use cleaned tables in Tableau Public.

⚠️ Limitations

Missing or inconsistent Transfermarkt fields

Market values fluctuate heavily mid-season

Card counts vary based on referee/league style

Lack of tactical formation or xG data

🚀 Future Work

Integrate xG/xA advanced metrics

Add wage-bill and net-spend analysis

Build ML model to predict league finish

League-adjusted competitiveness metrics
