# Predicting ED-to-Ward Waiting Times in Singapore Public Hospitals

INF2008 Machine Learning Project

## Project Overview

This project develops a predictive model for median waiting times from Emergency Department (ED) arrival to hospital ward admission across 10 Singapore public hospitals. The goal is to enable hospitals to forecast patient flow and optimize resource allocation.

## Repository Structure
```
├── data/
│   ├── WT for Admission to Ward.csv
│   ├── Attendances at EMD.csv
│   ├── Bed Occupancy Rate.csv
│   ├── public holidays.csv
│   ├── combined_hospital_daily_metrics.csv  (cleaned)
│   └── disease_data_2023_2026.csv  (infectious disease data)
├── Stage_1/
│   ├── Stage_1_Submission.ipynb
│   └── group06_labP2_stage1.pdf
├── Stage_2/
│   ├── INF2008_Stage2_Final.ipynb
│   └── group06_labP2_stage2.pdf
└── README.md
```

## Dataset

| Source | Granularity | Period |
|--------|-------------|--------|
| Waiting Time for Admission to Ward | Daily x Hospital | Jan 2023 - Jan 2026 |
| ED Attendance | Daily x Hospital | Jan 2023 - Jan 2026 |
| Bed Occupancy Rate | Daily x Hospital | Jan 2023 - Jan 2026 |
| Public Holidays | Date list | 2023 - 2026 |
| Infectious Disease Bulletin | Weekly | 2023 - 2026 |

Final cleaned dataset: 9,415 rows x 7 columns across 10 hospitals.

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

## Stage 2: Advanced Modelling

**Objective:** Improve upon Stage 1 baseline using feature engineering, external data, and hyperparameter tuning.

**Key Improvements:**
- sklearn Pipeline with ColumnTransformer (prevents data leakage)
- Temporal features (Lag_1_WaitTime)
- External data integration (Infectious disease data 2023-2026)
- Controlled ablation experiments for hyperparameter tuning

**Champion Model:** Random Forest Regressor
- n_estimators: 200
- max_depth: 10
- min_samples_leaf: 10

**Results:**

| Model | MAE (hrs) | RMSE (hrs) | R² |
|-------|-----------|------------|-----|
| Stage 1 Linear Regression | 2.44 | 3.67 | 0.40 |
| Stage 2 Random Forest | 1.40 | 2.44 | 0.74 |

**42.5% MAE improvement over Stage 1 baseline.**

**Ablation Study Results:**

| Experiment | Hypothesis | Best Value |
|------------|------------|------------|
| n_estimators | More trees reduce variance | 200 |
| max_depth | Depth limit reduces overfitting | 10 |
| Lag features | Lag captures temporal patterns | True |
| min_samples_leaf | Larger leaves reduce overfitting | 10 |

**Feature Set Comparison:**

| Feature Set | MAE | R² |
|-------------|-----|-----|
| Baseline | 2.308 | 0.473 |
| + Lag Features | 1.656 | 0.716 |
| + Disease Features | 2.028 | 0.608 |
| + Lag + Disease | 1.661 | 0.719 |

## Tools

- Python 3.12
- pandas, numpy, scikit-learn
- matplotlib, seaborn
- Google Colab

## References

- MOH Hospital Statistics: https://www.moh.gov.sg/others/resources-and-statistics/
- Singapore Public Holidays: data.gov.sg
- Weekly Infectious Disease Bulletin: https://www.cda.gov.sg/resources/
