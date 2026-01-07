# Higgs Boson Event Detection using Machine Learning

## 📌 Project Overview

This project builds an **end-to-end machine learning pipeline** to classify
particle collision events as either:

- **Signal** → Higgs boson present  
- **Background** → Standard Model processes

The project demonstrates **real-world ML engineering**, including:
- Data exploration
- Feature engineering
- Model training
- API-based inference
- Dockerized deployment

---

## 🧠 Problem Background

In particle physics experiments (such as CERN’s ATLAS detector), millions of
collision events are recorded. Only a **very small fraction** correspond to
Higgs boson production.

Manually identifying these events is impossible.

**Machine learning enables automatic detection of Higgs-like patterns** from
high-dimensional physics measurements.

---

## 🎯 Objective

Train a binary classifier that predicts the **probability** that a given
collision event is a Higgs boson signal.

---

## 📊 Dataset

- **Source**: Kaggle Higgs Boson Challenge
- **Training samples**: 250,000
- **Features**: 30 numerical physics features
- **Target**:
  - `s` → signal
  - `b` → background

### Dataset Characteristics
- Imbalanced classes (more background than signal)
- Missing values encoded as `-999`
- Physics-derived and detector-measured features

---

## 🧪 Exploratory Data Analysis (EDA)

EDA is performed in `notebook.ipynb` and includes:

- Class balance visualization
- Missing value analysis
- Feature distributions
- Signal vs background comparisons
- Correlation heatmaps
- Feature importance analysis

**Key insights**:
- Higgs-like events cluster around specific mass and momentum ranges
- Certain derived physics features are highly discriminative

---

## 🛠 Feature Engineering

Additional features were created to improve model performance:
- Feature sums (energy proxies)
- Ratios between momentum and mass
- Interaction terms

Missing values were handled using **median imputation**.

---

## 🤖 Model Training

### Model Used
- **CatBoost Classifier**
  - Excellent for tabular data
  - Robust to feature interactions
  - Handles complex non-linear patterns

### Training Details
- Train/validation split: 80/20
- Evaluation metric: ROC-AUC
- Cross-validation for stability

### Performance
- **Validation ROC-AUC ≈ 0.91**
- Stable performance across folds

---

## 🚀 Project Structure (DETAILED)

higgs-boson-event-detection/
│
├── data/
│ └── training.csv
│ └── README.md # Instructions to obtain dataset
│
├── model/
│ └── catboost_model.cbm # Trained model artifact
│
├── src/
│ ├── train.py # Model training script
│ ├── predict.py # Flask API for inference
│
├── notebook.ipynb # EDA + experimentation
├── requirements.txt # Python dependencies
├── Dockerfile # Containerization config
└── README.md # Project documentation


---

## 📂 File Descriptions

### `notebook.ipynb`
- Exploratory Data Analysis
- Feature engineering experiments
- Model evaluation and interpretation

### `src/train.py`
- Loads dataset
- Preprocesses features
- Trains CatBoost model
- Saves trained model to `model/`

### `src/predict.py`
- Loads trained model
- Exposes `/predict` endpoint
- Accepts JSON input
- Returns signal probability
- Automatically fills missing features for robustness

### `Dockerfile`
- Builds a reproducible environment
- Packages model and API
- Exposes port 9696

---
