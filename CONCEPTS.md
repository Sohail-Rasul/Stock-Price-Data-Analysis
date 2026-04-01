# Concepts - Quick Reference

A short reference for every indicator and metric used in this project.
For detailed explanations and maths, see the notebook comments.

---

## Returns Analysis

**Daily Return**
How much the stock moved each day as a percentage.
```
Daily Return = (Close_today - Close_yesterday) / Close_yesterday
```
- Green bar = up day, red bar = down day
- Tall bars = big move, something happened
- Clusters of tall bars = volatile period

**Cumulative Return**
Total return if you bought on day one and never sold.
```
Cumulative Return = (1 + Daily Return).cumprod() - 1
```
- Rising line = stock rewarded holders
- Dip then recovery = drawdown, check depth and recovery time

---

## Volatility

**Rolling Volatility (30-Day)**
Standard deviation of daily returns over a 30-day window.
```
Rolling Vol = Daily Return.rolling(30).std()
```
- High = stock was jumping around
- Low = smooth and calm
- Above the average line = more chaotic than usual

**Annualised Volatility**
Rolling volatility scaled to a yearly number for comparison.
```
Ann. Vol = Rolling Vol x sqrt(252)
```
- S&P 500 normally runs 15-20%
- Above 35% = high risk period

---

## Technical Indicators

**SMA - Simple Moving Average**
Average closing price over N days. Equal weight to all days.
```
SMA_20 = (P1 + P2 + ... + P20) / 20
```
- Price above SMA_200 = long-term uptrend
- SMA_20 crosses above SMA_50 = bullish signal (Golden Cross)
- SMA_20 crosses below SMA_50 = bearish signal (Death Cross)

**EMA - Exponential Moving Average**
Like SMA but weights recent prices more heavily.
```
k = 2 / (N + 1)
EMA_today = (Price_today x k) + (EMA_yesterday x (1 - k))
```
- Reacts faster than SMA to new price moves
- Used as the building block for MACD

**RSI - Relative Strength Index**
Ratio of average gains to average losses over 14 days, scaled 0-100.
```
RS  = Avg_Gain / Avg_Loss
RSI = 100 - (100 / (1 + RS))
```
- Above 70 = overbought, possible pullback
- Below 30 = oversold, possible bounce
- Crossing 50 upward = momentum turning bullish

**MACD - Moving Average Convergence Divergence**
Gap between a fast EMA (12) and slow EMA (26). Shows momentum.
```
MACD      = EMA_12 - EMA_26
Signal    = EMA_9 of MACD
Histogram = MACD - Signal
```
- MACD above Signal = bullish momentum
- Histogram shrinking = momentum fading, crossover coming
- MACD crossing zero = trend may be reversing

**Bollinger Bands**
SMA_20 with bands 2 standard deviations above and below.
```
Upper = SMA_20 + (2 x σ)
Lower = SMA_20 - (2 x σ)
```
- Price at upper band = unusually expensive
- Price at lower band = unusually cheap
- Bands squeezing = low volatility, big move coming

---

## Volume Analysis

**Average Volume**
Typical shares traded per day over 20 days. The baseline for normal.
```
Avg_Volume = Volume.rolling(20).mean()
```

**Volume Spike Ratio**
Today's volume divided by the 20-day average.
```
Spike = Volume_today / Avg_Volume
```
- Above 2.0 = notable spike, someone big acted
- Check if price was up or down to tell buying vs selling

**OBV - On Balance Volume**
Running total. Adds volume on up days, subtracts on down days.
```
Close up   - OBV = OBV + Volume
Close down - OBV = OBV - Volume
```
- OBV rising with price = uptrend confirmed
- OBV rising while price is flat = accumulation, breakout likely

---

## Multi-Stock Comparison

**Normalized Price Chart**
All stocks indexed to 100 on day one for fair comparison.
```
Normalized = (Price_today / Price_day1) x 100
```
- Above 100 = up from start date
- Line above SPY = outperforming the market

**Correlation Matrix**
How closely two stocks move together. Range -1 to +1.
```
Correlation(A,B) = Cov(A,B) / (σ_A x σ_B)
```
- Close to 1 = move together
- Close to 0 = move independently
- High correlation across all holdings = not truly diversified

**Beta**
How much the stock moves relative to the S&P 500.
```
Beta = Cov(Stock, Market) / Var(Market)
```
- Above 1 = more volatile than market
- Below 1 = less volatile than market
- Beta 1.3 = moves 30% more than the market in either direction

---

## Fundamental Metrics

**P/E - Price to Earnings**
How much you pay per $1 of company profit.
```
P/E = Stock Price / EPS
```
- Below 15 = cheap, above 25 = expensive
- Forward P/E < Trailing P/E = earnings expected to grow

**P/B - Price to Book**
Stock price vs what the company is worth on paper.
```
P/B = Stock Price / Book Value Per Share
```
- Below 1 = trading below asset value
- High P/B = market pricing in brand/future value

**EPS - Earnings Per Share**
Company profit divided by shares outstanding.
```
EPS = Net Income / Shares Outstanding
```
- Growing EPS = company becoming more profitable per share

**Dividend Yield**
Annual cash return as a percentage of stock price.
```
Yield = (Annual Dividend / Stock Price) x 100
```
- 0-1% = growth stock, 4%+ = income stock
- Very high yield can signal the stock price has crashed

**Revenue and Net Income Growth**
Is the business actually expanding year over year?
```
Growth = (This Year - Last Year) / Last Year x 100
```
- Both rising = healthy growth
- Revenue up, net income flat = margin pressure

---

## Backtesting

**What it is**
Testing a trading strategy on historical data to see if it would have made money.
Not a guarantee of future performance, but a disciplined way to evaluate a signal.

**Look-Ahead Bias**
The most common backtesting mistake. If you use today's crossover signal to trade
today, you're cheating — in reality you only see the close after the market shuts.
We fix this by shifting signals forward by 1 day.
```
Position_today = Signal_yesterday
```

**Strategy Return**
```
Strategy_Return = Daily_Return × Position
```
When Position = 1 (holding), you capture the market's return.
When Position = 0 (out), your return is 0.

**Sharpe Ratio**
Risk-adjusted return. How much return did you earn per unit of risk taken?
```
Sharpe = (Mean Daily Return / Std Daily Return) × sqrt(252)
```
* Above 1.0 = decent
* Above 2.0 = strong
* sqrt(252) scales from daily to annual (252 trading days per year)

**Max Drawdown**
The largest peak-to-trough loss during the period. The number that answers:
"At its worst, how much would I have lost?"
```
Drawdown = (Cumulative_Value - Rolling_Peak) / Rolling_Peak
Max Drawdown = min(Drawdown)
```

**Annualised Return**
Converts total return into a per-year figure so different time periods can be compared.
```
Annualised Return = (1 + Total Return) ^ (1 / n_years) - 1
```