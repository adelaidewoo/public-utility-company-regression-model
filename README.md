# public-utility-company-regression-model
# Revenue Forecasting with Seasonal Dummy Variables

Multiple linear regression analysis forecasting revenue from production volume, using seasonal dummy variables and interaction terms to capture winter and fall effects. Built in Google Colab as part of an AICPA data analytics course (Week 10 quiz).

## Overview

This project fits and compares two OLS regression models on monthly revenue/production data:

- **Model 1** — `revenue ~ production + winter_DV + winter_interaction`
- **Model 2** — `revenue ~ production + fall_DV + fall_interaction`

Each model is trained on a historical subset of the data and evaluated on a held-out test set using MAPE (mean absolute percentage error).

## Tech stack

- Python 3
- pandas
- numpy
- matplotlib
- statsmodels

## Getting started

```bash
pip install numpy pandas matplotlib statsmodels
```

Place `AICPA_regressionAnalysisData.csv` in the working directory, then run the notebook (`Week 10 Quiz.ipynb`) in Jupyter or Google Colab.

## Data

`AICPA_regressionAnalysisData.csv` contains monthly records (2011–2014):

| Column | Description |
|---|---|
| `type` | `dt4training` or `dt4testing` — pre-assigned split |
| `date` | month-end date |
| `revenue` | monthly revenue |
| `production` | monthly production volume |
| `coolDD` | cooling degree days |
| `heatDD` | heating degree days |

## Methodology

1. Convert `date` to datetime and derive:
   - `winter_DV` = 1 if month is Dec/Jan/Feb, else 0
   - `fall_DV` = 1 if month is Sep/Oct/Nov, else 0
   - `winter_interaction` = `production * winter_DV`
   - `fall_interaction` = `production * fall_DV`
2. Split rows into training/testing sets using the existing `type` column.
3. Fit OLS models on the training set (`statsmodels.api.OLS`).
4. Predict on the test set and compute MAPE for each model.
5. Plot production vs. revenue with fitted regression lines split by season.

## Results

| Model | Test MAPE |
|---|---|
| Model 1 (winter dummy + interaction) | ≈ 15.9% |
| Model 2 (fall dummy + interaction) | ≈ 22.0% |

Model 1 (winter) generalizes better to the test set than Model 2 (fall).

## Repo structure

```
.
├── Week 10 Quiz.ipynb   # analysis notebook
├── AICPA_regressionAnalysisData.csv
└── README.md
```

## Notes

I don't have the original assignment prompt/rubric — you may want to verify this matches what was actually assigned before publishing it.
