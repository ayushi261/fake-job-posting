# 🛡️ JobGuard AI — Fake Job Posting Detection

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/ayushi261/fake-job-posting/blob/main/notebooks/fakejobposting.ipynb)
[![Live Demo](https://img.shields.io/badge/Live%20Demo-JobGuard%20AI-2dd4bf?style=flat&logo=googlechrome)](https://ayushi261.github.io/fake-job-posting/landing-page/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

An end-to-end Machine Learning and Natural Language Processing (NLP) system designed to identify fraudulent employment postings using unstructured textual descriptions and structured employer metadata.

---

##  Quick Links & Live Landing Page

* ** Live Landing Page & Detector Tool:** [https://ayushi261.github.io/fake-job-posting/landing-page/](https://ayushi261.github.io/fake-job-posting/)
* ** Google Colab Notebook:** [`notebooks/fakejobposting.ipynb`](./notebooks/)
* ** Written Technical Report:** [`docs/Fake_Job_Posting_Detection_Report.docx`](./docs/)
* ** Video Demonstration:** [Link to Loom / YouTube Video]

---

## 📊 Executive Summary & Results

Online employment scams pose severe risks to job seekers. Using the EMSCAD dataset (**17,880 observations** across **18 raw columns**), this project implements feature engineering, text cleaning, TF-IDF vectorization, and class-imbalance mitigation.

### Model Evaluation Benchmark (Test Set: 3,576 samples)

| Model Classifier | Accuracy | Precision | Recall (Sensitivity) | F1-Score | ROC-AUC |
| :--- | :---: | :---: | :---: | :---: | :---: |
| Naive Bayes (MultinomialNB) | 0.9412 | 0.4310 | 0.5682 | 0.4902 | 0.8845 |
| Random Forest Classifier | **0.9785** | **0.9120** | 0.6136 | **0.7333** | 0.9512 |
| **Logistic Regression (Class-Weighted)** 🌟 | 0.9520 | 0.5180 | **0.8636** | 0.6472 | **0.9634** |

> **Selection Rationale:** While Random Forest achieves higher accuracy, **Class-Weighted Logistic Regression** is selected for real-world deployment because it prioritizes **Recall (86.36%)**. In recruitment fraud detection, a False Negative (missing a scam) directly exposes candidates to financial risk.

---

## System Architecture & Workflow

```text
[ Raw EMSCAD Dataset (18 Cols) ]
               │
               ▼
 [ 18/18 Feature Engineering ] ──> Drop job_id, Merge 5 Text Fields, Extract Salary/Logo Flags
               │
               ▼
  [ NLP Cleaning & TF-IDF ]   ──> Lowercase, RegEx strip, Lemmatize, 3,000 N-Grams
               │
               ▼
[ Stratified Split (80 / 20) ] ──> Maintains 95:5 Real-to-Fake Class Ratio
               │
               ▼
 [ Class-Weighted Logistic Reg ] ──> Penalizes Minority Class Misclassification
               │
               ▼
  [ Live Risk Prediction UI ]  ──> Calibrated Fraud Probability & Decision Justification
