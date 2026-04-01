# Stock Analysis Framework

A comprehensive stock analysis system built in Python and Jupyter Notebook.
Analyses a stock from the ground up: raw price data, technical indicators,
volume analysis, multi-stock comparison, and fundamental metrics, finishing
with an automated scorecard that aggregates all signals into a single verdict.

Built using AAPL as the working ticker throughout.

---

## Tech Stack

- Python, Jupyter Notebook
- `yfinance` - market data
- `pandas`, `numpy` - data manipulation
- `matplotlib` - visualisation

---

## Project Structure
```
notebook/
├── Section 1  - Company Overview
├── Section 2  - Price Data (OHLCV)
├── Section 3  - Returns Analysis
├── Section 4  - Volatility
├── Section 5  - Technical Indicators
├── Section 6  - Volume Analysis
├── Section 7  - Multi-Stock Comparison
├── Section 8  - Fundamental Metrics
└── Section 9  - Summary Scorecard
```

---

## What This Project Covers

| Section | What it answers |
|---|---|
| Returns | How much did the stock make? When were the wild days? |
| Volatility | How risky was it to hold? How does that compare to the market? |
| Technical Indicators | What is the trend, momentum, and volatility signal? |
| Volume | Are price moves backed by real conviction? |
| Comparison | How did it perform vs peers and the S&P 500? |
| Fundamentals | Is the business behind the stock actually healthy? |
| Scorecard | What does everything say together? |

---

## Sample Output
```
----------------------------------------------------
  AAPL (Apple Inc.) - Analysis Scorecard
----------------------------------------------------
  Current Price     : $250.83
----------------------------------------------------
  TREND
    Direction       : Bullish
    Price vs SMA200 : Above  ($211.52)
    SMA20 vs SMA50  : SMA20 above - bullish
----------------------------------------------------
  MOMENTUM
    Strength        : Mixed
    RSI (14)        : 58.4  ->  Bullish territory
    MACD            : Below signal - bearish
    Bollinger Band  : Above midline - mild bullish
----------------------------------------------------
  VOLATILITY
    Ann. Volatility : 27.1%  ->  Moderate
    Beta vs Market  : 1.21   ->  High
----------------------------------------------------
  VOLUME
    OBV Signal      : Confirming uptrend
----------------------------------------------------
  VALUATION
    Trailing P/E    : 32.2
    Forward P/E     : 27.2
    Assessment      : Expensive
----------------------------------------------------
  FUNDAMENTALS
    Health          : Strong
    Detail          : Revenue +6.4%  |  Net Income +19.5%
----------------------------------------------------
  OVERALL VERDICT   : Bullish - multiple indicators aligned
----------------------------------------------------
```

---

## How to Run
```bash
pip install yfinance pandas numpy matplotlib
```

Open `stock_analysis.ipynb` in Jupyter and run cells top to bottom.
To analyse a different stock, change the ticker symbol in Cell 2.

---

## A Note on Process

Code in this project was developed with AI assistance.
The concepts, analysis framework, and explanations are my own,
built by working through each indicator, understanding the maths
behind it, and learning how to read and interpret the outputs.

I also have working experience with pandas, numpy, and matplotlib
from prior data analysis projects.

For a full breakdown of every concept, indicator, and the maths
behind them, see [CONCEPTS.md](./CONCEPTS.md).

---

## Author
Mohammed Sohail Rasul