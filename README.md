# 📈 AdEase Business Case Study: Wikipedia Page View Forecasting

## 📘 About The Project

**AdEase** is a digital advertising company focused on helping clients achieve **maximum clicks at minimal cost**.

This project analyzes **Wikipedia page view data** across multiple languages over 550 days. The primary goal is to leverage data science and **time series forecasting** to predict future page view traffic. By accurately forecasting these trends, AdEase can **optimize ad placements** on high-traffic pages, ensuring a better **ROI** for its clients across different regions.

---

## 🚀 What We Did: A High-Level Overview

This repository contains the end-to-end data science workflow for forecasting page views.

### 1. 🧹 Data Exploration and Processing
* **Loaded Data:** The analysis started with a dataset of 145,000 Wikipedia pages and their daily view counts over 550 days.
* **Handled Missing Values:** We identified that `NaN` values represented dates before a page was created. These were filled with `0` to indicate zero views.
* **Feature Engineering:** Used regex to extract key features from the `Page` column, including page `language`, `access_type`, and `access_origin` (spider vs. agent).
* **Aggregation:** Grouped the data by language to create aggregated time series, identifying 'English' as the language with the most page views.

### 2. 📊 Time Series Analysis
* **Visualization:** Plotted the aggregated time series for each language to identify overall trends, seasonality, and unusual spikes (like one from July-Aug 2016).
* **Stationarity:** Used the **Augmented Dickey-Fuller test** to check for stationarity. Most languages, including English, were found to be non-stationary.
* **ACF/PACF:** Analyzed Autocorrelation and Partial Autocorrelation plots to understand the seasonal patterns (e.g., weekly) and determine potential model parameters.

### 3. 🧠 Forecasting & Modeling
The analysis focused on forecasting the non-stationary 'English' language data, comparing three different models:

* **ARIMA:** A simple ARIMA model was established as a baseline for performance.
* **SARIMAX:** To improve the forecast, we used a SARIMAX model, which accounts for **weekly seasonality** (a 7-day cycle). We then enhanced it further by including **exogenous variables** (a separate file mapping campaign/event dates), which significantly improved accuracy.
* **Prophet:** Implemented Facebook's **Prophet** model, which is robust for handling seasonality, trends, and external regressors (events/campaigns).

---

## 💡 Key Findings & Conclusion

* **Best Model:** The **SARIMAX** model that incorporated **exogenous variables** (campaign flags) performed the best, achieving the lowest Mean Absolute Percentage Error (MAPE) at **5.4%**.
* **Key Insight:** Simply forecasting based on past views is not enough. External events, like marketing campaigns, have a significant and measurable impact on page traffic.
* **Recommendation:** AdEase can significantly improve its ad placement strategy by adopting models like **SARIMAX** or **Prophet** that can effectively integrate data on external events.

---

## 🛠️ Technologies Used

* **Data Analysis:** Pandas, NumPy, re (Regex)
* **Data Visualization:** Matplotlib, Seaborn
* **Time Series Modeling:**
    * Statsmodels (ARIMA, SARIMAX, seasonal_decompose, ACF/PACF, ADF Test)
    * Prophet (by Facebook)
* **Model Evaluation:** Scikit-learn (MAE, MSE, MAPE)
