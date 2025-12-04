---
date:
  created: 2025-11-23T15:00:00+09:00
  updated: 2025-11-23T15:50:00+09:00
authors:
  - abdukarimovhm
categories:
  - Tech Blog
tags:
  - Benchmarking
  - TabPFN V2
  - XGBoost
  - CatBoost
  - Tabular Data
---
# Benchmarking TabPFN V2 against XGboost and Catboost on Kaggle datasets

This study benchmarks CatBoost, XGBoost, and TabPFN V2 across multiple Kaggle datasets, including classification, regression, and time series tasks. TabPFN V2 showed strong performance on small datasets, often outperforming the boosting models without any feature engineering or preprocessing. However, it struggles with large datasets over 10,000 rows due to memory limitations, where XGBoost remains more effective, particularly for time series forecasting. Overall, TabPFN V2 is a powerful tool for quick experimentation on smaller tabular datasets but is less practical for large-scale applications.

**Side note: TabPFN V2.5 has been released.**

<!-- more -->

## 1. Objective

The objective of this study is to benchmark the performance of three models — **CatBoost**,
**XGBoost**, and **TabPFN V2** — across multiple Kaggle datasets. The aim is to evaluate how these
models perform on diverse tasks including binary classification, regression, and time series
forecasting. The focus is on comparing predictive accuracy, error metrics, and general
applicability of TabPFN V2 (a transformer-based model designed for tabular data) against
well-established gradient boosting models.

- **Note:** For comparison purposes, we did not perform feature engineering, missing
  value handling, or extensive data cleaning. All models were trained on the raw
  datasets to observe their out-of-the-box capabilities.

---

## 2. Datasets

The experiments were conducted on four Kaggle datasets covering different predictive modeling
tasks. A summary of each dataset is provided below:

| Dataset Name | Task Type | Target Variable | Number of Samples | Number of Features | Notes |
|---|---|---|---|---|---|
| **Titanic - Machine Learning from Disaster** | Binary Classification | Survived (0/1) | 891 (train set) | 11 (after cleaning) | Predict passenger survival |
| **House Prices - Advanced Regression Techniques** | Regression | SalePrice | 1,460 | 79 | Predict house sale prices |
| **Binary Prediction with a Rainfall Dataset** | Binary Classification | RainTomorrow (Yes/No) | 2,190 | 12 | Predict if it will rain tomorrow |
| **Forecasting Sticker Sales** | Time Series Forecasting | num_sold | 230,130 | 5 (date, country, store, product, id) | Predict sticker sales; missing values present in num_sold |


## 3. Results

The models were evaluated based on metrics appropriate to each task. For the **House Prices**
dataset, RMSLE (Root Mean Squared Log Error) was used in accordance with Kaggle’s official
evaluation method

- **Note:** Due to TabPFN V2’s limitation of handling a maximum of 10,000 rows, for large
  datasets (Sticker Sales), we performed random sampling of 10,000 entries and
  further split them into training and validation sets. CatBoost and XGBoost were also
  trained on the same sampled data to ensure a fair comparison.

| Dataset Name | Metric | CatBoost | XGBoost | TabPFN V2 | Notes |
|---|---|---|---|---|---|
| **Titanic - Machine Learning from Disaster** | Accuracy | 0.77511 | 0.73584 | 0.78947 | |
| **House Prices - Advanced Regression Techniques** | RMSLE (Root Mean Squared Log Error) | 0.1283 | 0.15554 | 0.11359 | Evaluated on log(predictions)vslog(actual) as per Kaggle |
| **Binary Prediction with a Rainfall Dataset** | AUC ROC | 0.84231 | 0.8458 | 0.86564 | |
| **Forecasting Sticker Sales** | RMSE | 102.08 | 89.56 | 99.24 | All models were trained on a sampled dataset of 10,000 entries. |


## 4. Observations

- **Titanic Dataset:** TabPFN V2 slightly outperformed CatBoost and XGBoost in terms of
  accuracy, showing good performance on smaller classification tasks without feature
  engineering.
- **House Prices:** TabPFN V2 achieved the lowest RMSLE, indicating strong generalization
  ability for regression problems with log-transformed targets, even when trained on raw
  data.
- **Rainfall Dataset:** TabPFN V2 achieved the highest AUC ROC, outperforming both boosting
  models despite no additional data preprocessing or feature engineering.
- **Sticker Sales:** XGBoost showed the best performance on time series forecasting.
  TabPFN V2 performed reasonably well, but its performance lagged

---

## 5. Limitations

During this benchmarking study, the following limitations were encountered:

- **TabPFN V2 Row Limitations:** TabPFN V2 officially supports datasets with up to 10,000 rows.
- **Handling Large Datasets:**
  - For the **Sticker Sales dataset** (230,130 samples), attempts to train on the full
    dataset by ignoring the 10,000-row limit resulted in failures:
    - On GPU (3.8 GB VRAM), the training failed due to out-of-memory errors.
    - On CPU, running TabPFN V2 on the full dataset caused the kernel to crash.
- Therefore, for **Sticker Sales**, we trained all models on a 10,000-entry random sample to
ensure comparability.

---

## 6. Conclusion

This benchmarking study demonstrates that **TabPFN V2**, trained on large-scale synthetic data and
leveraging in-context learning, can outperform or match established models like CatBoost and
XGBoost on small datasets with minimal preprocessing. Its ability to handle raw tabular data
without requiring feature engineering makes it a powerful tool for quick experimentation and
baseline modeling.

However, significant limitations arise when working with larger datasets beyond 10,000 rows, as
noted by the model’s creators. Attempts to run TabPFN V2 on large datasets resulted in memory
overloads and kernel crashes, making it impractical for large-scale training.

In summary:

- **TabPFN V2 is highly competitive or even superior on smaller datasets without preprocessing.**
- **It is not recommended for large datasets** due to its scalability limitations and resource
  consumption issues.
- **In domain-specific or structured time series forecasting tasks, models like XGBoost still outperform TabPFN V2.**
- Future improvements in scaling TabPFN V2 and adapting it for specialized tasks could make
  it a strong candidate for broader practical use.
