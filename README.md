# Walmart Sales Forecasting

Predicts weekly sales for 45 Walmart stores across 81 departments using historical sales, macroeconomic features, and holiday flags. The project benchmarks Ridge, Lasso, Decision Tree, and Random Forest regressors — with Random Forest achieving an R² of **0.971** and RMSE of **$3,881** — to help store managers plan inventory and staffing around seasonal demand spikes.

---

## Quickstart

```bash
# 1. Clone
git clone <repo-url>
cd "Walmart Sales Forecasting"

# 2. Create a virtual environment (recommended)
python -m venv .venv
# Windows
.venv\Scripts\activate
# macOS / Linux
source .venv/bin/activate

# 3. Install dependencies (no requirements.txt in repo — derived from notebook imports)
pip install numpy pandas matplotlib seaborn plotly scikit-learn jupyter

# 4. Launch the notebook
jupyter notebook Walmart_Sales_Forecasting.ipynb
```

> **Python version:** The notebook kernel metadata specifies **Python 3.11.9**. It originally ran on Google Colab with GPU enabled. Any Python 3.9+ should work.

> **[unverified]** Whether specific library version pins are needed. No `requirements.txt` exists in the repo.

---

## Configuration

This repo has **no environment variables, config files, or CLI flags**. All behaviour is controlled inside the notebook.

| Item | Location | What it does |
|:---|:---|:---|
| **Data paths** | Cell 2 of notebook | Hardcoded as `E:/Project/Walmart Sales Forecasting/*.csv`. **You must update these** to match your local directory. |
| **Train/test split** | `train_test_split(…)` call | Sets the holdout fraction for model evaluation. |
| **Hyperparameter grids** | `GridSearchCV` / `RandomizedSearchCV` cells | Defines the search space for Decision Tree and Random Forest tuning. |
| **`.gitignore`** | Repo root | Ignores `.ipynb_checkpoints/`, `*.pyc`, `__pycache__/`, `.env`. |

### Data Files

| File | Size | Key Columns |
|:---|:---|:---|
| `train.csv` | ~12 MB | `Store`, `Dept`, `Date`, `Weekly_Sales`, `IsHoliday` |
| `test.csv` | ~2.5 MB | `Store`, `Dept`, `Date`, `IsHoliday` |
| `features.csv` | ~580 KB | `Store`, `Date`, `Temperature`, `Fuel_Price`, `MarkDown1`–`5`, `CPI`, `Unemployment`, `IsHoliday` |
| `stores.csv` | ~0.5 KB | `Store`, `Type`, `Size` |

---

## Usage

The entire workflow lives in one Jupyter notebook: [`Walmart_Sales_Forecasting.ipynb`](file:///e:/Project/Walmart%20Sales%20Forecasting/Walmart_Sales_Forecasting.ipynb).

### Load data

```python
train_df = pd.read_csv('train.csv')
features_df = pd.read_csv('features.csv')
stores_df = pd.read_csv('stores.csv')
```

### Train the best model (Random Forest)

```python
from sklearn.ensemble import RandomForestRegressor

rf = RandomForestRegressor()
rf.fit(X_train, y_train)
y_pred = rf.predict(X_test)
```

### Evaluate predictions

```python
from sklearn.metrics import mean_squared_error as mse, r2_score
from math import sqrt

rmse = sqrt(mse(y_test, y_pred))
r2 = r2_score(y_test, y_pred)
print(f"RMSE: ${rmse:,.0f}  |  R²: {r2:.3f}")
```

### Tune hyperparameters

```python
from sklearn.model_selection import GridSearchCV

grid = GridSearchCV(RandomForestRegressor(), param_grid={...}, cv=5)
grid.fit(X_train, y_train)
```

> The snippets above are simplified. See the notebook for the full feature-engineering pipeline (merging `features.csv` and `stores.csv`, date extraction, markdown handling) and the exact param grids.

### Model Results

| Model | Test RMSE | Test R² | Verdict |
|:---|:---|:---|:---|
| Ridge Regression | $21,812 | 0.085 | Poor |
| Lasso Regression | $22,092 | 0.061 | Poor |
| Decision Tree | $4,889 | 0.954 | Very Good |
| **Random Forest** | **$3,881** | **0.971** | **Best** |

---

## Development

### Run the notebook end-to-end (headless)

```bash
jupyter nbconvert --to notebook --execute Walmart_Sales_Forecasting.ipynb
```

**[unverified]** — This uses standard `nbconvert`. The repo has no Makefile, test script, or CI configuration.

### Tests

There are **no automated tests**. Validation is done visually via plots and metric print-outs inside the notebook.

### Contributing

1. Fork the repo and create a feature branch.
2. Update the hardcoded data paths to use relative paths (e.g., `./train.csv`).
3. Ensure the notebook runs top-to-bottom without errors before opening a PR.
4. Large CSVs are already tracked in Git. **[unverified]** whether Git LFS is set up.

---

## Project Structure

```
├── Walmart_Sales_Forecasting.ipynb   # Main analysis & modelling notebook
├── train.csv                         # Historical weekly sales (target variable)
├── test.csv                          # Holdout set (no Weekly_Sales column)
├── features.csv                      # Store-level macro & promotional features
├── stores.csv                        # Store metadata (type, size)
├── sales_forecasting_banner.jpg      # Banner image
├── README.md
└── .gitignore
```
