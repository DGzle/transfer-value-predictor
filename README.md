# Soccer Player Transfer Value Predictor

Course project: predict a soccer player's market value from their stats and profile using a linear regression model in Python.

## Goal

Turn player data (age, position, contract, goals, assists, ...) into a transparent, repeatable market value estimate:
**stats in -> model in the middle -> market value out.**

## Data sources

| Need | Source |
|---|---|
| Squads, positions, birth dates, contract dates, market value | [football-data.org](https://www.football-data.org/) API (`/competitions/{code}/teams`) |
| Goals, assists, penalties | football-data.org (`/competitions/{code}/scorers`) |
| Fallback for market values / extra stats | Transfermarkt or API-Football, if the free tier is not enough |

Scope: one league (Premier League, code `PL`) to start.

## Pipeline

1. Collect data from the API (`notebooks/01_data_collection.ipynb`)
2. Clean and merge (`notebooks/02_cleaning_merging.ipynb`)
3. Engineer features: age, position (one-hot), contract years remaining, goals/assists
4. Log-transform the skewed target (market value)
5. Train a linear regression and evaluate with R² and MAE
6. Visualize the main value drivers

## Setup (Ubuntu)

```bash
git clone https://github.com/DGzle/transfer-value-predictor.git
cd transfer-value-predictor
sudo apt install python3-venv     # only if venv is missing
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
cp .env.example .env              # then put your API token in .env
jupyter notebook
```

Get a free API token at https://www.football-data.org/client/register. Never commit `.env`.

## Repository layout

```
data/raw/          raw API responses (not tracked in git)
data/processed/    cleaned datasets
notebooks/         exploration and modeling notebooks
src/               reusable code
```

## Status

- [x] Repository and environment set up
- [ ] API access and first data pull
- [ ] Cleaned, merged dataset
- [ ] Baseline linear regression (R², MAE)
- [ ] Visualizations
- [ ] Checkpoint presentation (due for review by Oct 21, 2026)

## Team

- DGzle
- (teammate)
