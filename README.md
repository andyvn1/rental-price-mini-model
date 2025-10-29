# Rental Price Mini-Model (Linear Regression)

Predict monthly **rent (USD)** from basic listing features using a compact, reproducible scikit-learn pipeline (OLS + Ridge/Lasso). The project is intentionally small for learning and portfolio use.

## What it does
- Loads tabular listing data (beds, baths, sqft, city, property_type)
- Cleans & encodes features (scale numerics, one-hot categoricals)
- Trains **OLS**, **Ridge**, and **Lasso** (with light CV for α)
- Evaluates on a held-out test split with **MAE / RMSE / R² (USD)**
- Saves the best pipeline to `models/best_model.pkl` and metrics to `reports/metrics.json`

## Repo structure
rental-price-mini-model/<br>
├─ README.md<br>
├─ requirements.txt<br>
├─ .gitignore<br>
├─ data/<br>
│  ├─ README.md<br>
│  └─ sample/<br>
│  └─ rentals_sample.csv # tiny demo so it runs instantly<br>
├─ scripts/<br>
│  └─ train.py # CLI: train/evaluate/save<br>
├─ notebooks/<br>
│  └─ rental_price_regression.ipynb # (optional) end-to-end notebook<br>
├─ models/ # saved pipeline (.gitignored, .gitkeep)<br>
└─ reports/ # metrics/figures (.gitignored, .gitkeep)<br>

bash
Copy code

## Quick start

> **PowerShell (Windows)**
```powershell
# 1) Activate your venv (example)
.\.venv\Scripts\Activate.ps1

# 2) Install deps
pip install -r requirements.txt

# 3) Run training on the tiny sample
python scripts\train.py

# (later) Run on your real CSV
python scripts\train.py --data data\rentals.csv
Outputs:

models\best_model.pkl – serialized sklearn pipeline (preprocess + model)

reports\metrics.json – e.g. {"model":"ridge_tuned","RMSE":..., "MAE":..., "R2":...}

Data schema
Minimum columns (required):

rent_usd (float), bedrooms (int), bathrooms (float), sqft (int),

city (str), property_type (str: apt|house|condo)

CSV format: UTF-8, comma-delimited, header row present.

The training script applies light guards (filters extreme values and uses log1p(rent) internally; metrics are computed back on USD).

Evaluation metrics (plain English)
MAE – average absolute error in dollars (typical miss)

RMSE – emphasizes big misses more than MAE

R² – variance explained (0–1; higher is better)

For a small mixed dataset, a baseline target is roughly MAE $250–$450 and RMSE $350–$600 (data-dependent).

Reproducing with Jupyter (optional)
powershell
Copy code
# launch
jupyter notebook
# open notebooks\rental_price_regression.ipynb and Run All
Notes
Real/big data files live in data/ and are gitignored; keep only tiny samples in data/sample/.

The pipeline is simple by design—ideal for learning and a quick portfolio entry.

Resume snippets (fill in your numbers)
Built a linear-regression baseline (OLS/Ridge/Lasso) to predict rental prices; achieved $<MAE> MAE / $<RMSE> RMSE, R²=<R2> on a held-out test set.

Delivered a reproducible workflow with saved model (joblib) and metrics JSON.

pgsql
Copy code

If you want, I can also add a tiny `scripts/predict.py` that loads `models/best_model.pkl` and predicts a single row you pass in as JSON—handy for demos.




>>>>>>> 5db3f01 (Init: README, requirements, clean structure (.gitignore, placeholders))
