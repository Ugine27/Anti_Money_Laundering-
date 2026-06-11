# Anti-Money Laundering Detection using Graph Analytics and XGBoost

## Overview

Developed an Anti-Money Laundering (AML) detection system to identify suspicious financial transactions within highly imbalanced banking datasets. The project combines graph analytics, feature engineering, and XGBoost classification to detect illicit transaction patterns and improve financial crime detection.

## Problem Statement

Money laundering transactions represent an extremely small fraction of banking activity, making them difficult to detect using traditional machine learning approaches. The objective of this project is to identify suspicious transactions while minimizing false positives in a highly imbalanced environment.

## Key Questions Addressed

### Why is AML Detection Difficult?

- Illicit transactions constitute only ~0.1% of total transactions.
- Traditional accuracy metrics become misleading because a model predicting all transactions as legitimate can still achieve very high accuracy.
- Effective AML systems require specialized evaluation metrics and sampling strategies.

### Why Use Graph-Based Features?

- Money laundering is rarely visible from a single transaction.
- Suspicious behaviour emerges through transaction networks and account interactions.
- Graph analytics help identify:
  - Circular money movement
  - High-risk intermediary accounts
  - Complex transaction chains
  - Central nodes within laundering networks

### Why Perform Undersampling?

- Training directly on millions of legitimate transactions causes models to ignore rare illicit cases.
- Undersampling creates a balanced training environment while preserving the real-world distribution in testing.
- Multiple negative-to-positive ratios were evaluated to determine the optimal balance between precision and recall.

### Why Use PR-AUC Instead of Accuracy?

- Accuracy is unreliable for extreme class imbalance.
- Precision-Recall AUC focuses specifically on identifying rare positive events.
- PR-AUC was selected as the primary optimization metric throughout model development and tuning.

## Dataset

- IBM Anti-Money Laundering Dataset
- Training Dataset: HI-Small
- Testing Dataset: LI-Small
- Millions of transaction records
- Extremely imbalanced classification problem

## Methodology

### Data Processing

- Cleaned and validated transaction records.
- Created separate training and testing pipelines.
- Applied frequency encoding for high-cardinality features.
- Performed robust scaling to reduce the impact of outliers.

### Feature Engineering

#### Aggregation Features

- Total transactions sent
- Total transactions received
- Average transaction amount
- Fan-In
- Fan-Out

#### Graph Analytics Features

- Degree Centrality
- Connected Component Size
- Cycle Detection
- PageRank
- Transaction Network Connectivity

### Model Development

- XGBoost Classifier
- Cross-validation based model selection
- RandomizedSearchCV hyperparameter tuning
- Multiple undersampling ratios tested:
  - 1:1
  - 5:1
  - 10:1
  - 20:1

### Model Evaluation

Metrics used:

- Precision-Recall AUC (Primary Metric)
- ROC-AUC
- Precision
- Recall
- F1-Score

## Results

- PR-AUC: 0.1465
- ROC-AUC: 0.956
- Evaluated on 3.46 million unseen transactions
- Approximately 285× improvement over random detection performance

## Tech Stack

- Python
- Pandas
- NumPy
- SciPy
- Scikit-learn
- XGBoost
- Matplotlib
- Seaborn

## Applications

- Anti-Money Laundering (AML)
- Fraud Detection
- Financial Crime Analytics
- Banking Compliance
- Transaction Monitoring Systems

## Key Takeaways

- Accuracy is not suitable for evaluating highly imbalanced AML datasets.
- Graph-based features significantly improve laundering detection performance.
- Undersampling is essential for learning rare-event patterns.
- PR-AUC provides a more meaningful evaluation than ROC-AUC in extreme imbalance settings.
- Hyperparameter tuning improves model generalization and detection capability.

## Future Improvements

### Graph Neural Networks (GNNs)

- Learn directly from transaction networks.
- Capture more complex laundering behaviour patterns.

### Sequence-Based Modelling

- Model temporal transaction behaviour.
- Detect evolving laundering schemes.

### Currency Normalization

- Standardize transactions across currencies.
- Improve cross-border transaction analysis.

### Real-Time Monitoring

- Deploy the model as a streaming transaction monitoring system.
- Enable real-time suspicious activity alerts.

### Explainable AI

- Integrate SHAP and feature importance analysis.
- Improve interpretability for compliance teams.

## Impact

This project demonstrates how graph analytics and machine learning can be combined to detect financial crime within highly imbalanced transaction datasets. The solution successfully identifies suspicious patterns across millions of transactions while maintaining strong predictive performance and scalability.
