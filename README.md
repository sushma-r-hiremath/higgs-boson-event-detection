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

## 📁 Project Structure (Detailed)

```text
higgs-boson-event-detection/
│
├── data/
│   ├── training.csv          # Higgs Boson training dataset
│   └── README.md             # Instructions to obtain the dataset
│
├── model/
│   └── catboost_model.cbm    # Trained CatBoost model artifact
│
├── src/
│   ├── train.py              # Model training script
│   └── predict.py            # Flask API for inference
│
├── notebook.ipynb            # EDA and experimentation
├── requirements.txt          # Python dependencies
├── Dockerfile                # Docker container configuration
└── README.md                 # Project documentation



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

---

## 📈 Results and Model Evaluation

This section summarizes the quantitative performance of the trained model
and demonstrates its ability to distinguish Higgs boson signal events from
background events.

---

### 🔹 Evaluation Metrics Used

The following metrics were chosen due to class imbalance in the dataset:

- **ROC-AUC** – Measures how well the model separates signal from background
- **Accuracy** – Overall correctness of predictions
- **Confusion Matrix** – Detailed breakdown of prediction outcomes
- **Cross-Validation ROC-AUC** – Stability across multiple data splits

---

### 🔹 Validation Performance

The CatBoost classifier achieved the following performance on the validation set:

- **ROC-AUC:** ~0.91  
- **Accuracy:** ~85–88% (varies by split)

A high ROC-AUC score indicates strong separability between Higgs signal
and background events.

---

### 🔹 Confusion Matrix (Validation Set)

The confusion matrix below summarizes the model’s predictions:

| Actual \ Predicted | Background (0) | Signal (1) |
|--------------------|----------------|------------|
| **Background (0)** | True Negatives  | False Positives |
| **Signal (1)**     | False Negatives | True Positives  |

**Interpretation:**
- True Positives: Correctly identified Higgs events
- True Negatives: Correctly identified background events
- False Positives: Background events predicted as Higgs
- False Negatives: Missed Higgs events

The model maintains a good balance between detecting rare signal events
and minimizing false positives.

---

### 🔹 Cross-Validation Results

To ensure robustness, stratified 5-fold cross-validation was performed.

- **Mean ROC-AUC (5-fold):** ~0.90+
- Performance remained stable across all folds

This indicates that the model generalizes well and is not overfitting
to a specific train/validation split.

---

### 🔹 Feature Importance

Feature importance analysis shows that physics-derived features such as:

- `DER_mass_MMC`
- `DER_pt_h`
- `DER_mass_vis`
- `DER_deltar_tau_lep`

contribute most significantly to distinguishing Higgs signal events.

This aligns well with physical intuition, as Higgs events cluster around
specific mass and momentum ranges.

---

### 🔹 API Inference Example

Once deployed via Docker, the model can be queried using a REST API.

#### Example Request
```json
{
  "DER_mass_MMC": 125,
  "DER_pt_h": 45
}

#### Example Request

signal_probability : 0.23159195881853417
