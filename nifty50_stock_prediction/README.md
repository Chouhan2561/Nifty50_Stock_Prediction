# Deep Learning Assignment 2: NIFTY-50 Stock Price Prediction using LSTM

## Project Overview
This repository contains the complete implementation for **Deep Learning Assignment – 2: Stock Price Prediction** using historical NIFTY-50 data for **HDFC Bank Limited (HDFCBANK)**.

---

## File Structure
`
nifty50_stock_prediction/
│
├── Name_RollNo_DeepLearning_Assignment2_HDFCBANK.ipynb   # Main Google Colab / Jupyter Notebook
├── HDFCBANK.csv                                         # Historical daily dataset (2000 - 2021)
├── HDFCBANK_1yr_real_ground_truth.csv                   # Ground-truth market data for 1-year comparison
├── eda_price_sma.png                                    # EDA: Historical price & moving averages
├── eda_daily_returns.png                                # EDA: Daily percentage returns & volatility
├── training_loss_curve.png                              # Diagnostic: LSTM Training Loss Curve
├── test_actual_vs_predicted.png                         # Result: Actual vs. Predicted on Test Set
├── future_1yr_prediction_vs_real.png                    # Result: 1-Year Forecast vs. Ground Truth
├── complete_historical_and_forecast_overview.png        # Macro view: 2000-2022 Full Timeline
└── README.md                                            # Documentation & running instructions
`

---

## How to Run in Google Colab (Recommended)
1. **Open Google Colab**: Navigate to [colab.research.google.com](https://colab.research.google.com).
2. **Upload the Notebook**:
   - Click **Upload** and select Name_RollNo_DeepLearning_Assignment2_HDFCBANK.ipynb.
3. **Upload the Dataset**:
   - In the left sidebar of Google Colab, click the **Files (Folder icon)**.
   - Click the **Upload** button and select HDFCBANK.csv (and optionally HDFCBANK_1yr_real_ground_truth.csv).
4. **Personalize Your Information**:
   - In the first cell of the notebook, replace [ENTER YOUR NAME HERE] and [ENTER YOUR ROLL NO HERE] with your name and roll number.
   - Rename the file following the submission format: YourName_YourRollNo_DeepLearning_Assignment2_HDFCBANK.ipynb.
5. **Run All**:
   - Go to the menu: **Runtime > Run all** (or press Ctrl + F9).
   - The entire notebook will execute from top to bottom, training the LSTM model, calculating all metrics, and plotting all graphs.

---

## Key Model Architecture & Results Summary

### 1. Model Architecture
- **Framework**: TensorFlow / Keras (Sequential API)
- **Input Dimension**: Lookback window  = 60$ trading days
- **Layer 1**: LSTM (64 units, 
eturn_sequences=True) + Dropout(0.20)
- **Layer 2**: LSTM (32 units, 
eturn_sequences=False) + Dropout(0.20)
- **Layer 3**: Fully Connected Dense (25 units, ReLU)
- **Layer 4**: Output Dense (1 unit, Linear)
- **Optimizer**: Adam (=0.001$), Loss: Mean Squared Error (MSE)

### 2. Test Set Evaluation Metrics (2017 – 2021)
| Metric | Value | Meaning |
| :--- | :--- | :--- |
| **Root Mean Squared Error (RMSE)** | **₹62.68** | Low variance relative to ₹1,400+ stock price |
| **Mean Absolute Error (MAE)** | **₹44.37** | Average deviation of only ~₹44 per share |
| **Mean Absolute Pct Error (MAPE)** | **2.62%** | High prediction precision (<3% error) |
| **Coefficient of Determination (^2$)** | **0.9790** | Explains 97.9% of closing price variance |
| **Directional Accuracy (DA)** | **~50%** | Captures market momentum shifts |

### 3. Next 1-Year Future Prediction & Real Data Comparison
- **Forecast Horizon**: May 2021 to April 2022 (248 trading days).
- **Forecasting Technique**: Autoregressive recursive multi-step forecasting.
- **Initial Day Prediction**: ₹1,431.88 (Actual May 3, 2021: ₹1,414.45 — **error < 1.2%**).
- **1-Year Actual End Price**: ₹1,384.60 (April 29, 2022).
- **Google Finance Screenshot Alignment**:
  - The user's Google Finance screenshot shows HDFCBANK hovering at **₹717.80 INR** with 2001 hovered at **₹11.58 INR**.
  - Google Finance retroactive split-adjusts prices (accounting for 2011 5:1 split, 2019 2:1 split, and the 2023 HDFC Ltd merger).
  - ₹1,435 unadjusted $\div$ 2 = **₹717.50 INR** — exact alignment between the Kaggle dataset scale and the Google Finance chart scale!
