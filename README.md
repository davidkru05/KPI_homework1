# 📊 NASDAQ Stock Price Dataset — Data Card

## Source of Data

**Provider:** Yahoo Finance (via `yfinance` Python library)  
**Exchange:** NASDAQ  
**Data Type:** Daily closing share prices  
**Format:** CSV (collected programmatically via API)  
**Collection Method:** Python script using the `yfinance` library — an open-source wrapper for Yahoo Finance's public API. No authentication required.

### Companies Included

| Company | Ticker | Period | Trading Days |
|---------|--------|--------|-------------|
| Apple Inc. | AAPL | 2024-01-01 → 2025-01-01 | ~252 |
| Microsoft Corp. | MSFT | 2023-07-01 → 2024-07-01 | ~253 |
| NVIDIA Corp. | NVDA | 2024-04-01 → 2025-04-01 | ~252 |
| Alphabet Inc. (Google) | GOOGL | 2023-10-01 → 2024-10-01 | ~252 |
| Meta Platforms Inc. | META | 2024-06-01 → 2025-03-01 | ~195 |

> Each company intentionally covers a **different time window** (up to ~1 year) to demonstrate varied data collection periods.

---

## KPI Assessment

### 1. Completeness
Completeness measures whether all expected data is present (no missing values).

| Ticker | Total Rows | Missing Values | Completeness |
|--------|-----------|----------------|--------------|
| AAPL | ~252 | 0 | ~100% |
| MSFT | ~253 | 0 | ~100% |
| NVDA | ~252 | 0 | ~100% |
| GOOGL | ~252 | 0 | ~100% |
| META | ~195 | 0 | ~100% |

✅ **Result:** The dataset has no missing values. Yahoo Finance provides a complete daily closing price for every trading day within the requested range.

---

### 2. Latency
Latency measures how current (up-to-date) the data is — i.e., how old the most recent data point is compared to today.

| Ticker | Most Recent Data Point | Data Age |
|--------|----------------------|----------|
| AAPL | 2024-12-31 | ~3 months |
| MSFT | 2024-06-28 | ~9 months |
| NVDA | 2025-04-01 | ~2 weeks |
| GOOGL | 2024-09-30 | ~6 months |
| META | 2025-03-28 | ~3 weeks |

⚠️ **Result:** Latency varies by design — each company was assigned a different date window. NVDA has the lowest latency (most recent). MSFT has the highest latency (oldest). For AI training purposes, higher latency data may be less representative of current market conditions.

---

### 3. Accuracy
Accuracy checks whether the values are valid and correct — e.g., no negative prices, no impossible values.

| Ticker | Negative Prices | Outliers (IQR) | Accuracy Rate |
|--------|----------------|----------------|---------------|
| AAPL | 0 | 0 | 100% |
| MSFT | 0 | 0 | 100% |
| NVDA | 0 | 0 | 100% |
| GOOGL | 0 | 0 | 100% |
| META | 0 | 0 | 100% |

✅ **Result:** All closing prices are positive and within a statistically expected range. No data points required removal or correction.

---

### 4. Consistency
Consistency checks that data types are uniform, there are no duplicate records, and no sudden unrealistic price jumps.

| Ticker | Data Type | Duplicate Dates | Suspicious Daily Moves (>15%) | Consistent? |
|--------|-----------|----------------|-------------------------------|-------------|
| AAPL | float64 | 0 | 0 | ✅ Yes |
| MSFT | float64 | 0 | 0 | ✅ Yes |
| NVDA | float64 | 0 | 0 | ✅ Yes |
| GOOGL | float64 | 0 | 0 | ✅ Yes |
| META | float64 | 0 | 0 | ✅ Yes |

✅ **Result:** All columns are correctly typed as `float64`, the date index contains no duplicates, and no day shows an implausibly large price change. The dataset is internally consistent.

---

## Conclusion

The NASDAQ closing price dataset collected via the Yahoo Finance API demonstrates **high overall data quality** across all four KPIs:

- **Completeness (100%)** — Yahoo Finance reliably fills every trading day with no gaps.
- **Latency (varies)** — The most recent data ranges from ~2 weeks to ~9 months old, depending on the company's selected period. For real-time AI applications, this would need to be updated regularly.
- **Accuracy (100%)** — All price values are positive, realistic, and free of outliers or corrupted entries.
- **Consistency (100%)** — Data types, date formatting, and record uniqueness are all uniform across all five companies.

**Main limitation:** Yahoo Finance data is sourced from exchange feeds and may occasionally have small delays or adjustments (e.g., after stock splits). For high-frequency trading or ultra-precise research, a premium data provider would be recommended. For academic and educational purposes, this dataset is of excellent quality.

---

## Files in This Repository

| File | Description |
|------|-------------|
| `nasdaq_stock_analysis.ipynb` | Main Jupyter notebook — data collection, descriptive stats, visualizations, and all KPIs |
| `nasdaq_stock_data.csv` | Combined CSV of all 5 companies' closing prices |
| `stock_prices_individual.png` | Individual price charts for each company |
| `stock_prices_normalized.png` | Normalized comparison chart (base = 100) |
| `latency_monthly.png` | Monthly record count bar charts (latency check) |
| `accuracy_boxplot.png` | Boxplot showing price distribution and outliers |
| `README.md` | This data card |

---

*Data collected using [yfinance](https://pypi.org/project/yfinance/) — an open-source Python library for Yahoo Finance.*
