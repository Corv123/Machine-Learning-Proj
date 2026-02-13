# Predicting ED-to-Ward Waiting Times in Singapore Public Hospitals

INF2008 Machine Learning Project

## Project Overview

This project develops a predictive model for median waiting times from Emergency Department (ED) arrival to hospital ward admission across 9 Singapore public hospitals. The goal is to enable hospitals to forecast patient flow and optimize resource allocation.

## Repository Structure
```
├── data/
│   ├── WT for Admission to Ward.csv
│   ├── Attendances at EMD.csv
│   ├── Bed Occupancy Rate.csv
│   ├── public holidays.csv
│   └── combined_hospital_daily_metrics.csv  (cleaned)
├── Stage_1/
│   ├── Stage_1_Submission.ipynb
│   └── group06_labXX_stage1.pdf
└── README.md
```

## Dataset

| Source | Granularity | Period |
|--------|-------------|--------|
| Waiting Time for Admission to Ward | Daily x Hospital | Jan 2023 - Jan 2026 |
| ED Attendance | Daily x Hospital | Jan 2023 - Jan 2026 |
| Bed Occupancy Rate | Daily x Hospital | Jan 2023 - Jan 2026 |
| Public Holidays | Date list | 2023 - 2026 |

Final cleaned dataset: 9,415 rows x 7 columns across 9 hospitals.

## Stage 1: Baseline Modelling

**Objective:** Establish baseline feasibility using CRISP-DM methodology.

**Models (default parameters):**
- DummyRegressor (mean baseline)
- Linear Regression
- Decision Tree Regressor

**Results:**

| Model | MAE (hrs) | R² |
|-------|-----------|-----|
| Dummy (Mean) | 3.36 | -0.001 |
| Linear Regression | 2.44 | 0.40 |
| Decision Tree | 2.83 | -0.11 |

Linear Regression achieved 27.4% improvement over the dummy baseline.

## Stage 2: Planned Improvements

- Hyperparameter tuning for Decision Tree
- Feature engineering (lagged waiting times, rolling averages)
- External data integration (infectious disease rates, air quality)
- Alternative framing as multi-class classification

## Tools

- Python 3.12
- pandas, numpy, scikit-learn
- matplotlib, seaborn
- Google Colab

## References

- MOH Hospital Statistics: https://www.moh.gov.sg/others/resources-and-statistics/
- Singapore Public Holidays: data.gov.sg
