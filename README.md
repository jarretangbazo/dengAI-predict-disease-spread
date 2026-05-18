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
Dengue fever is a mosquito-borne disease that occurs in tropical and sub-tropical parts of the world. In mild cases, symptoms are similar to the flu: fever, rash, and muscle and joint pain. In severe cases, dengue fever can cause severe bleeding, low blood pressure, and even death.

Because it is carried by mosquitoes, the transmission dynamics of dengue are related to climate variables such as temperature and precipitation. Although the relationship to climate is complex, a growing number of scientists argue that climate change is likely to produce distributional shifts that will have significant public health implications worldwide.

In recent years dengue fever has been spreading. Historically, the disease has been most prevalent in Southeast Asia and the Pacific islands. These days many of the nearly half billion cases per year are occurring in Latin America.

**Why it matters**
An understanding of the relationship between climate and dengue dynamics can improve research initiatives and resource allocation to help fight life-threatening pandemics.

### Task

Using environmental data collected by various U.S. Federal Government agencies—from the Centers for Disease Control and Prevention to the National Oceanic and Atmospheric Administration in the U.S. Department of Commerce, predict the number of dengue fever cases reported each week in San Juan, Puerto Rico and Iquitos, Peru.

### Getting the Data

1. Sign up or log in at https://www.drivendata.org
2. Join the competition at the link above
3. Go to the **Data** tab and download all files into `data/raw/`

#### Data Files

| File | Description |
|------|-------------|
| `training_set_features.csv` | Survey responses for ~26,700 training respondents |
| `training_set_labels.csv` | The two vaccine targets for each training respondent |
| `test_set_features.csv` | Survey responses for ~26,700 test respondents |
| `submission_format.csv` | Template showing the required submission structure |

## Environment Setup

### Project Structure

```
dengai-predict-disease-spread/
├── data/
│   ├── raw/             # Raw competition files (not committed)
│   ├── processed/       # Cleaned and engineered datasets
├── notebooks/           # EDA and experimentation
│   ├── 01_eda.ipynb
│   ├── 02_data_cleaning.ipynb
│   └── 03_feature_engineering.ipynb
│   └── 04_baseline_models.ipynb
│   └── 05_advanced_models.ipynb
│   └── 06_model_evaluation.ipynb
├── reports/           
│   ├── figures
├── src/
│   ├── features.py      # Feature engineering functions
│   ├── train.py         # Training and MLflow logging script
│   └── api.py           # FastAPI deployment
├── models/              # Saved model files (not committed)
├── submissions/         # Competition CSV files
├── logs/                # Prediction and monitoring logs
├── app.py               # Streamlit demo app
├── Dockerfile
├── requirements.txt
```

### Local Setup

```bash
git clone https://github.com/YOUR_USERNAME/dengai-predict-disease-spread.git
cd dengai-predict-disease-spread
python -m venv venv && source venv/bin/activate
pip install -r requirements.txt
streamlit run app.py
```

To launch the MLflow experiment dashboard:
```bash
mlflow ui   # opens at http://localhost:5000
```

To run the prediction API:
```bash
uvicorn src.api:app --reload    #opens at http://localhost:8000
```

### Tech Stack

Python | pandas | scikit-learn | XGBoost | LightGBM | SHAP | Optuna | MLflow | FastAPI | Docker | Streamlit

---

## Results and Key Findings

### Results

| Model | H1N1 AUC | Seasonal AUC | Mean AUC |
|-------|----------|--------------|----------|
| Logistic Regression (baseline) | | | |
| XGBoost (tuned) | | | |
| XGBoost + LightGBM ensemble | | | |


### Key Findings

*Summary of key findings forthcoming*

---

DrivenData. (2015). *DengAI: Predicting Disease Spread.* Retrieved May 10, 2026 from https://www.drivendata.org/competitions/44/dengai-predicting-disease-spread/.