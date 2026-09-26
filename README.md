# 📈 Stock Price Forecasting using LSTM

## Objective
This project aims to develop and evaluate **LSTM-based time series models** for forecasting daily stock closing prices of **AAPL** and **AMD** using historical stock price data. A baseline LSTM and modified architectures were developed and compared based on **MAE, RMSE, MAPE, and R²**.

## Table of Contents
- [Dataset Used](#dataset-used)
- [Methodology](#methodology)
- [Model Architecture](#model-architecture)
- [Results](#results)
- [Technologies](#technologies)

## Dataset Used

The [dataset](https://drive.google.com/drive/folders/1jNMQ5BJz_GAjjopaVB2mdefU_yW1Hst8?usp=sharing) contains historical daily stock price data for **AAPL** and **AMD**, sourced from [**Yahoo Finance**](https://finance.yahoo.com/quote/AAPL/history/?utm_source=chatgpt.com&frequency=1d&period1=345479400&period2=1790346095). The original data includes Date, Open, High, Low, Close, Adj Close, and Volume.

For this project, only the **Date** and **Close** columns were used for stock price forecasting.

| Stock | Records | Period |
|---|---:|---|
| AAPL | 9,909 | Dec 1980 – Apr 2020 |
| AMD | 10,098 | Mar 1980 – Apr 2020 |

## Methodology

### 1. Data Loading & Inspection
The **AAPL** and **AMD** datasets were loaded and inspected to understand their structure and data types. The **Date** column was converted to datetime format and set as the time-series index, while **Date** and **Close** were selected for the forecasting process.

### 2. Exploratory Data Analysis
The closing price trends of **AAPL** and **AMD** were visualized over time to examine their historical price movements and overall time-series patterns before model development.

### 3. Train-Test Split
The data was split chronologically, with the **last one year of observations reserved as the test set** and the remaining historical data used for training. This preserves the temporal order of the time-series data.

### 4. Scaling & Windowing
The training data was scaled using **Min-Max Scaling**, with the scaler fitted on the training set and then applied to the test set. The scaled time series was transformed into input-output sequences using a **window size of 5** and a **forecast horizon of 1**.

### 5. Train-Validation Split
The training sequences were divided into **90% training** and **10% validation** sets while maintaining the chronological order of the time-series data.

### 6. Model Development
Two LSTM-based approaches were developed and compared: a **baseline LSTM** and a **modified LSTM architecture**. The baseline model used a single LSTM layer with 50 units and ReLU activation, followed by a Dense output layer. The modified architectures introduced different configurations for AAPL and AMD to explore potential improvements in forecasting performance.

### 7. Model Training
The models were trained using the **Adam optimizer** with **Mean Squared Error (MSE)** as the loss function. The baseline model was trained for up to **20 epochs**, while the modified models used **EarlyStopping** and **ReduceLROnPlateau** to help manage training and retain the best-performing weights.

### 8. Evaluation
The baseline and modified models were evaluated on the unseen test set using **Mean Absolute Error (MAE)**, **Root Mean Squared Error (RMSE)**, **Mean Absolute Percentage Error (MAPE)**, and **R²** to measure forecasting performance.

## Model Architecture

### Baseline LSTM
The baseline model consists of a single **LSTM layer with 50 units and ReLU activation**, followed by a **Dense layer with 1 unit** for predicting the next closing price.

```text
LSTM (50 units, ReLU)
        ↓
Dense (1)
```

### Modified LSTM
Different modified architectures were developed for **AAPL** and **AMD**.

#### AAPL
The modified AAPL model uses a **Bidirectional LSTM with 100 units and tanh activation**, followed by a **32-unit Dense layer with ReLU activation**, **Dropout of 0.1**, and a final **Dense layer with 1 unit**.

```text
Bidirectional LSTM (100 units, tanh)
        ↓
Dense (32, ReLU)
        ↓
Dropout (0.1)
        ↓
Dense (1)
```

#### AMD
The modified AMD model uses a **Bidirectional LSTM with 50 units and ReLU activation**, followed by a **Dense layer with 1 unit**.

```text
Bidirectional LSTM (50 units, ReLU)
        ↓
Dense (1)
```

## Results
The baseline and modified LSTM models were evaluated on the unseen test set using **MAE, RMSE, MAPE, and R²**.

### AAPL Results
The modified LSTM architecture achieved lower error values and a higher R² compared to the baseline model.

| Model | MAE | RMSE | MAPE | R² |
|---|---:|---:|---:|---:|
| Baseline LSTM | 24.9192 | 33.2201 | 9.42% | 0.4089 |
| **Modified LSTM** | **5.3706** | **7.3424** | **2.19%** | **0.9711** |

### AMD Results
The modified LSTM architecture achieved slightly lower error values and a slightly higher R² compared to the baseline model.

| Model | MAE | RMSE | MAPE | R² |
|---|---:|---:|---:|---:|
| Baseline LSTM | 0.9865 | 1.4253 | 2.64% | 0.9705 |
| **Modified LSTM** | **0.9605** | **1.4046** | **2.55%** | **0.9713** |

### Model Comparison

| Stock | Model | MAE | RMSE | MAPE | R² |
|---|---|---:|---:|---:|---:|
| AAPL | Baseline LSTM | 24.9192 | 33.2201 | 9.42% | 0.4089 |
| AAPL | Modified LSTM | 5.3706 | 7.3424 | 2.19% | 0.9711 |
| AMD | Baseline LSTM | 0.9865 | 1.4253 | 2.64% | 0.9705 |
| AMD | Modified LSTM | 0.9605 | 1.4046 | 2.55% | 0.9713 |

### Overall Results
The modified LSTM architectures outperformed the baseline models on both **AAPL** and **AMD** based on lower **MAE, RMSE, and MAPE**, along with higher **R²** values. The improvement was particularly significant for AAPL, while AMD showed a smaller but consistent improvement across all evaluation metrics.

## Technologies
- **Language:** Python
- **Deep Learning:** TensorFlow / Keras
- **Data Processing:** Pandas, NumPy, Scikit-learn
- **Visualization:** Matplotlib
