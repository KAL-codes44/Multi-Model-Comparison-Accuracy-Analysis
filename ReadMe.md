## Here's the ReadMe for Iris Data Set Prediction Multi-Model Comparison & Accuracy Analysis

## 1. Project Overview
This project benchmarks seven machine learning classifiers on the classic Iris flower dataset from the UCI Machine Learning Repository. The data is manually split into separate Excel files for training (118 samples) and testing (32 samples). Model accuracy is computed using a custom comparison loop no built-in scoring utilities are used.
The goal is to understand not just which model performs best, but why different algorithms produce different accuracy scores on the same dataset


## 2. Dataset
# Source
UCI Machine Learning Repository — Iris Dataset
https://archive.ics.uci.edu/ml/datasets/iris
# Structure
•	Total samples: 150 (118 training + 32 testing)
•	Features: 4 numeric measurements per flower
•	Target: 3 species classes
# Features
•	sepallength — Sepal length in cm
•	sepalwidth  — Sepal width in cm
•	petallength — Petal length in cm
•	petalwidth  — Petal width in cm
# Target Classes
•	Iris-setosa
•	Iris-versicolor
•	Iris-virginica

## 3. Models Used
Seven classifiers from scikit-learn are trained and evaluated. Each model uses default hyperparameters unless otherwise noted.

Model	                                                              How It Works	                                                                                                            Strengths / Limitations
Random Forest	                Builds 100 decision trees on random data subsets and averages their votes	            Very robust; handles noise and small datasets well; rarely overfits
Decision Tree	                    Splits data by the feature that best separates classes at each node	                            Simple and interpretable; prone to overfitting on small data
K-Nearest Neighbors	        Predicts class based on the k=5 closest training samples by distance	                        Non-parametric; no training phase; can struggle with unscaled features
Support Vector Machine	    Finds the widest-margin hyperplane separating classes (RBF kernel)	                        Excellent on small-to-medium clean datasets; slow on very large data
Logistic Regression	            Models class probability via a sigmoid of a linear combination of features	                Fast and explainable; struggles when decision boundaries are non-linear
Gradient Boosting	            Sequentially builds trees, each correcting the errors of the previous	                        Powerful but slower; can overfit with too many trees on small data
Naive Bayes	                        Applies Bayes theorem assuming each feature contributes independently	                Very fast; accuracy suffers when the independence assumption is violated

## 4. Accuracy Results
Accuracy is computed manually by iterating over predictions and comparing each to the actual label. The formula used is:
accuracy (%) = (correct predictions / total predictions) × 100

Model		                                Test Acc	                               Key Reason
Random Forest		                93.75%	           Ensemble of trees covers all patterns
Decision Tree		                    90.625%	           Simple rules; can fully memorize small data
K-Nearest Neighbors		        93.75%	           Distance-based; sensitive to scale
Support Vector Machine	    	93.75%	           Strong on clean linearly-separable data
Logistic Regression		            90.65%	           Linear boundaries; less flexible
Gradient Boosting		            90.65%	           Sequential correction; can overfit small sets
Naive Bayes		                        96.875%	           Assumes feature independence (not always true)


## 5. Why Do Models Produce Different Accuracies?
Even on the same dataset, different algorithms yield different results because each makes fundamentally different assumptions about how to learn from data. The six key factors below explain the variation observed.

Factor	                                                    Explanation
Small test set (32 samples):	                    Each wrong prediction costs ~3.1%. One misclassification drops accuracy from 100% to 96.9%, so tiny differences are magnified.

Linear vs Non-linear boundaries:	        Iris classes are nearly linearly separable, but the versicolor/virginica boundary has slight overlap. Linear models (Logistic Regression) miss some of these edge cases.

Feature independence assumption:	    Naive Bayes assumes all four measurements are independent. In reality, petal length and width are highly correlated, which degrades its accuracy slightly.

Ensemble power:         	                        Random Forest and Gradient Boosting combine many weak learners. Even if individual trees make mistakes, the majority vote corrects them yielding consistently high accuracy.

Distance sensitivity in KNN:	                KNN relies on Euclidean distance. If features are on very different scales, one feature can dominate the distance metric. Feature scaling would likely boost KNN further.

Overfitting risk:	                                    Decision Trees can memorize small training sets perfectly (100% train accuracy) but this same memorisation can hurt generalisation though with 150 clean samples it still performs well.

## 6. Notes
•	Manual split: 
    Two separate Excel files are used instead of train_test_split(), giving full control over which samples are trained and tested on.
•	Manual accuracy loop: 
    A for-loop compares predictions element by element, no sklearn.metrics dependency.
•	Default hyperparameters: 
    All models use scikit-learn defaults. Tuning (e.g. grid search) would likely push lower-scoring models closer to 100%.
•	Small test set effect: 
    With only 32 test samples, each single misclassification equals a ~3.1% accuracy drop, which amplifies small model differences.

