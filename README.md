# QuickCart Stockout Risk Prediction

A supervised machine learning project for predicting inventory stockout risk across QuickCart stores and products.

## 📌 Overview

Quick-commerce businesses need to maintain enough inventory to satisfy customer demand while avoiding unnecessary overstocking.

This project addresses a practical inventory-planning problem:

> **For every SKU at every store on every day, will the product remain sufficiently stocked until the next supplier delivery arrives?**

Each inventory record is classified into one of three stockout-risk categories:

- 🟢 **Safe** — Sufficient stock coverage is available.
- 🟡 **At-Risk** — Stock coverage is getting close to the replenishment requirement.
- 🔴 **Imminent** — Stock is expected to run out before the next supplier delivery arrives.

The project combines inventory, product, store, supplier, and event information to build a predictive classification system.

---

## 🎯 Objectives

The main objectives of this project are to:

- Prepare and integrate multiple related datasets.
- Identify and handle data-quality issues.
- Engineer meaningful inventory and demand-related features.
- Predict daily stockout risk using supervised machine learning.
- Compare different classification approaches.
- Evaluate model performance with particular attention to **Imminent stockout recall**.

---

## 📊 Dataset

The project contains five related datasets:

| Dataset | Description |
|---|---|
| `dim_stores.csv` | Store-level information |
| `dim_skus.csv` | Product/SKU information |
| `dim_suppliers.csv` | Supplier information |
| `dim_events.csv` | Festival and promotional event information |
| `fact_inventory_daily.csv` | Daily inventory records used for modeling |

The modeling table contains **21,600 records**, representing:

```text
12 stores × 60 SKUs × 30 days = 21,600 records
