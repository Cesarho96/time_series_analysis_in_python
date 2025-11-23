## Purpose

This repository contains the source material for a time-series analysis course (Jupyter notebooks, small CSV datasets). These instructions give an AI coding assistant enough context to make useful, low-risk edits: updating notebooks, fixing small code cells, improving examples, or adding minimal helper scripts.

## High-level architecture / big picture
- Primary artifacts: Jupyter notebooks organized by `Section X/` folders. Most folders contain a "Template" notebook and a "Completed" notebook.
- Data files live inside lesson subfolders (examples: `Section 3/S_3_L_11/Index2018.csv`, `Section 5/S_5_L_22/RandWalk.csv`). Notebooks open these CSVs via relative paths.
- There is no monolithic Python package or service; logic is distributed across notebook cells. Changes should respect notebook-first workflows.

## Developer workflows (how humans run the project)
- Install runtime: pip install -r requirements.txt (the repo uses pinned versions; preserve compatibility when editing examples).
- Work interactively: open the notebooks in Jupyter Lab/Notebook and run cells. Notebooks include both "Template" and "Completed" variants; prefer editing templates and producing a new completed notebook if needed.
- For automated execution of a notebook (e.g., validation), use nbconvert/execute: `jupyter nbconvert --to notebook --execute --inplace path/to/notebook.ipynb` (validate before pushing changes).

## Conventions and patterns to preserve
- Keep file paths relative. Notebooks reference datasets using relative paths (do not hard-code absolute paths).
- Datasets are small CSVs included under their lesson's `S_*` folder; if you add or move data, update all notebooks that reference it.
- Prefer small, local helper scripts only when reusing logic across multiple notebooks. If extracting code into modules, place them in a top-level `src/` (create if necessary) and update notebooks' import paths.
- Don't refactor notebook linearity (reordering essential setup cells) without verifying the whole notebook runs.

## Integration points & external dependencies
- Primary external deps are listed in `requirements.txt` (pinned). Key libraries: `pandas`, `numpy`, `statsmodels`, `arch`, `matplotlib`, `seaborn`.
- No CI, tests, or packaging currently present. Treat new changes as local edits and validate by running the affected notebooks.

## Typical tasks the assistant can safely perform
- Fix obvious Python errors inside notebook cells (syntax, missing imports) while ensuring the cell's inputs/outputs remain consistent.
- Update plots' labels, small typos in markdown cells, and clarifying comments in code cells.
- Replace deprecated API calls with modern equivalents only when covered by pinned `requirements.txt` versions; prefer minimally invasive fixes and test by executing the notebook.

## When *not* to change automatically
- Large restructures (convert many notebooks to a package) or changes that alter lesson content substantially—ask a human.
- Changing or deleting datasets without explicit instruction.

## Examples from this repo
- Templates vs Completed: `Section 10/Section 10 - The ARIMA Model - Template.ipynb` and `Section 10/Section 10 - The ARIMA Model - Completed .ipynb`
- Small datasets: `Section 3/S_3_L_11/Index2018.csv`, `Section 5/S_5_L_22/RandWalk.csv` — notebooks load these by relative path.

## Quick checklist for edits
1. Identify the notebook(s) to change (prefer the `Template` file).
2. Run `pip install -r requirements.txt` in a fresh venv matching the user environment.
3. Open and run the notebook locally (or run nbconvert execute) to reproduce the issue.
4. Make minimal change, re-run the notebook end-to-end, and commit only the modified notebook and any tiny helper script or data file.

## If you need clarification
- Ask the repo owner to specify whether a change should modify the `Template` or `Completed` notebook. When in doubt, modify the `Template` and leave the `Completed` copy untouched.