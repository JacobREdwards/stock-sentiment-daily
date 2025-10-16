# 📈 Stock Sentiment Daily Prediction Model

🚀 **Live Demo:** [Hugging Face Space](https://jacobre20-stock-sentiment-service.hf.space)  
🧠 **Model Hub:** [jacobre20/stock-sentiment-daily-v1](https://huggingface.co/spaces/jacobre20/stock-sentiment-service/tree/main)  
📘 **Notebook:** [Open in Google Colab](https://colab.research.google.com/github/JacobREdwards/stock-sentiment-daily/blob/main/Stock_Sentiment_Model.ipynb)

---

## 🎯 Project Overview

This project builds and deploys a **machine learning model** that predicts whether a stock’s price will rise or fall on the **next trading day**, based on historical technical indicators (2015–present).

The model is trained in **Python (scikit-learn)** and deployed to **Hugging Face Spaces** with a public **REST API** for live testing.

---

## ⚙️ Model Summary

| Component | Description |
|------------|-------------|
| **Algorithm** | Logistic Regression |
| **Goal** | Binary classification — 1 = stock goes **up**, 0 = stock goes **down** |
| **Data Source** | Yahoo Finance (`yfinance`, 2015 → present) |
| **Performance** | ~52–55% accuracy on test data (normal for daily direction models) |

### 📊 Input Features

| Feature | Description |
|----------|-------------|
| `ret_1d` | 1-day return |
| `ret_5d` | 5-day return |
| `vol_5d`, `vol_20d` | 5-day & 20-day volatility |
| `rsi14` | 14-day Relative Strength Index |
| `macd`, `macd_signal`, `macd_hist` | MACD indicators |
| `bb_pct` | Bollinger Band % position |
| `sma_ratio` | 10-day / 20-day SMA ratio |
| `spy_ret_1d` | S&P 500 1-day return (market context) |

### 📈 Output Fields

| Field | Meaning |
|--------|----------|
| `prob_up` | Probability stock will rise next day (0–1) |
| `pred_up` | Final binary prediction (1 = up, 0 = down) |

---

## ☁️ Hugging Face Deployment

**Model Hub ID:**  
[`jacobre20/stock-sentiment-daily-v1`](https://huggingface.co/spaces/jacobre20/stock-sentiment-service/tree/main)

**Live Space (API + UI):**  
👉 [Stock Sentiment Service on Hugging Face Spaces](https://jacobre20-stock-sentiment-service.hf.space)

---

## 🔗 API Endpoint

**POST** request to:  
`https://jacobre20-stock-sentiment-service.hf.space/predict`

### Example Request
```json
{
  "rows": [
    {
      "symbol": "AAPL",
      "date": "2025-10-10",
      "features": {
        "ret_1d": -0.0008,
        "ret_5d": 0.0073,
        "vol_5d": 0.0045,
        "vol_20d": 0.0159,
        "rsi14": 67.78,
        "macd": 6.9671,
        "macd_signal": 7.0192,
        "macd_hist": -0.052,
        "bb_pct": 0.71,
        "sma_ratio": 1.0321,
        "spy_ret_1d": -0.0037
      }
    }
  ]
}
