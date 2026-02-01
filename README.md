# 📈 Market Mood & Moves: Sentiment-Driven Stock Prediction



> **A Multimodal Trading Engine fusing Technical Analysis (LSTM) with Fundamental Sentiment (FinBERT).**

---

## 📖 Table of Contents
- [About the Project](#-about-the-project)
- [How It Works](#-how-it-works)
- [Key Features](#-key-features)
- [Installation](#-installation)
- [Usage](#-usage)
- [Results & Case Studies](#-results--case-studies)
- [Project Structure](#-project-structure)
- [Mentors & Contributors](#-mentors--contributors)

---

## 🧐 About the Project
**Market Mood & Moves** is a research-based algorithmic trading system developed during **WIDS (Winter in Data Science)**. 

Traditional quantitative models (ARIMA, RNNs) often fail during high-volatility events because they ignore the "why" behind price movements. This project solves that by creating a **Dual-Engine System**:
1.  **The "Eyes" (NLP):** Reads financial news using **FinBERT** to understand market sentiment.
2.  **The "Brain" (Time-Series):** Analyzes price trends using an **LSTM** network.

A trade signal is only generated when **both engines agree** (Convergence), effectively filtering out false breakouts and "dead cat bounces."

---

## ⚙️ How It Works

The system operates on a **Multimodal Fusion** logic:

1.  **Data Acquisition:** Fetches real-time OHLCV data via `yfinance` and live news headlines.
2.  **Sentiment Engine:** Uses `ProsusAI/finbert` to score news from **-1 (Bearish)** to **+1 (Bullish)**.
3.  **Forecasting Engine:** Uses a stacked **LSTM** trained on a 60-day sliding window of price, volatility, and returns.
4.  **Decision Matrix:**
    * **BUY:** Technical Upside > 0.5% **AND** Sentiment > 0.15
    * **SELL:** Technical Downside < -0.5% **AND** Sentiment < -0.15
    * **HOLD:** Any divergence between Price and News.

---

## 🚀 Key Features
* **Domain-Adapted NLP:** Uses FinBERT (trained on TRC2-Financial corpus) instead of generic BERT.
* **Robust Time-Series:** LSTM architecture with Dropout to prevent overfitting on noise.
* **Risk Management:** Defaults to "HOLD" when signals diverge (e.g., Price goes up, but News is negative).
* **Live Inference:** Can predict the next trading session's move for any ticker (AAPL, NVDA, TSLA, etc.).
* **Visualization:** Generates forecast plots with clear buy/sell indicators.

---

## 💻 Installation

1.  **Clone the Repo**
    ```bash
    git clone [https://github.com/yourusername/market-mood-moves.git](https://github.com/yourusername/market-mood-moves.git)
    cd market-mood-moves
    ```

2.  **Install Dependencies**
    ```bash
    pip install torch torchvision torchaudio
    pip install transformers pandas numpy scikit-learn matplotlib yfinance
    ```

    *Note: If you have a GPU, ensure you install the CUDA version of PyTorch.*

---

## 🛠 Usage

You can run the main pipeline script to analyze a specific stock.

```python
# Open the main notebook or python script
python main.py
