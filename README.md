# 📊 Portfolio Risk & VaR Dashboard — Indian Equity Markets

> A quantitative risk analysis tool for Indian blue-chip stocks, implementing **Value-at-Risk (VaR)**, **Expected Shortfall (CVaR)**, and **portfolio risk metrics** aligned with industry treasury risk management practices.

---

## 🧭 Overview

This project builds an end-to-end **Portfolio Risk Dashboard** for a basket of Indian NSE-listed equities. It was inspired by work done under the **EY CAFTA Treasury360 framework**, where VaR modelling and liquidity risk management are core tools used by corporate treasury teams.

The model downloads live historical price data, computes risk metrics using two industry-standard methods, and generates a multi-panel visual dashboard — fully automated in Python.

**Portfolio:** Bajaj Auto · GCPL · Reliance Industries · TCS  
**Data Source:** Yahoo Finance (NSE tickers)  
**Period Analyzed:** January 2022 – December 2024

---

## 📐 Methodology

### 1. Daily Log Returns
Log returns are used instead of simple percentage returns for their superior statistical properties — they are time-additive and more suitable for risk modelling.

```
r_t = ln(P_t / P_{t-1})
```

### 2. Portfolio Return
Weighted sum of individual stock returns, where equal weights (25% each) are assigned by default.

### 3. Value-at-Risk (VaR)

Two methods are implemented and compared:

| Method | Description |
|--------|-------------|
| **Historical Simulation** | Sorts actual historical returns; finds loss at the Xth percentile. No distribution assumptions — uses real data. |
| **Parametric (Normal)** | Assumes returns follow a normal distribution. Uses Z-score × standard deviation to estimate loss threshold. |

Both are computed at **95%** and **99%** confidence levels.

**Interpretation:** A 99% VaR of ₹25,000 means: *"On 99 out of 100 days, portfolio loss will not exceed ₹25,000."*

### 4. Expected Shortfall (CVaR)
Average loss on days where the loss *exceeds* the VaR threshold. CVaR better captures **tail risk** and is preferred by Basel III banking regulation.

```
CVaR = E[Loss | Loss > VaR]
```

### 5. Sharpe Ratio
Risk-adjusted return metric — how much excess return is earned per unit of risk:

```
Sharpe = (Annual Return − Risk-Free Rate) / Annual Volatility
```
Risk-free rate used: **6.8%** (RBI repo rate benchmark)

### 6. Maximum Drawdown
Largest peak-to-trough decline in cumulative portfolio value over the analysis period.

---

## 📈 Dashboard Output

The script generates a **7-panel PNG dashboard** (`var_dashboard.png`) containing:

| Panel | Description |
|-------|-------------|
| 1 | Cumulative portfolio return over time |
| 2 | Key risk metrics summary table |
| 3 | Daily return distribution with VaR thresholds overlaid |
| 4 | Individual stock performance comparison |
| 5 | Return correlation heatmap across all 4 stocks |
| 6 | VaR method comparison bar chart (Historical vs Parametric) |
| 7 | Rolling 30-day annualised volatility |

---

## 🚀 How to Run

### Step 1 — Clone this repository
```bash
git clone https://github.com/YOUR_USERNAME/portfolio-var-dashboard.git
cd portfolio-var-dashboard
```

### Step 2 — Install dependencies
```bash
pip install -r requirements.txt
```

### Step 3 — Run the script
```bash
python var_dashboard.py
```

The dashboard image will be saved as `var_dashboard.png` in the same folder.

---

## ⚙️ Customise the Model

Open `var_dashboard.py` and edit the **Configuration** section at the top:

```python
# Change the stocks
TICKERS = {
    'Bajaj Auto': 'BAJAJ-AUTO.NS',
    'GCPL':       'GODREJCP.NS',
    'Reliance':   'RELIANCE.NS',
    'TCS':        'TCS.NS'
}

# Change portfolio weights (must sum to 1.0)
WEIGHTS = np.array([0.25, 0.25, 0.25, 0.25])

# Change portfolio size
PORTFOLIO_VALUE = 1_000_000   # ₹10 Lakhs

# Change date range
START_DATE = '2022-01-01'
END_DATE   = '2024-12-31'
```

> **Tip:** To add a US stock, use its standard ticker (e.g., `'AAPL'`). For BSE-listed stocks, use the `.BO` suffix instead of `.NS`.

---

## 📦 Dependencies

| Library | Purpose |
|---------|---------|
| `yfinance` | Download NSE stock price data |
| `pandas` | Data manipulation and time series handling |
| `numpy` | Numerical calculations (returns, VaR, Sharpe) |
| `matplotlib` | Plotting and dashboard visualisation |
| `scipy` | Normal distribution fitting and Z-scores |

---

## 🔗 Context & Motivation

This project was built as part of an MBA in **Strategic Financial Management** (UPES × EY), drawing on:
- **EY CAFTA Treasury360** programme — VaR modelling and liquidity risk frameworks
- **Financial Resilience Assessment** project on Bajaj Auto (Ind AS 115/37, commodity hedging, FX risk)
- **Regression Analysis** coursework (CFI Certification — R², RMSE, volatility)

The model reflects the kind of quantitative risk analysis performed by corporate treasury teams and risk management functions at financial institutions.

---

## 👤 Author

**Ria Agrawal**  
MBA, Strategic Financial Management — UPES School of Business × EY  
📧 riaagrawal.ra4523@gmail.com  
🔗 [LinkedIn](https://linkedin.com/in/ria-agrawal-1546a5230)

---

## 📄 License

MIT License — free to use, adapt, and share with attribution.
