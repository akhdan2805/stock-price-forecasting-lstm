# 📈 Stock Price Forecasting using LSTM

## Objective

This project aims to develop and evaluate **LSTM-based time series models** for forecasting daily stock closing prices of **AAPL** and **AMD** using historical stock price data. A baseline LSTM and modified architectures were developed and compared based on **RMSE, MAE, and MAPE**.

## Table of Contents
- [Dataset Used](#dataset-used)
- [Methodology](#methodology)
- [Model Architecture](#model-architecture)
- [Results](#results)
- [Technologies](#technologies)

## Dataset Used

The [dataset](https://drive.google.com/drive/folders/1jNMQ5BJz_GAjjopaVB2mdefU_yW1Hst8?usp=sharing) contains historical daily stock price data for technology-sector companies, sourced from **Yahoo Finance**. The data includes Date, Open, High, Low, Close, Adj Close, and Volume.

For this project, **AAPL** and **AMD** were selected, with only the **Date** and **Close** columns used for stock price forecasting.

| Stock | Records | Period |
|---|---:|---|
| AAPL | 9,909 | Dec 1980 – Apr 2020 |
| AMD | 10,098 | Mar 1980 – Apr 2020 |

## Methodology

### 1. Data Loading & Inspection
- Load AAPL and AMD
- Select Date and Close
- Check data structure / missing values

### 2. Exploratory Data Analysis
- Historical closing price visualization
- Time-series characteristics

### 3. Train-Test Split
- Last 1 year → test set
- Remaining historical data → training set

### 4. Scaling & Windowing
- Min-Max Scaling
- Window size = 5
- Horizon = 1

### 5. Train-Validation Split
- 90% training
- 10% validation

### 6. Model Development
- Baseline LSTM
- Modified LSTM

### 7. Model Training
- Optimizer
- Loss function
- Training configuration
- EarlyStopping / ReduceLROnPlateau

### 8. Evaluation
- RMSE
- MAE
- MAPE

## Model Architecture

### Baseline LSTM
- LSTM 50 units
- ReLU
- Dense 1

### Modified LSTM
- AAPL architecture
- AMD architecture
- Architectural differences from baseline

## Results

### AAPL Results
[Baseline vs Modified]

### AMD Results
[Baseline vs Modified]

### Model Comparison
| Stock | Model | MAE | RMSE | MAPE |
|---|---|---:|---:|---:|
| AAPL | Baseline | ... | ... | ... |
| AAPL | Modified | ... | ... | ... |
| AMD | Baseline | ... | ... | ... |
| AMD | Modified | ... | ... | ... |

## Technologies

- **Language:** Python
- **Deep Learning:** TensorFlow / Keras
- **Data Processing:** Pandas, NumPy, Scikit-learn
- **Visualization:** Matplotlib
