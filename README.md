# Oil Price Time Series Forecasting — ARIMA vs LSTM

## Project Overview

This project analyses and forecasts crude oil prices using two different time-series modelling approaches:

1. **ARIMA (AutoRegressive Integrated Moving Average)** – a classical statistical model used for time series forecasting.
2. **LSTM (Long Short-Term Memory Neural Network)** – a deep learning model capable of capturing complex nonlinear patterns in sequential data.

The objective of this project is to compare the forecasting performance of ARIMA and LSTM models on oil price data and evaluate their ability to predict future price movements.

---

## Dataset

The dataset contains daily oil prices covering the period:

## Technologies and Libraries Used

This project was implemented in **Python** using the following libraries:

* NumPy
* Pandas
* Matplotlib
* Seaborn
* Statsmodels
* TensorFlow / Keras
* Scikit-learn
* SciPy

---

## Project Workflow

The project follows a complete **time series forecasting pipeline**.

### 1. Data Loading and Validation

The dataset is loaded and validated using a custom `OilPriceLoader` class.

Steps performed:

* Import dataset
* Convert date column
* Sort time index
* Detect missing values
* Check duplicate dates
* Generate descriptive statistics

---

### 2. Exploratory Data Analysis (EDA)

Exploratory analysis is performed to understand the characteristics of oil prices.

Visualisations include:

* Daily oil price trajectory
* Rolling mean trends
* Rolling volatility
* Monthly average prices
* Distribution of daily returns

These analyses help identify volatility patterns and potential non-stationarity in the series.

---

### 3. Stationarity Testing

Time series models such as ARIMA require stationary data.

Two statistical tests are applied:

**Augmented Dickey-Fuller (ADF) Test**

* Null hypothesis: series contains a unit root (non-stationary)

**KPSS Test**

* Null hypothesis: series is stationary

First-order differencing is applied to achieve stationarity.

---

### 4. ARIMA Model

An **exhaustive grid search** is performed to identify the optimal ARIMA parameters.

Parameter search:

```
p = 0–8
d = 0–2
q = 0–8
```

Model selection is based on:

* AIC (Akaike Information Criterion)
* BIC (Bayesian Information Criterion)

---

### 5. ARIMA Model Diagnostics

Residual diagnostics are performed to ensure model validity:

* Residual time plot
* Residual autocorrelation (ACF)
* Histogram with normal distribution
* Q-Q plot
* Ljung-Box autocorrelation test
* Shapiro-Wilk normality test

These tests confirm whether residuals behave like white noise.

---

### 6. ARIMA Forecasting

The ARIMA model is evaluated using a **train-test split**.

Test window:

```
60 days
```

Evaluation metrics:

* RMSE
* MAE
* MAPE

The model also generates a **24-month future forecast** with confidence intervals.

---

## Deep Learning Model — LSTM

### 7. LSTM Data Preprocessing

The dataset is prepared for neural network training using:

* **MinMax scaling**
* **Sliding window sequences**

Parameters used:

```
Lookback window: 30 days
Test size: 60 days
```

---

### 8. LSTM Model Architecture

The neural network architecture used in this project:

```
Bidirectional LSTM (128 units)
Dropout (0.3)
LSTM (64 units)
Dropout (0.3)
Dense (32)
Dense (1)
```

Additional training strategies:

* Early stopping
* Learning rate reduction
* Validation monitoring

---

### 9. LSTM Forecasting

The trained LSTM model generates predictions for the test set and is evaluated using:

* RMSE
* MAE
* MAPE

---

### 10. Uncertainty Estimation

To quantify prediction uncertainty, **Monte Carlo Dropout** is applied during inference.

Method:

* 30 stochastic simulations
* Recursive multi-step forecasting
* Confidence intervals generated using percentile bounds

This approach approximates a Bayesian predictive distribution.

---

## Model Comparison

Both models are compared using out-of-sample test performance.

Evaluation metrics:

* Root Mean Squared Error (RMSE)
* Mean Absolute Error (MAE)
* Mean Absolute Percentage Error (MAPE)

A visual comparison and performance table are generated to identify the best performing model.

---

## Forecast Results

Both models generate **24-month forward projections**.
