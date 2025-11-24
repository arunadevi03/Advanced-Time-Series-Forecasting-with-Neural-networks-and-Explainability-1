Project Title:
Advanced Time Series Forecasting Using LSTM, SARIMAX & Explainability Techniques (AEP Hourly Dataset)


---

📌 1. Overview

This project focuses on advanced time-series forecasting using deep learning (LSTM) and classical statistical modeling (SARIMAX).
The dataset consists of hourly electricity load measurements from American Electric Power (AEP).

To meet robust industry and academic standards, the project incorporates:

Multivariate synthetic feature generation

LSTM neural network forecasting

Optuna-based hyperparameter optimization

SARIMAX as a classical baseline

SHAP explainability

Sensitivity analysis on input window sizes and forecast horizons

Reproducible pipeline with config files and saved models


This project is fully automated and produces evaluation metrics, plots, and model files in a results/ directory.


---

📌 2. Project Objectives

1. Develop a multivariate time-series dataset using original AEP load and synthetic external regressors.


2. Build and optimize an LSTM forecasting model using sliding-window sequences.


3. Create a classical baseline model using SARIMAX with exogenous variables.


4. Provide explainability through SHAP values.


5. Evaluate forecasting performance across multiple window sizes and horizons.


6. Generate a reproducible configuration file and final report output.




---

📌 3. Dataset

The project uses:

File: AEP_hourly.csv
Columns:

Datetime (timestamp)

AEP_MW (hourly electricity consumption)


Synthetic Multivariate Features Added

Since external data was not allowed, realistic regressors were generated:

temp_synth (synthetic temperature)

hum_synth (synthetic humidity)

hour, dayofweek, month, is_weekend

Lag features: lag_24, lag_48, lag_168

Rolling means: rolling_24_mean, rolling_168_mean


These features create a valid multivariate dataset used by both LSTM and SARIMAX.


---

📌 4. Project Structure

│
├── project_complete.py # Main runnable script
├── config.json # Model configuration file
├── README.md # Project documentation
│
└── results/
    ├── metrics.csv
    ├── sarimax_metrics.csv
    ├── final_config.json
    ├── report_summary.txt
    ├── figures/
    │ ├── forecast_win24_h1.png
    │ ├── shap_win24_h1.png
    │ ├── ...
    └── models/
        ├── lstm_win24_h1.h5
        ├── scaler_X.pkl
        └── scaler_y.pkl


---

📌 5. Installation

Run the following:

pip install pandas numpy matplotlib seaborn scikit-learn tensorflow statsmodels optuna shap joblib

For SHAP on CPU:

pip install shap


---

📌 6. Running the Project

Simply run:

python project_complete.py

All outputs will be saved in the results/ directory.


---

📌 7. Methodology

7.1 Data Preprocessing

Enforced hourly frequency with asfreq("H")

Interpolated missing values

Added lag features, rolling averages, and synthetic weather

Standardized features using StandardScaler

Created sliding-window sequences for LSTM


7.2 LSTM Model

Multi-step output

Tuned using Optuna:

Units: 32 / 64 / 128

Layers: 1–2

Dropout: 0.0–0.3

Learning rate: 1e-4 – 1e-2


Trained with:

EarlyStopping

ModelCheckpoint

30 epochs

Batch size = 64



7.3 SARIMAX Baseline

Order: (1,1,1)

Seasonal: (1,1,1,24)

Exogenous variables used: all multivariate columns


7.4 Explainability

SHAP DeepExplainer (fallback to KernelExplainer when required)

Feature importance plots saved under results/figures/


7.5 Sensitivity Analysis

Tested combinations:

Window Size Horizons

24 1, 24
48 1, 24


Results saved in metrics.csv.


---

📌 8. Results Summary

Results are written to:

results/metrics.csv

results/sarimax_metrics.csv

results/report_summary.txt


Key Outputs:

LSTM generally outperforms SARIMAX in RMSE and MAE

SHAP reveals top contributing features are lag-based and synthetic temperature

Larger windows improve long-horizon accuracy



---

📌 9. Key Features of the Project

✔ Multivariate time series

✔ LSTM with Optuna tuning

✔ Classical SARIMAX model

✔ Explainability using SHAP

✔ Window-size & horizon sensitivity

✔ Fully reproducible with config file

✔ Professional metrics & figures

This aligns with industry practices for demand forecasting and advanced analytics.


---

📌 10. Future Work

Add real meteorological data

Train GRU/CNN-LSTM hybrid models

Deploy as API (Flask/FastAPI)

Add attention mechanism for improved explainability

Multi-step direct forecasting approach


