# FinalProject-CLY
Final Project - Detecting Online Fraudulent Activity (anomaly detection)

Overview
This project builds a high‑performance fraud detection model using the IEEE‑CIS Fraud Detection dataset from Kaggle. The dataset mirrors real-world e‑commerce fraud patterns, including device spoofing, synthetic identities, and behavioral anomalies. The final LightGBM model achieves an AUC of 0.9556, demonstrating strong discriminatory power for identifying fraudulent transactions.

Dataset
The project uses two tables merged on TransactionID:

Transaction Table: transaction amount, product codes, card metadata, device/browser info, timestamps, fraud label

Identity Table: device type, OS, browser, network attributes

The combined dataset contains 400+ features and 1M+ rows, requiring memory optimization before modeling.

Key Steps
1. Memory Optimization
A custom downcasting function reduced RAM usage by ~46%, enabling smooth processing in Google Colab.

2. Exploratory Data Analysis
Severe class imbalance

High missingness in identity fields

Right‑skewed transaction amounts

Weak raw correlations → feature engineering essential

3. Feature Engineering
Includes:

Time features (hour, day, weekday)

Email domain grouping

Device/browser normalization

Frequency encoding for cards & addresses

Log/sqrt transforms for TransactionAmt

Aggregation features (mean, std, count per card/address/device)

These engineered features significantly improved model performance.

4. Model Development
A LightGBM classifier was selected for its speed, handling of missing values, and performance on large tabular data.

Key hyperparameters:

num_leaves = 64

learning_rate = 0.05

feature_fraction = 0.8

bagging_fraction = 0.8

num_boost_round = 300

Early stopping (100 rounds)

Validation AUC: 0.9556

5. Feature Importance
Top contributors included:

TransactionAmt

card1_trans_mean

card1_freq

addr1

card2_trans_mean

P_emaildomain_trans_count

These align with known fraud patterns such as unusual spending, inconsistent card behavior, and suspicious email domains.

6. Interactive Prediction Demo
A single‑transaction scoring function outputs a clear fraud probability for real‑time use cases.

Results
AUC: 0.9556

Strong ROC curve performance

Robust handling of high‑dimensional, imbalanced data

Business Impact
This workflow supports:

Real‑time fraud scoring

Risk‑based authentication

Analyst investigation queues

Device & identity anomaly detection

Future Work
Add unsupervised anomaly detection (Isolation Forest, Autoencoders)

GPU‑accelerated hyperparameter tuning

SHAP explainability for analyst‑friendly insights
