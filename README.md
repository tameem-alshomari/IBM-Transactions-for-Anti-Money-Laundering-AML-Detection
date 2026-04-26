# IBM-Transactions-for-Anti-Money-Laundering-AML-Detection

IBM Transactions for Anti-Money Laundering (AML) Detection
This project implements a machine learning solution to detect illicit transactions using the IBM Transactions for Anti-Money Laundering dataset. The solution focuses on handling extreme class imbalance and capturing behavioral patterns through temporal feature engineering.

Project Overview
The primary challenge of this dataset is the high degree of class imbalance, where money laundering cases represent a tiny fraction of the total volume. This solution utilizes Gradient Boosted Decision Trees (LightGBM) and advanced feature engineering to identify suspicious financial flows.

Key Features
Memory Optimization: Implementation of a downcasting utility to handle large-scale financial data within limited RAM environments like Kaggle.

Temporal Engineering: Calculation of transaction velocity and rolling averages to identify sudden changes in account behavior.

Imbalance Handling: Utilization of the is_unbalance parameter and Area Under Precision-Recall Curve (AUPRC) optimization to ensure high recall for illicit activities.

Financial Signal Extraction: Features targeting "smurfing" (breaking large sums into small transactions) and cross-currency obfuscation.

Technical Stack
Language: Python

Libraries: Pandas, NumPy, LightGBM, Scikit-learn

Environment: Kaggle / Jupyter Notebooks

Implementation Details
Data Preprocessing
The pipeline converts raw timestamps into usable time-of-day features and sorts records to ensure temporal consistency. Categorical variables such as Payment Format and Currency are handled using native category encoding for better performance in tree-based models.

Feature Engineering
Three main types of features are generated:

Velocity Features: Tracking the frequency of transactions per account over a rolling window.

Monetary Shifts: Measuring the deviation of current transaction amounts from an account's historical average.

Cross-Entity Signals: Identifying currency mismatches and payment discrepancies.

Model Configuration
The LightGBM model is configured with the following parameters to maximize detection:

Objective: Binary

Metric: Average Precision (AUPRC)

Balance Strategy: is_unbalance=True

Boosting: GBDT with Early Stopping

Evaluation Metrics
Standard accuracy is not a reliable metric for this task. Instead, the model is evaluated based on:

AUPRC: The primary metric for measuring the trade-off between precision and recall in imbalanced datasets.

Recall: Ensuring that the maximum number of laundering cases are flagged for investigation.

Confusion Matrix: To visualize the balance between false positives and false negatives.
