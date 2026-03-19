## Quick context

This repository contains a single Jupyter notebook `Gitversion-tesi.ipynb` that implements a Monte Carlo simulation to estimate a transition-risk capital buffer. The analysis is a master's thesis by Lorenzo van Cadsand and relies on CSV inputs in the repository root (regional `portafoglio_*.csv` and `shock_*.csv` files).

Keep guidance tightly focused: this project is notebook-first (not a package). Changes should preserve reproducibility and the original analysis flow.

## What an AI coding agent should know up-front

- Single entrypoint: work inside `Gitversion-tesi.ipynb`. Most logic, parameters (e.g., `num_simulations`, `max_percentages`) and orchestration live in that notebook.
- Data files live at repo root with Italian names (e.g., `portafoglio_Asia.csv`, `Shock_Asia(Foglio1).csv`, `shock_results_final(in).csv`). Notebook currently uses absolute user-specific paths (e.g., `/Users/lorenzovancadsand/Downloads/...`). Avoid changing these paths silently; instead provide configurable relative-path alternatives.
- Parallelization: the notebook uses `joblib.Parallel` (and imports `dask`/`concurrent.futures`) for compute-heavy loops. Preserve semantics when refactoring; ensure n_jobs default uses available cores (`-1`) and remains configurable.
- Random seeds: random number generators are used (numpy, random, gamma). For reproducible outputs, expose a seed parameter and set seeds consistently across numpy, random, and joblib workers.

## Key files to reference in code suggestions

- `Gitversion-tesi.ipynb` — main analysis and simulation logic.
- `README.md` — high-level run instructions and parameter explanations.
- CSV files in repo root — input data. When proposing changes, reference these filenames explicitly.

## Typical developer workflows & commands

- Run interactively (recommended): open the notebook and run cells in order. Use Jupyter or Jupyter Lab.
  ```bash
  jupyter notebook
  # or
  jupyter lab
  ```
- Create a reproducible environment: there is no `requirements.txt`. When adding dependencies, update a top-level `requirements.txt` and document the python version (assume Python 3.10+). Minimal expected dependencies: `pandas`, `numpy`, `scipy`, `dask`, `joblib`, `tqdm`, `openpyxl`.

## Project-specific patterns and conventions

- Notebook-first, exploratory style: many values are hard-coded in the notebook (paths, `num_simulations`, `max_percentages`). When refactoring, keep defaults the same but move configuration into a small top-level configuration cell or a `config.py` to avoid breaking reproducibility.
- IO uses pandas CSV / Excel writers with absolute paths under `/users/lorenzovancadsand/...`. Replace with `Path`-based relative paths and an environment-aware default that preserves current behavior (e.g., fall back to absolute path only when a user override is provided).
- Data aggregation uses pandas groupby -> `.sum()` -> `.quantile()`. Keep column naming conventions (e.g., `shock_YYYY`, `weighted_shock_YYYY`, `sum_delta_v_YYYY`, `percentile_99.5_YYYY`) intact when making edits.

## Safety and correctness checks for PRs

- Do not change numeric defaults silently. If you propose a different `num_simulations`, label it as an optional performance optimization and ensure examples show how to run with the original value.
- Preserve output column names and final Excel output path by default; if changing file locations, update the `README.md` or add a short migration note in the notebook.
- Add or update a `requirements.txt` when introducing new packages.

## Small, safe refactors an agent can propose and apply

- Replace absolute paths with `pathlib.Path` + a single configurable `DATA_DIR` variable at the top of the notebook. Provide a code cell showing how to set `DATA_DIR = Path('.') / 'data'` and fall back to original absolute locations if files aren't found.
- Add a `RANDOM_SEED = 42` config cell and call `np.random.seed(RANDOM_SEED); random.seed(RANDOM_SEED)` before simulations.
- Add a short `Environment` section to `README.md` documenting required packages and a `pip install -r requirements.txt` command.

## When to ask the human

- If you need to change the simulation logic (different shock aggregation, discounting, or VaR percentile), stop and ask — these are methodological choices central to the thesis and should not be altered without approval.
- Confirm where outputs should be written instead of writing to the author's Downloads folder.

## Examples (use these snippets as guidance)

- Refer to the code that generates `final_columns` and `weighted_shock_*` naming — keep that naming when adding derived columns.
- When parallelizing, mirror the notebook's `Parallel(n_jobs=-1)` pattern and make `n_jobs` configurable.

## Final note

Keep instructions concise and avoid heavy restructuring unless the author asks. Prioritize reproducibility: add configuration cells, document dependencies, and avoid silent behavioral changes.

---

If you'd like, I can (1) add a small `requirements.txt` with pinned versions, (2) add a short config cell to the notebook replacing absolute paths with relative `Path` lookups, and (3) insert a reproducible-seed cell. Tell me which of these you'd like me to implement next.
