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
  - TabPFN
  - XGBoost
  - CatBoost
  - Tabular Data
---
# Benchmarking TabPFN against XGboost and Carboost on Kaggle datasets

This study benchmarks CatBoost, XGBoost, and TabPFN across multiple Kaggle datasets, including classification, regression, and time series tasks. TabPFN showed strong performance on small datasets, often outperforming the boosting models without any feature engineering or preprocessing. However, it struggles with large datasets over 10,000 rows due to memory limitations, where XGBoost remains more effective, particularly for time series forecasting. Overall, TabPFN is a powerful tool for quick experimentation on smaller tabular datasets but is less practical for large-scale applications.

<!-- more -->

## 1. Objective

The objective of this study is to benchmark the performance of three models — **CatBoost**,
**XGBoost**, and **TabPFN** — across multiple Kaggle datasets. The aim is to evaluate how these
models perform on diverse tasks including binary classification, regression, and time series
forecasting. The focus is on comparing predictive accuracy, error metrics, and general
applicability of TabPFN (a transformer-based model designed for tabular data) against
well-established gradient boosting models.

- **Note:** For comparison purposes, we did not perform feature engineering, missing
  value handling, or extensive data cleaning. All models were trained on the raw
  datasets to observe their out-of-the-box capabilities.

---

## 2. Datasets

The experiments were conducted on four Kaggle datasets covering different predictive modeling
tasks. A summary of each dataset is provided below:

![Kaggle datasets](/assets/images/blog/kaggle-datasets.png)

---

## 3. Results

The models were evaluated based on metrics appropriate to each task. For the **House Prices**
dataset, RMSLE (Root Mean Squared Log Error) was used in accordance with Kaggle’s official
evaluation method

- **Note:** Due to TabPFN’s limitation of handling a maximum of 10,000 rows, for large
  datasets (Sticker Sales), we performed random sampling of 10,000 entries and
  further split them into training and validation sets. CatBoost and XGBoost were also
  trained on the same sampled data to ensure a fair comparison.

![Kaggle datasets results](/assets/images/blog/kaggle-results.png)

---

## 4. Observations

- **Titanic Dataset:** TabPFN slightly outperformed CatBoost and XGBoost in terms of
  accuracy, showing good performance on smaller classification tasks without feature
  engineering.
- **House Prices:** TabPFN achieved the lowest RMSLE, indicating strong generalization
  ability for regression problems with log-transformed targets, even when trained on raw
  data.
- **Rainfall Dataset:** TabPFN achieved the highest AUC ROC, outperforming both boosting
  models despite no additional data preprocessing or feature engineering.
- **Sticker Sales:** XGBoost showed the best performance on time series forecasting.
  TabPFN performed reasonably well, but its performance lagged

---

## 5. Limitations

During this benchmarking study, the following limitations were encountered:

- **TabPFN Row Limitations:** TabPFN officially supports datasets with up to 10,000 rows.
- **Handling Large Datasets:**
  - For the **Sticker Sales dataset** (230,130 samples), attempts to train on the full
    dataset by ignoring the 10,000-row limit resulted in failures:
    - On GPU (3.8 GB VRAM), the training failed due to out-of-memory errors.
    - On CPU, running TabPFN on the full dataset caused the kernel to crash.
- Therefore, for **Sticker Sales**, we trained all models on a 10,000-entry random sample to
ensure comparability.

---

## 6. Conclusion

This benchmarking study demonstrates that **TabPFN**, trained on large-scale synthetic data and
leveraging in-context learning, can outperform or match established models like CatBoost and
XGBoost on small datasets with minimal preprocessing. Its ability to handle raw tabular data
without requiring feature engineering makes it a powerful tool for quick experimentation and
baseline modeling.

However, significant limitations arise when working with larger datasets beyond 10,000 rows, as
noted by the model’s creators. Attempts to run TabPFN on large datasets resulted in memory
overloads and kernel crashes, making it impractical for large-scale training.

In summary:

- **TabPFN is highly competitive or even superior on smaller datasets without preprocessing.**
- **It is not recommended for large datasets** due to its scalability limitations and resource
  consumption issues.
- **In domain-specific or structured time series forecasting tasks, models like XGBoost still outperform TabPFN.**
- Future improvements in scaling TabPFN and adapting it for specialized tasks could make
  it a strong candidate for broader practical use.
