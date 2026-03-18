# AGENTS Guide

## Project Snapshot
- This repo is a single-workflow ML exercise centered in `linear_regression.ipynb`.
- Data source is Kaggle House Prices training data in `train.csv` (target column: `SalePrice`).
- There is no package/module layout, test suite, or CLI; work happens cell-by-cell in the notebook.

## Canonical Pipeline (follow this order)
1. Import libs: `pandas`, `numpy`, `matplotlib`, `seaborn`, `scikit-learn` (`linear_regression.ipynb`).
2. Load data from local `train.csv` using `pd.read_csv("train.csv")`.
3. Preprocess in-place:
   - numeric nulls -> median (`select_dtypes(include=[np.number])`)
   - categorical nulls -> mode (`select_dtypes(include=['object', 'string', 'category'])`)
   - one-hot encode with `pd.get_dummies(..., drop_first=True)`
   - drop `Id`
4. Split features/target: `X = df.drop('SalePrice')`, `y = df['SalePrice']`.
5. Train/validation split: `train_test_split(..., test_size=0.2, random_state=42)`.
6. Fit baseline model: `LinearRegression().fit(X_train, y_train)`.
7. Evaluate with scatter plot and metrics: MAE, MSE, R2.

## Project Conventions To Preserve
- Keep preprocessing deterministic and aligned with existing cells (median/mode + one-hot + `drop_first=True`).
- Keep `random_state=42` for comparable outputs across runs.
- Use notebook-style incremental outputs (`print`, plots) instead of building abstractions unless requested.
- When adding new models/features, keep baseline linear regression cells intact for side-by-side comparison.

## Known Gotchas In Current Notebook
- `y_pred = model.predict(sX_test)` is a typo; use `X_test`.
- `pd.get_dummies` is applied before split on the full dataframe; keep behavior consistent unless explicitly refactoring.
- Only training CSV is in-repo; Kaggle test/submission flow is described but not implemented.

## Quick Run Workflow
```powershell
pip install pandas numpy seaborn matplotlib scikit-learn
```
- Open and run `linear_regression.ipynb` top-to-bottom.
- If adding code for Kaggle submission, ensure test data receives identical preprocessing columns as training.

## Key Reference Files
- `linear_regression.ipynb`: end-to-end workflow and assignment tasks.
- `train.csv`: schema and target distribution used by all modeling code.

