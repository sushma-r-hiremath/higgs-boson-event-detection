# Higgs Boson Event Detection using Machine Learning

## 📌 Problem Description

In particle physics, a **collision event** can either be a **signal** (indicating the presence of a Higgs boson) or a **background** event (explained by known physical processes).

The goal of this project is to **classify particle collision events** as:
- **Signal (Higgs boson present)** or
- **Background (no Higgs boson)**

This is a **binary classification problem** where machine learning helps physicists identify rare Higgs boson events from a large amount of noisy data.

---

## 🎯 Why This Problem Matters

- Higgs boson events are **extremely rare**
- Manual detection is impractical
- Machine learning helps:
  - Improve detection accuracy
  - Reduce false positives
  - Speed up scientific discovery

This project demonstrates how **data science and ML can solve real-world scientific problems**.

---

## 📊 Dataset

- Dataset: **Higgs Boson Challenge Dataset**
- Source: Kaggle  
- Link: https://www.kaggle.com/c/higgs-boson

### Dataset Details
- **Training samples:** 250,000
- **Test samples:** 550,000
- **Features:** 30 numerical physics-based features
- **Target:**  
  - `s` → Signal  
  - `b` → Background

### How to Get the Data
1. Create a Kaggle account
2. Download the dataset from the link above
3. Place `training.csv` inside the `data/` folder

---

## 🧪 Exploratory Data Analysis (EDA)

The notebook (`notebook.ipynb`) includes:
- Class distribution analysis
- Missing value handling (`-999` values)
- Feature distributions
- Signal vs background comparison
- Correlation heatmaps
- Feature importance analysis

EDA helped identify:
- Important physics features
- Class imbalance
- Need for feature engineering

---

## 🛠 Feature Engineering

Additional features were created to improve model performance:
- Sum of multiple physics features
- Ratios between momentum and mass
- Interaction terms

These features improved model separability between signal and background.

---

## 🤖 Model Training

### Models Used
- **CatBoost Classifier**
  - Well-suited for tabular data
  - Handles missing values
  - Performs well on imbalanced datasets

### Training Strategy
- Train–validation split (80/20)
- Stratified sampling
- ROC-AUC as primary metric
- Cross-validation for stability

### Evaluation Metrics
- Accuracy
- ROC-AUC
- Confusion Matrix

---

## 🚀 Project Structure

