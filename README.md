# BEES – Order Days Prediction (Data Science Challenge)

## Project Overview

This project addresses a real-world logistics optimization problem proposed in the **BEES Data Science Challenge**.  
The objective is to **predict the remaining number of order days in a month for each user**, at any point in time, using historical transaction data and partial current-month information.

The solution is designed to be **interpretable, statistically grounded, and scalable**, aligning with practical business constraints.

---

## Problem Statement

For each user, we want to predict:

> **How many days the user will still place at least one order during the remainder of August 2022**

Key characteristics of the problem:

- A user may place **multiple orders on the same day**, but this still counts as **one order day**
- Predictions must consider:
  - Orders already observed in August
  - Historical ordering behavior
  - (Optionally) forecasted total monthly sales
- Some users have **no observed August orders** (missing values)

---

## Data Sources

The solution uses the following datasets:

### 1. `historical_orders.parquet`
- Complete transaction history
- Used as the **training dataset**
- Enables estimation of:
  - Typical number of order days per month
  - Inter-arrival times between order days
  - User-level behavioral patterns

### 2. `august_with_missing_order_days.parquet`
- Partial August 2022 data
- Some users have:
  - Known order days
  - No observed orders yet (NaN)
- All users in this file must receive a prediction

### 3. `august_total_sales.parquet`
- Forecasted total August sales per user
- Treated as **ground truth**
- Used as an auxiliary signal to refine predictions

---

## Modeling Strategy

### Target Variable
For each user:

