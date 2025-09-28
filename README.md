# LEGO Sets Price Prediction

This repository contains a Jupyter Notebook that loads a LEGO sets CSV, performs cleaning and feature fixes, trains a few regression models, and uses them to predict set prices. The notebook demonstrates end-to-end steps from data loading to model evaluation and example predictions.

---

## Project structure

```
project_folder/
│── SIAP LEGO.ipynb                 # Main notebook
│── dataset/
│   ├── sets.csv                    # Raw dataset (expected location)
```

> The notebook uses a **relative path** `dataset/sets.csv` so the project is portable. Put your `sets.csv` inside the `dataset/` folder next to the notebook.

---

## What the notebook does

1. **Load dataset** from `dataset/sets.csv` using `pandas`.
2. **Inspect & display** the DataFrame (shape, sample rows).
3. **Drop duplicate rows**.
4. **Impute `USD_MSRP` missing values** with the median (so there are no missing `USD_MSRP` values afterwards).
5. **Apply a simple heuristic fix**:

   * If `Name` contains `"Key Chain"` and `Minifigures` is missing → set `Minifigures = 1`, `Pieces = 3`.
6. **Save cleaned dataset** to `dataset/cleaned_lego_dataset.csv`.
7. **Modeling for `Current_Price`**:

   * Prepare features and target (`Current_Price`), fill `Current_Price` with `USD_MSRP` where missing.
   * Split train/test sets.
   * Train/evaluate three regressors inside pipelines with preprocessing:

     * Linear Regression
     * Decision Tree
     * Random Forest
   * Compute RMSE and R² for each model (example results shown in the notebook).
8. **Make example predictions** for sample LEGO sets and print per-model predicted prices.

---

## Key outputs

* Cleaned dataset: `dataset/cleaned_lego_dataset.csv`
* Model performance printed in the notebook (example values from a run):

  * Linear Regression RMSE: \~186.49, R²: \~0.115
  * Decision Tree RMSE: \~194.95, R²: \~0.033
  * Random Forest RMSE: \~181.57, R²: \~0.161
* Example per-set predictions (printed in the notebook).

---

## Requirements

This notebook was executed with a Python kernel reporting `Python 3.12.7`.

Install minimal dependencies:

```bash
pip install pandas scikit-learn jupyterlab notebook
```

---

## How to run

1. Clone repo or copy the notebook and place your `sets.csv` under `dataset/sets.csv`.
   If `dataset/` folder doesn't exist, create it:

   ```bash
   mkdir dataset
   # move or copy sets.csv into dataset/
   ```

2. Start Jupyter and open the notebook:

On Windows:
   ```cmd
   jupyter notebook "SIAP LEGO.ipynb"
   ```

3. Run cells top to bottom (Run → Run All). The notebook will:

   * Clean the data,
   * Save cleaned CSV to `dataset/cleaned_lego_dataset.csv`,
   * Train the models and print evaluation results,
   * Print example predictions.

---

## Quick troubleshooting

* **FileNotFoundError for `dataset/sets.csv`** → ensure the file exists at that relative path.
* **Different Python version** → verify your kernel matches installed packages. Use virtualenv/conda to control the environment.
* **Very high RMSE / low R²** → try more/cleaner features, remove outliers, log-transform price.

---

## License & attribution

MIT license, granted full access to edit and contribute to this repository.
