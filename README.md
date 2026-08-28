# QuickCart Stockout Risk Prediction

A supervised machine learning project for predicting daily inventory stockout risk across QuickCart stores and products.

## 📌 Overview

Quick-commerce businesses need to maintain enough inventory to satisfy customer demand while avoiding unnecessary overstocking.

This project addresses a practical inventory-planning problem:

> For every SKU at every store on every day, will the product remain sufficiently stocked until the next supplier delivery arrives?

Each inventory record is classified into one of three stockout-risk categories:

- 🟢 **Safe** — Sufficient stock coverage is available.
- 🟡 **At-Risk** — Stock coverage is getting close to the replenishment requirement.
- 🔴 **Imminent** — Stock is expected to run out before the next supplier delivery arrives.

The project combines inventory, product, store, supplier, and event information to build a predictive classification system.

## 🎯 Objectives

The main objectives of this project are to:

- Prepare and integrate multiple related datasets.
- Identify and handle data-quality issues.
- Engineer meaningful inventory and demand-related features.
- Predict daily stockout risk using supervised machine learning.
- Compare different classification approaches.
- Evaluate model performance with particular attention to Imminent stockout recall.

## 📊 Dataset

The project uses five related datasets:

- `dim_stores.csv` — Store-level information.
- `dim_skus.csv` — Product and SKU information.
- `dim_suppliers.csv` — Supplier information.
- `dim_events.csv` — Festival and promotional event information.
- `fact_inventory_daily.csv` — Daily inventory records used for modeling.

The modeling dataset contains 21,600 records representing 12 stores, 60 SKUs, and 30 days of inventory observations.

Each inventory record represents a specific Store × SKU × Date combination.

## 🏷️ Target Variable

The target variable is `stockout_risk`.

It contains three classes:

- **Safe** — Days of stock cover exceeds the replenishment wait by 3 or more days.
- **At-Risk** — Days of stock cover is within 3 days of the replenishment wait.
- **Imminent** — Stock will run out, or has already run out, before the next delivery arrives.

The target is imbalanced, with Safe being the majority class and Imminent being the minority class.

## 🔍 Data Preparation

The datasets were inspected for dimensions, data types, missing values, duplicate records, key relationships, and date consistency.

Two deliberate data-quality issues were addressed:

- Inconsistent capitalization in the `city_display` column was standardized.
- Missing supplier reliability values were handled through median imputation.

The five datasets were then joined into a single modeling dataset, with the daily inventory table acting as the central table.

## ⚙️ Feature Engineering

The following features were created based on the project specification:

- `reorder_gap` — Difference between the reorder point and closing stock.
- `days_of_cover_ratio` — Days of cover normalized by expected supplier lead time.
- `supplier_reliability_clean` — Clean numerical supplier reliability.
- `is_recent_reorder` — Indicates whether a reorder was recently placed for the same store-SKU combination.
- One-hot encoded category features.
- `day_of_month` — Day of the month extracted from the date.
- `days_since_festival_start` — Number of days relative to the start of the festival period.

## 📈 Exploratory Analysis

The analysis examined the key business signals highlighted in the project.

Festival periods showed a significant increase in Imminent stockout risk compared with non-festival days.

Supplier reliability also showed a clear relationship with stockout risk, with lower-reliability suppliers associated with higher Imminent rates.

Perishable products showed a higher Imminent stockout rate than non-perishable products.

These patterns demonstrate the importance of demand changes, supplier reliability, and product characteristics when predicting inventory risk.

## 🤖 Machine Learning

Three classification approaches were evaluated:

**Majority-Class Baseline**

A baseline model that always predicts the majority class, Safe. This provides a reference point for determining whether the machine learning models provide meaningful improvement.

**Multinomial Logistic Regression**

An interpretable multiclass classification model used to predict Safe, At-Risk, and Imminent inventory conditions.

**Random Forest**

A tree-based ensemble model capable of capturing nonlinear relationships between inventory, demand, supplier, store, and temporal features.

## 🧪 Train/Test Strategy

Because the same Store × SKU combinations appear across multiple days, a random row-level split could introduce information leakage.

A time-based split was therefore used:

- Training period: October 1–23, 2026.
- Testing period: October 24–30, 2026.

This provides a more realistic evaluation by using earlier dates for training and later dates for testing.

## 📏 Model Evaluation

The models were evaluated using accuracy, precision, recall, F1-score, and confusion matrices.

Special attention was given to **recall for the Imminent class**.

This is particularly important because failing to identify a genuine stockout can lead to lost sales, empty shelves, and poor customer experience.

Therefore, the model with the highest overall accuracy is not automatically considered the best model. The ability to correctly identify Imminent cases is a key consideration.

## 🔎 Feature Importance

Random Forest feature importance was analyzed to identify the variables that contributed most to the model's predictions.

This provides additional insight into the inventory, demand, supplier, product, and temporal factors associated with stockout risk.

## 💡 Key Takeaways

This project demonstrates an end-to-end supervised machine learning workflow for an operational inventory problem.

It covers:

- Multi-table data integration.
- Data-quality handling.
- Missing-value treatment.
- Feature engineering.
- Class imbalance.
- Time-based model validation.
- Information leakage prevention.
- Multiclass classification.
- Model comparison.
- Confusion-matrix analysis.
- Feature importance.
- Business-focused model evaluation.

The project demonstrates why machine learning evaluation should consider the business cost of different types of errors rather than relying only on overall accuracy.

## 🛠️ Technologies Used

Python, Pandas, NumPy, Matplotlib, Scikit-learn, Google Colab, and GitHub.

## 📁 Project Structure

```text
QuickCart-Stockout-Risk-Prediction/
│
├── QuickCart_Stockout_Risk.ipynb
├── README.md
├── .gitignore
│
└── data/
    └── Dataset files


