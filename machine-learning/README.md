# Machine Learning

Notes and solutions related to machine learning concepts, models, and practical applications.

## Roadmap

Learn the stages in order. Each one assumes the previous stage.

As you finish a subtopic, add the resource URL in the **Resource** column (docs, course, notes, or project).

| Stage | Focus |
| --- | --- |
| [1. Python](#1-python) | Working with data in code |
| [2. Mathematics](#2-mathematics) | The ideas behind the models |
| [3. Data](#3-data) | Turning raw data into features |
| [4. Classical ML](#4-classical-ml) | Models for tabular problems |
| [5. Deep learning](#5-deep-learning) | Models for images, text, and sequences |
| [6. Specialization](#6-specialization) | One applied track |
| [7. Production](#7-production) | Shipping and maintaining models |

### 1. Python

Read and write scripts before modeling libraries.

| Subtopic | Resource |
| --- | --- |
| Python basics (syntax, functions, classes) | |
| NumPy (arrays, broadcasting, linear ops) | [NumPy docs](https://numpy.org/doc/) |
| pandas (DataFrames, filtering, groupby) | |
| matplotlib / seaborn (plots and EDA visuals) | |

### 2. Mathematics

Linear algebra for data and weights. Calculus for how models learn. Probability and statistics for uncertainty and evaluation.

| Subtopic | Resource |
| --- | --- |
| Linear algebra (vectors, matrices, eigenvalues) | |
| Calculus (derivatives, gradients, chain rule) | |
| Probability (distributions, Bayes, expectation) | |
| Statistics (sampling, hypothesis testing, bias/variance) | |

### 3. Data

Most of the work is here: missing values, leakage, scaling, encoding, and a split that matches how the model will be used.

| Subtopic | Resource |
| --- | --- |
| Data cleaning (missing values, outliers, types) | |
| Exploratory data analysis (EDA) | |
| Feature engineering (encoding, scaling, transforms) | |
| Train / validation / test splits | |
| Data leakage and validation design | |

### 4. Classical ML

Start with linear models, then trees and boosting. Learn metrics and cross-validation before deeper architectures.

| Subtopic | Resource |
| --- | --- |
| Linear regression | |
| Logistic regression | |
| Classification vs regression | |
| Clustering (k-means, hierarchical) | |
| Decision trees | |
| Random forests | |
| Gradient boosting (XGBoost / LightGBM / CatBoost) | |
| Evaluation metrics (accuracy, precision, recall, F1, ROC-AUC, RMSE) | |
| Cross-validation | |
| Regularization (L1 / L2) and overfitting | |

### 5. Deep learning

Build a small network so backpropagation is concrete, then use PyTorch.

| Subtopic | Resource |
| --- | --- |
| Neural networks (layers, activations, loss) | |
| Backpropagation and gradient descent | |
| PyTorch basics (tensors, autograd, training loop) | |
| Convolutional neural networks (CNNs) | |
| Sequence models (RNN / LSTM / GRU) | |
| Transformers and attention | |
| Transfer learning and fine-tuning | |

### 6. Specialization

Finish one applied track. Depth on a single path is more useful than a survey of every subfield.

| Subtopic | Resource |
| --- | --- |
| Natural language processing (NLP) | |
| Computer vision | |
| Recommendation systems | |
| Time series forecasting | |

### 7. Production

Track experiments, version data and models, serve predictions, and watch for drift.

| Subtopic | Resource |
| --- | --- |
| Experiment tracking (MLflow / W&B) | |
| Model packaging and serving (API / batch) | |
| Data and model versioning | |
| Monitoring and data/model drift | |
| CI/CD for ML pipelines | |

## Projects

| Project | Description |
| --- | --- |
| [Smart Invoice System](https://github.com/SanjayKushwah0601/smart-invoice-system) | End-to-end machine learning project |
