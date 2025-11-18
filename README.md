# Zeolite ML Notebook

## Overview
This repository contains zeo_predictition.ipynb, a single Jupyter Notebook that trains XGBoost regressors to predict eight zeolite binding-energy targets (4m1, 4m6, 4m11, 4l3, 6m1, 6m6, 6m11, 6l3). Each block performs training/validation, produces publication-ready plots, ranks features with SHAP, and generates CSV predictions for large candidate lists. The narrative has been cleaned up so the notebook reads like a GitHub-ready report.

## Repository layout
- zeo_predictition.ipynb – end-to-end workflow split into eight target sections plus optional filtering utilities.
- data/ – training/inference CSVs (see data/README.md). Raw files are not versioned, but this folder describes the required schema.
- data/ml_data/ – optional workspace for intermediate CSV exports (produced by the notebook).

## Notebook structure
1. **Imports & helpers** – loads pandas, NumPy, scikit-learn metrics, XGBoost, LightGBM, SHAP, Matplotlib/Seaborn, Optuna, Plotly, and Yellowbrick.
2. **Per-target sections** – each labeled ## Target: … and containing:
   - Model training cell that reads data/ml_6m.csv, selects the shared structural descriptors + the current label, tunes/stores an xgb.train booster, and reports RMSE/MAE/R² for train/test splits.
   - Evaluation cell that draws predicted-vs-calculated scatter plots and SHAP bar charts using a consistent 12x8 style guide.
   - Optional SHAP bee-swarm cell to visualize signed contributions.
   - Inference cell that loads data/prediction.csv, applies the latest booster, masks rows lacking 	arget_h, and exports 	arget_20000.csv.
3. **Post-processing cells** – merge the eight prediction CSVs, build aggregate files such as merged_20000.csv, and filter zeolite IDs (e.g., drop IDs containing the digit 1).

## Getting started
1. Create a Python >=3.10 environment and install the main libraries:
   `ash
   pip install pandas numpy scikit-learn xgboost lightgbm shap matplotlib seaborn optuna plotly yellowbrick
   `
2. Place ml_6m.csv and prediction.csv in the data/ directory (see the schema notes in data/README.md).
3. Launch Jupyter Lab/Notebook from the project root and open zeo_predictition.ipynb.
4. Execute the cells top-to-bottom. Each section is independent as long as you do not skip the training cell that populates the st object for that target.

## Outputs
- Text metrics for every target and data split.
- Publication-ready .png/.jpg figures (scatter plots + SHAP bar/bee-swarm charts) in the project root.
- CSVs named <target>_20000.csv storing predictions for the 20k-candidate screening set.
- Aggregated exports such as merged_20000.csv, 20000_p.csv, iza_p.csv, and output.csv when the optional filtering utilities are run.

## Data notes
The notebook expects Latin-1 encoded CSVs. ml_6m.csv must include every feature column listed inside the notebook feature arrays (density, space group number, Si/SiO statistics, PLD, ASA, channel counts, AV, and the relevant <target>/<target>_h columns). prediction.csv reuses the same feature names plus a zeolite identifier column for export. Consult data/README.md for the exact schema and recommended preprocessing steps.

## Contributing / next steps
- Parameter blocks are currently hard-coded per target; feel free to script a loop or move the logic into Python modules if you need automation.
- Add a 
equirements.txt or conda environment file if you plan to share the environment definition.
- Integrate CI to re-run the notebook or extract the training logic into scripts when moving beyond exploratory work.
