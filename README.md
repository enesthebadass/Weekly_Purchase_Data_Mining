# 🧠 AI-Based Weekly Purchase Prediction using CatBoost

## 📌 Project Overview

This project aims to predict **in which week of February** a customer will purchase a specific product, based on their historical transaction data from the previous 7 months (June to January). We approach this as a **multi-class classification problem**, where the model predicts the week number (1 to 4/5) or 0 if no purchase is expected.

We utilize advanced feature engineering, including customer and product-level statistics, and apply a CatBoost classifier to train the model. Predictions are generated for a test set containing customer-product pairs.

---

## 📅 Problem Definition

- **Input:** 7 months of transaction data (June 1 to January 31)
- **Goal:** For each customer-product pair in the test set, predict **in which week of February** the product will be purchased (1 to 4/5). If the product is not expected to be purchased, predict **0**.
- **Model type:** Multi-class classification

---

## 📁 Dataset

### `transactions.csv`
Historical purchase data containing:
- `customer_id`
- `product_id`
- `purchase_date`
- `quantity`

### `test.csv`
Pairs of customers and products for which the model should predict the purchase week.

---

## 🔍 Feature Engineering

We derived several features based on transaction history:

- **Temporal features:**
  - `week_number`: Calculated from purchase_date
  - `month`: Numeric month extracted from purchase_date

- **Customer features:**
  - `mean`, `std`, `sum`, `count` of purchased quantities
  - `purchase frequency` per customer

- **Product features:**
  - Aggregate statistics similar to customers

- **Filtering logic:**
  - Customers with an average purchase frequency >28 days were labeled with `target_week = 0` (i.e., unlikely to repurchase in February)

---

## 🧠 Model

We use the `CatBoostClassifier` due to its strong performance on categorical data and ability to handle missing values.

**Training:**
- Model: CatBoostClassifier
- Iterations: 500
- Depth: 6
- Learning rate: 0.1
- Categorical features: `customer_id`, `product_id`

---

## 📈 Evaluation Results

The model was evaluated using accuracy and classification metrics on a hold-out validation set.

