# Forecasting Peak Electricity Demand in New South Wales (NSW)

## Project Overview

This project develops and evaluates time series forecasting models for predicting **daily maximum electricity demand** in **New South Wales (NSW), Australia**, using historical demand data from **January 2024 through October 2025**.

Accurate electricity demand forecasting is essential for:
- Maintaining grid stability  
- Preventing power outages  
- Optimizing energy generation and cost management  

This analysis compares **ARIMA**, **Exponential Smoothing (ETS)**, and **Time Series Linear Models (TSLM)** to determine the most effective approach for forecasting peak daily electricity demand.

✅ **Final selected model:**  
**ETS(M,A,M)** – *Multiplicative error, additive trend, multiplicative seasonality*

This model successfully captured:
- An upward demand trend  
- Weekly seasonality  
- Changing variation in demand over time  

---

## Repository Structure

| File | Description |
|------|------------|
| `MaximumDemand.ipynb` | Full data preparation, modeling, evaluation, and forecasting workflow |
| `combined.csv` | Raw 5-minute interval electricity demand data (NSW) |
| `README.md` | Project documentation (this file) |

---

## Dataset Description

**Source:** Australian Energy Market Operator (AEMO)  
**Region:** New South Wales  
**Raw Frequency:** 5-minute intervals  
**Date Range:** January 2024 – October 2025  
**Target Variable:** Total electricity demand (MW)

The raw dataset was aggregated to **daily maximum values**, resulting in **639 daily observations**.

**Final fields used in the analysis:**
- `Date` – Observation date
- `MaxDemand` – Maximum daily electricity demand (MW)

**Descriptive statistics:**
- Minimum: **7,623 MW**
- Maximum: **13,764 MW**
- Mean: **9,750 MW**
- Range: **6,141 MW**

---

## Methods & Models

The following time series models were implemented and compared:

### 🔹 ARIMA
- Manual: ARIMA(0,1,1)(0,1,1)[7]
- Automatic: ARIMA(1,1,2)(0,0,2)[7]

### 🔹 TSLM (Time Series Linear Model)
- Manual: `trend + trend² + weekly seasonality`
- Automatic: `trend + weekly seasonality`

### ✅ ETS (Final Model)
- Manual: **ETS(M,A,M)**
- Automatic: ETS selected via `ETS()`

The **ETS(M,A,M)** model provided the best fit and forecast accuracy.

---

## Model Evaluation

Models were evaluated using a **holdout test set (October 2025)** and assessed using:

- RMSE – Root Mean Squared Error
- MAE – Mean Absolute Error
- MAPE – Mean Absolute Percentage Error
- Residual Diagnostics (Ljung-Box Test)

### Accuracy Comparison

| Model | RMSE (MW) | MAPE (%) |
|------|----------|----------|
| ✅ ETS(M,A,M) | **686** | **4.97** |
| Best ARIMA | 742 | 6.42 |
| Best TSLM | 1556 | 17.69 |

A Box-Cox transformation (λ ≈ -0.9) was tested but **rejected** because back-transformed forecasts performed worse than the original-scale ETS model.

---

## How to Run This Project

1. Clone this repository
```bash
git clone https://github.com/alligmckernan/ADS-506-Team-4-Final-Project
