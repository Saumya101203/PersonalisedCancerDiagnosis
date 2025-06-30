# Personalized Cancer Diagnosis - ML-Based Genomic Classification

This project aims to classify genetic mutations into predefined cancer-related classes based on structured genomic data and associated clinical literature. It was inspired by the [MSKCC Kaggle Challenge](https://www.kaggle.com/c/msk-redefining-cancer-treatment), and focuses on building interpretable, probabilistic machine learning models suitable for real-world clinical use.

---

## 🧬 Problem Statement

Given a set of gene mutations and their corresponding clinical evidence in text format, classify each mutation into one of nine cancer-related classes. The classification must be:

- **Probabilistic** (i.e., return the probability of each class)
- **Interpretable** (critical in healthcare)
- **Accurate**, minimizing the log-loss metric

---

## 📁 Dataset

The dataset comes from **Memorial Sloan Kettering Cancer Center (MSKCC)** via Kaggle and includes:

- `training_variants.csv`: Structured data (ID, Gene, Variation, Class)
- `training_text.csv`: Unstructured clinical literature (ID, Text)

---

## 🔍 Project Pipeline

### 1. Data Preprocessing
- Merged gene, variation, and text data on ID
- Cleaned clinical text with lowercasing, punctuation removal, stopword filtering (using NLTK)

### 2. Feature Engineering
- Gene & Variation: One-Hot Encoding, Response Coding
- Text: Bag-of-Words representation (optional)
- Final feature matrix constructed by stacking categorical and text features

### 3. Train / CV / Test Split
- Stratified split with ratios 64% / 16% / 20%
- Class distribution preserved in all splits

---

## 🤖 Models Implemented

| Model                     | Log Loss     | Misclassification Rate |
|--------------------------|--------------|-------------------------|
| Naïve Bayes              | 1.23         | 38.5%                   |
| K-Nearest Neighbors      | **1.05**     | 35.7%                   |
| Logistic Regression (CB) | 1.07         | **34.4%**               |
| Logistic Regression      | 1.09         | 34.2%                   |
| Linear SVM               | 1.12         | 35.1%                   |
| Random Forest (OHE)      | 1.16         | 39.4%                   |
| Random Forest (RC)       | 1.83         | 71.2%                   |
| Stacking Classifier      | 1.14         | 36.6%                   |
| Majority Voting Classifier| 1.18        | 35.9%                   |

- **CB** = Class Balanced
- **OHE** = One-Hot Encoding
- **RC** = Response Coding

---

## 🧠 Key Insights

- Gene and text features were highly predictive; variation less so due to high cardinality and sparse coverage.
- K-NN yielded the lowest log loss, while class-balanced Logistic Regression minimized classification error.
- Ensemble methods (Stacking and Majority Voting) improved robustness.

---

## ⚙️ How to Run

### Requirements

Install dependencies via:

```bash
pip install -r requirements.txt
```
Or manually install key packages:
```bash
pip install numpy pandas scikit-learn matplotlib seaborn nltk imbalanced-learn mlxtend
```
Also, make sure to download NLTK stopwords:
```bash
import nltk
nltk.download('stopwords')
```
### 🚀 Running on Google Colab
If you are using Google Colab, follow these steps to set up the dataset:
- **1. Upload Dataset to Google Drive**
  Create a folder in your Google Drive:
```
  My Drive/
└── cancer_diagnosis_project/
    ├── training_variants.csv
    └── training_text.csv
```
- **2. Mount Drive in Colab**
  ```
  from google.colab import drive
  drive.mount('/content/drive')
  ```
  
### ▶️ Run the Notebook
- Open notebooks/Personalized_Cancer_Diagnosis.ipynb in Colab or Jupyter.
- Run all cells sequentially to reproduce results.
- Visualizations and model outputs will be generated in-place.
