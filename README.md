<!-- omit in toc -->
# DengAI: Predicting Disease Spread
<!-- omit in toc -->
### Predict H1N1 and Seasonal Flu Vaccines
**DrivenData Competition:** https://www.drivendata.org/competitions/44/dengai-predicting-disease-spread/

Using environmental data collected by U.S. Federal Government agencies to predict the number of dengue fever cases reported each week in San Juan, Puerto Rico and Iquitos, Peru.

[![Live Demo](https:/img.shields.io/badge/Live%20Demo-Streamlit-red)](https://url.streamlit.app)
[![Competition](https:/img.shields.io/badge/DrivenData-%2366-blue)](https://www.drivendata.org/competitions/44/dengai-predicting-disease-spread/)

---
<!-- omit in toc -->
## Table of Contents

- [Competition](#competition)
  - [Problem Definition](#problem-definition)
  - [Task](#task)
  - [Getting the Data](#getting-the-data)
    - [Data Files](#data-files)
- [Environment Setup](#environment-setup)
  - [Project Structure](#project-structure)
  - [Local Setup](#local-setup)
  - [Tech Stack](#tech-stack)
- [Results and Key Findings](#results-and-key-findings)
  - [Results](#results)
  - [Key Findings](#key-findings)


---

## Competition

### Problem Definition
Dengue fever is a mosquito-borne disease that occurs in tropical and sub-tropical parts of the world. In mild cases, symptoms are similar to the flu: fever, rash, and muscle and joint pain. In severe cases, dengue fever can cause severe bleeding, low blood pressure, and even death. In recent years dengue fever has been spreading. Historically, the disease has been most prevalent in Southeast Asia and the Pacific islands. These days many of the nearly half billion cases per year are occurring in Latin America.

Because it is carried by mosquitoes, the transmission dynamics of dengue are related to climate variables such as temperature and precipitation. An understanding of the relationship between climate and dengue dynamics can improve research initiatives and resource allocation to help life-threatening pandemics.

### Task

Using environmental data collected by various U.S. Federal Government agencies, from the Centers for Disease Control and Prevention to the National Oceanic and Atmospheric Administration in the U.S. Department of Commerce, predict the number of dengue fever cases reported each week in San Juan, Puerto Rico and Iquitos, Peru. The competition metric is **Mean Absolute Error (MAE)**.

### Getting the Data

1. Sign up or log in at https://www.drivendata.org
2. Join the competition at the link above
3. Go to the **Data** tab and download all files into `data/raw/`

#### Data Files

| File | Description |
|------|-------------|
| `training_set_features.csv` | Weekly environmental features for 1,456 training weeks |
| `training_set_labels.csv` | Weekly dengue case counts for each training week |
| `test_set_features.csv` | Weekly environmental features for 416 test weeks |
| `submission_format.csv` | Template showing the required submission structure |

## Environment Setup

### Project Structure

```
dengai-predict-disease-spread/
├── data/
│   ├── raw/                              # Raw competition files (not committed)
│   └── processed/                        # Cleaned and engineered datasets
├── notebooks/
│   ├── 01_eda.ipynb
│   ├── 02_data_cleaning.ipynb
│   ├── 03_feature_engineering.ipynb
│   ├── 04_baseline_models.ipynb
│   ├── 05_advanced_models.ipynb
│   └── 06_model_evaluation.ipynb
├── models/                               # Saved model files (not committed)
├── submissions/                          # Competition CSV files
├── reports/           
│   └── figures                            # EDA and evaluation plots
├── requirements.txt
└── README.md
```

### Local Setup

```bash
git clone https://github.com/YOUR_USERNAME/dengai-predict-disease-spread.git
cd dengai-predict-disease-spread
python -m venv venv && source venv/bin/activate
pip install -r requirements.txt
jupyter notebook notebooks/01_eda.ipynb
```

### Tech Stack

Python | pandas | scikit-learn | XGBoost | LightGBM | SHAP | matplotlib | seaborn

---

## Results and Key Findings

### Results

| **Model** | **SJ CV MAE** | **IQ CV MAE** | **Combined CV MAE** |
|-----------|---------------|---------------|---------------------|
| Naive (mean) baseline | - | - | 23.00 |
| Ridge | 33.03 | 7.60 | 23.95 |
| Random Forest | 28.94 | 7.43 | 21.25 |
| XGBoost | 28.90 | 7.66 | 21.31 |
| XGBoost + LightGBM ensemble | 27.01 | 7.07 | 19.89 |
| **LightGBM (city-specific)** | **23.54** | **6.63** | **17.50** |

Hold-out evaluation (last 20% of training data per city):

| **City** | **MAE** | **RMSE** | **R-squared** |
|-----------|---------------|---------------|---------------------|
| San Juan | 6.52 | 15.57 | 0.750 |
| Iquitos | 2.70 | 6.91 | 0.634 |
| Overall (weighted) | 5.16 | - | - |


### Key Findings

**What works:** City-specific LightGBM models with L1 objective outperform all other approaches, achieving a 24% improvement over the naive baseline. Training separate models for San Juan and Iquitos is critical. The two cities have different climate patterns, case magnitudes, and seasonal drivers.

**Most important features**

*San Juan:* Long-run (12-week rolling) minimum temperature and relative humidity dominate. Sustained warm nights and high humidity over months, not individual spikes, predict dengue burden.

*Iquitos:* Seasonality (week-of-year cyclical encoding) is the single strongest signal, followed by atmospheric moisture (dew point, specific humidity). Dengue in Iquitos follows the wet season closely and predictably.

**Feature engineering matters:** Adding temporal lags (1-12 weeks) and rolling window features (4, 8, 12 weeks) was the largest single driver of improvement, reflecting the ~2-week mosquito lifecycle and ~1-2-week transmission delay between environmental conditions and reported cases.

**Public health implication:** For San Juan, a 12-week sustained humidity + temperature composite is the key monitoring signal. For Iquitos, seasonal calendar timing is sufficient for basic resource pre-positioning; short-term humidity deviations provide secondary early-warning value.

---

DrivenData. (2015). *DengAI: Predicting Disease Spread.* Retrieved May 10, 2026 from https://www.drivendata.org/competitions/44/dengai-predicting-disease-spread/.