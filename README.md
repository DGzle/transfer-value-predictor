# Soccer Player Transfer Value Predictor

Course project: predict a soccer player's market value from their stats and profile using a linear regression model in Python.

## Goal

Turn player data (age, position, minutes, goals, assists, caps, contract) into a transparent, repeatable market value estimate:
**stats in -> model in the middle -> market value out.**

## Data sources

| Need | Source |
|---|---|
| Market value (target), player profile, appearances (minutes, goals, assists), international caps, contract expiry | [transfermarkt-datasets](https://github.com/dcaribou/transfermarkt-datasets) (Kaggle: `davidcariboo/player-scores`, CC0), snapshot to July 2026 |
| Squads and top scorers via API (tested) | football-data.org free tier. It returned no market values and no contract dates for the 543 Premier League players, so it cannot supply the target. Kept in notebook 01 as a documented finding. |

Scope: Premier League, 2025/26 season.

## Pipeline

1. `notebooks/01_data_collection.ipynb` - tests the football-data.org API and documents its free-tier limits
2. `notebooks/02_cleaning_merging.ipynb` - builds one row per Premier League player (target = latest valuation in the season; features from appearances and profile)
3. `notebooks/03_model.ipynb` - log-transform the target, linear regression, R² and MAE, charts, random forest preview
4. Charts are saved to `figures/`

## Setup (Ubuntu)

```bash
git clone https://github.com/DGzle/transfer-value-predictor.git
cd transfer-value-predictor
sudo apt install python3-venv     # only if venv is missing
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
cp .env.example .env              # only needed for notebook 01 (football-data.org token)
```

Download the dataset zip from Kaggle (`davidcariboo/player-scores`) and unzip it into `data/raw/`. Raw data is not tracked in git.

```bash
unzip ~/Downloads/archive.zip -d data/raw/
jupyter notebook
```

Never commit `.env`.

## Repository layout

```
data/raw/          raw downloads and API responses (not tracked in git)
data/processed/    cleaned datasets
notebooks/         01 data collection, 02 cleaning/merging, 03 model
figures/           charts for the slides
src/               reusable code
```

## Status

- [x] Repository and environment set up
- [x] football-data.org API tested (no market values on free tier)
- [x] Switched market value source to the Transfermarkt dataset
- [ ] Cleaned, merged dataset (notebook 02)
- [ ] Baseline linear regression (R², MAE) (notebook 03)
- [ ] Visualizations
- [ ] Checkpoint presentation (reviews/comments due Oct 21, 2026)

## Team

- DGzle
- (teammate)
