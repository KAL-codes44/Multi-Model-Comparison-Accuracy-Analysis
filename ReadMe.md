# Iris Dataset Prediction — Multi-Model Comparison & Accuracy Analysis

## 1. Project Overview
This project benchmarks **seven machine learning classifiers** on the classic **Iris flower dataset** from the **UCI Machine Learning Repository**.

The dataset is manually split into **two Excel files**:
- Training set: **118 samples**
- Testing set: **32 samples**

Model accuracy is calculated using a **custom comparison loop** (no built-in scoring utilities are used).

The goal of this project is not only to determine **which model performs best**, but also to understand **why different algorithms produce different accuracy scores on the same dataset**.

---

# 2. Dataset

## Source
UCI Machine Learning Repository — Iris Dataset  
https://archive.ics.uci.edu/ml/datasets/iris

## Structure
- Total samples: **150**
- Training samples: **118**
- Testing samples: **32**
- Features: **4 numeric measurements per flower**
- Target: **3 species classes**

## Features
- **sepallength** — Sepal length in cm  
- **sepalwidth** — Sepal width in cm  
- **petallength** — Petal length in cm  
- **petalwidth** — Petal width in cm  

## Target Classes
- Iris-setosa  
- Iris-versicolor  
- Iris-virginica  

---

# 3. Models Used

Seven classifiers from **scikit-learn** are trained and evaluated.  
Each model uses **default hyperparameters** unless otherwise noted.

| Model | How It Works | Strengths / Limitations |
|------|--------------|-------------------------|
| Random Forest | Builds many decision trees on random subsets and averages their predictions | Robust, handles noise well, reduces overfitting |
| Decision Tree | Splits data using feature rules that best separate classes | Simple and interpretable but can overfit |
| K-Nearest Neighbors | Predicts class based on the closest training samples | Non-parametric but sensitive to feature scaling |
| Support Vector Machine | Finds the maximum margin hyperplane separating classes | Very effective for small clean datasets |
| Logistic Regression | Uses a linear model with a sigmoid probability function | Fast and interpretable but limited for nonlinear data |
| Gradient Boosting | Builds trees sequentially correcting previous errors | Powerful but can overfit on small datasets |
| Naive Bayes | Applies Bayes theorem assuming feature independence | Very fast but assumption may reduce accuracy |

---

# 4. Accuracy Results

Accuracy is computed manually using the formula:
accuracy (%) = (correct predictions / total predictions) × 100


| Model | Test Accuracy | Key Reason |
|------|---------------|-----------|
| Random Forest | 93.75% | Ensemble trees capture multiple patterns |
| Decision Tree | 90.625% | Simple rules can memorize small datasets |
| K-Nearest Neighbors | 93.75% | Distance-based classification |
| Support Vector Machine | 93.75% | Strong on well-separated data |
| Logistic Regression | 90.65% | Linear decision boundary |
| Gradient Boosting | 90.65% | Sequential learning from errors |
| Naive Bayes | 96.875% | Fast probabilistic classification |

---

# 5. Why Do Models Produce Different Accuracies?

Even on the same dataset, different algorithms produce different results because they **learn patterns differently**.

### Key Factors

**Small Test Set (32 samples)**  
Each wrong prediction costs ~3.1% accuracy.  
One misclassification can drop accuracy from **100% → 96.9%**.

**Linear vs Non-Linear Boundaries**  
Iris classes are almost linearly separable, but **versicolor and virginica overlap slightly**.

**Feature Independence Assumption**  
Naive Bayes assumes features are independent.  
However **petal length and width are highly correlated**.

**Ensemble Power**  
Random Forest and Gradient Boosting combine multiple trees, improving prediction stability.

**Distance Sensitivity in KNN**  
KNN depends on Euclidean distance. Without feature scaling some features dominate the metric.

**Overfitting Risk**  
Decision Trees can memorize small datasets which may reduce generalization.

---

# 6. Notes

**Manual Data Split**  
Two separate Excel files are used instead of `train_test_split()`.

**Manual Accuracy Calculation**  
A simple loop compares predicted and actual labels.
