Company Branch Sales Analysis

Overview

This repository contains a small sales-analysis project for multiple company branches. It shows how branch-level CSV files are combined and analyzed using Jupyter notebooks. The analysis notebook performs exploratory data analysis, date/time parsing, grouping/aggregation, and plotting.

Repository structure

- `Abuja_Branch.csv`, `Lagos_Branch.csv`, `Port_Harcourt_Branch.csv` — raw branch CSV files (examples).
- `branches.csv` — combined CSV produced by `combine_data.ipynb` (concatenation of the branch files).
- `data.csv` — a small sample dataset used for examples.
- `combine_data.ipynb` — lightweight notebook that finds all `.csv` files in the project folder and concatenates them into `branches.csv`.
- `main.ipynb` — the main analysis notebook (imports `branches.csv`, does EDA, parses dates/times, computes groupby statistics, and generates seaborn/matplotlib plots).

Typical columns used in the analysis

The notebooks refer to and use columns such as:
- Branch, City, Date, Time, Quantity, Price, Product, Product line, Payment, gross income

Note: exact columns present depend on your CSV files; `data.csv` includes Product, Quantity, Price, Date.

Requirements

- Python 3.8+ recommended
- See `requirements.txt` for the minimal Python packages used

Quickstart (recommended)

1. Create and activate a virtual environment (macOS / zsh):

```bash
python3 -m venv .venv
source .venv/bin/activate
```

2. Install dependencies:

```bash
pip install -r requirements.txt
```

3. Combine branch CSVs (option A — run the notebook):
- Open `combine_data.ipynb` in Jupyter and run the cells. It will create/overwrite `branches.csv` by concatenating all `*.csv` files in the project folder.

Option B — run a one-liner Python script to combine CSVs:

```python
import glob
import pandas as pd
files = glob.glob("*.csv")
files = [f for f in files if f != 'branches.csv']
df = pd.concat(map(pd.read_csv, files), ignore_index=True)
df.to_csv('branches.csv', index=False)
```

4. Open `main.ipynb` and run the analysis cells. The notebook performs these steps:
- Load `branches.csv` into a DataFrame
- Convert `Date` and `Time` to datetime types
- Create Day/Month/Year/Hour columns
- Run groupby aggregations (by City, Branch, etc.) and produce seaborn/matplotlib plots

Notes and suggestions

- If your CSV files are large, consider filtering before loading or sampling for quick iteration.
- If you want the repo to exclude raw data files in future, add patterns to `.gitignore` (already included in this repo).
- The project currently committed CSV files; if you later want to keep data out of git, remove them from the index with `git rm --cached <file>` and commit.

License & contact

This repo doesn't include a license. If you want to open-source it, add a `LICENSE` file.

For questions, update the README or open an issue in your GitHub repo.
