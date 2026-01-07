---
columns:
- current_high (FLOAT64)
- current_low (FLOAT64)
- current_price (FLOAT64)
- current_volume (FLOAT64)
- date (DATE)
- exchange (STRING)
- high_1mo (FLOAT64)
- high_1yr (FLOAT64)
- high_3mo (FLOAT64)
- high_6mo (FLOAT64)
- high_9mo (FLOAT64)
- low_1mo (FLOAT64)
- low_1yr (FLOAT64)
- low_3mo (FLOAT64)
- low_6mo (FLOAT64)
- low_9mo (FLOAT64)
- pct_change_1mo (FLOAT64)
- pct_change_1yr (FLOAT64)
- pct_change_3mo (FLOAT64)
- pct_change_6mo (FLOAT64)
- pct_change_9mo (FLOAT64)
- std_diff_1mo (FLOAT64)
- std_diff_1yr (FLOAT64)
- std_diff_3mo (FLOAT64)
- std_diff_6mo (FLOAT64)
- std_diff_9mo (FLOAT64)
- symbol (STRING)
schema_hash: 000013a54dbaa630b1e53fb2064ec577bdd6dcaec2b7fbea1519c19737e95ce3

---
# Table Summary: global_markets_analysis_return

## Overall Dataset Characteristics

This table contains **45,797 rows** of time-series financial market data tracking daily performance metrics for international equity ETFs (Exchange-Traded Funds). The dataset spans **3,525 unique dates** and covers **13 different ETF symbols** traded on two exchanges (ARCX and XNAS).

**Data Quality Observations:**
- Core fields (date, exchange, symbol, current_price, current_volume) have 0% null values, indicating strong data integrity for essential metrics
- Historical comparison metrics show significant null percentages, particularly for percentage change fields (23-47% nulls), suggesting these calculations may not be available for all time periods
- High/low values for different timeframes (1mo, 3mo, 6mo, 9mo, 1yr) show consistent null patterns (~4-11%), likely due to insufficient historical data for recent entries
- Standard deviation fields (std_diff) are nearly complete with only 0.06% nulls

**Notable Patterns:**
- The data tracks multiple time horizons (1 month, 3 months, 6 months, 9 months, and 1 year) for comparative analysis
- ETFs represent various geographic markets (e.g., EWA=Australia, EWJ=Japan, EWG=Germany, EWY=South Korea, EEM=Emerging Markets)
- Volume data shows extreme ranges (15 to 322+ million), indicating varying liquidity across symbols and dates

## Column Details

### **date** (DATE)
- **Format:** Standard SQL date format (YYYY-MM-DD)
- **Null Pattern:** Complete (0% nulls)
- **Distribution:** 3,525 unique dates from 2012 to 2023
- **Use Case:** Primary time-series key for filtering and grouping

### **exchange** (STRING)
- **Values:** ARCX (NYSE Arca), XNAS (NASDAQ)
- **Null Pattern:** Complete (0% nulls)
- **Distribution:** Binary categorical field
- **Use Case:** Filter by trading venue; most ETFs trade on ARCX

### **symbol** (STRING)
- **Values:** 13 unique ETF ticker symbols (ACWI, EEM, EPI, EWA, EWG, EWJ, EWQ, EWU, EWW, EWY, FXI, EZA, and one more)
- **Null Pattern:** Complete (0% nulls)
- **Use Case:** Primary identifier for specific ETFs; key for filtering and grouping by geographic market

### **current_price** (FLOAT64)
- **Range:** $12.34 to $144.35
- **Null Pattern:** Complete (0% nulls)
- **Distribution:** 30,405 unique values indicating high precision
- **Use Case:** Core metric for analysis; baseline for return calculations

### **current_high** (FLOAT64)
- **Range:** $12.54 to $144.70
- **Null Pattern:** 10.98% nulls (likely for recent dates without intraday data)
- **Distribution:** 32,355 unique values
- **Use Case:** Intraday volatility analysis; day's trading range

### **current_low** (FLOAT64)
- **Range:** $12.05 to $143.81
- **Null Pattern:** 10.98% nulls (matches current_high)
- **Distribution:** 32,590 unique values
- **Use Case:** Intraday volatility analysis; paired with current_high

### **current_volume** (FLOAT64)
- **Range:** 15 to 322,620,100 shares
- **Null Pattern:** Complete (0% nulls)
- **Distribution:** 45,135 unique values (highly variable)
- **Use Case:** Liquidity indicator; filter for significant trading activity

### **high_1yr** (FLOAT64)
- **Range:** $14.84 to $144.70
- **Null Pattern:** 3.72% nulls (early dataset records)
- **Distribution:** 3,537 unique values
- **Use Case:** 52-week high benchmark; performance ceiling reference

### **low_1yr** (FLOAT64)
- **Range:** $12.05 to $104.29
- **Null Pattern:** 3.72% nulls (matches high_1yr)
- **Distribution:** 2,451 unique values
- **Use Case:** 52-week low benchmark; support level reference

### **pct_change_1yr** (FLOAT64)
- **Range:** -55.15% to +127.9%
- **Null Pattern:** 26.81% nulls (requires full year of historical data)
- **Distribution:** 8,157 unique values
- **Use Case:** Annual performance metric; year-over-year comparison

### **std_diff_1yr** (FLOAT64)
- **Range:** 0.0233 to 1.4709
- **Null Pattern:** Nearly complete (0.06% nulls)
- **Distribution:** 9,633 unique values
- **Use Case:** Volatility measure; standardized deviation from mean over 1 year

### **high_9mo** (FLOAT64)
- **Range:** $14.84 to $144.70
- **Null Pattern:** 5.59% nulls
- **Distribution:** 3,772 unique values
- **Use Case:** 9-month high benchmark; intermediate-term peak

### **low_9mo** (FLOAT64)
- **Range:** $12.05 to $108.55
- **Null Pattern:** 5.59% nulls (matches high_9mo)
- **Distribution:** 2,521 unique values
- **Use Case:** 9-month low benchmark; intermediate-term trough

### **pct_change_9mo** (FLOAT64)
- **Range:** -51.64% to +115.83%
- **Null Pattern:** 46.71% nulls (requires 9+ months of data)
- **Distribution:** 6,866 unique values
- **Use Case:** 9-month performance metric

### **std_diff_9mo** (FLOAT64)
- **Range:** 0.0233 to 1.5547
- **Null Pattern:** Nearly complete (0.06% nulls)
- **Distribution:** 9,893 unique values
- **Use Case:** 9-month volatility measure

### **high_6mo** (FLOAT64)
- **Range:** $14.84 to $144.70
- **Null Pattern:** 7.35% nulls
- **Distribution:** 4,514 unique values
- **Use Case:** 6-month high benchmark

### **low_6mo** (FLOAT64)
- **Range:** $12.05 to $127.77
- **Null Pattern:** 7.35% nulls (matches high_6mo)
- **Distribution:** 3,501 unique values
- **Use Case:** 6-month low benchmark

### **std_diff_6mo** (FLOAT64)
- **Range:** 0.0233 to 1.802
- **Null Pattern:** Nearly complete (0.06% nulls)
- **Distribution:** 10,051 unique values
- **Use Case:** 6-month volatility measure

### **pct_change_6mo** (FLOAT64)
- **Range:** -49.65% to +90.21%
- **Null Pattern:** 43.80% nulls
- **Distribution:** 6,043 unique values
- **Use Case:** 6-month performance metric

### **high_3mo** (FLOAT64)
- **Range:** $14.84 to $144.70
- **Null Pattern:** 9.14% nulls
- **Distribution:** 6,019 unique values
- **Use Case:** Quarterly high benchmark

### **low_3mo** (FLOAT64)
- **Range:** $12.05 to $135.23
- **Null Pattern:** 9.14% nulls (matches high_3mo)
- **Distribution:** 5,381 unique values
- **Use Case:** Quarterly low benchmark

### **std_diff_3mo** (FLOAT64)
- **Range:** 0.0233 to 2.3322
- **Null Pattern:** Nearly complete (0.06% nulls)
- **Distribution:** 10,288 unique values
- **Use Case:** Quarterly volatility measure

### **pct_change_3mo** (FLOAT64)
- **Range:** -55.29% to +64.8%
- **Null Pattern:** 23.21% nulls
- **Distribution:** 5,245 unique values
- **Use Case:** Quarterly performance metric

### **high_1mo** (FLOAT64)
- **Range:** $14.56 to $144.70
- **Null Pattern:** 10.33% nulls
- **Distribution:** 8,439 unique values
- **Use Case:** Monthly high benchmark

### **low_1mo** (FLOAT64)
- **Range:** $12.05 to $138.51
- **Null Pattern:** 10.33% nulls (matches high_1mo)
- **Distribution:** 7,739 unique values
- **Use Case:** Monthly low benchmark

### **std_diff_1mo** (FLOAT64)
- **Range:** 0.0233 to 3.573
- **Null Pattern:** Nearly complete (0.06% nulls)
- **Distribution:** 10,706 unique values
- **Use Case:** Monthly volatility measure

### **pct_change_1mo** (FLOAT64)
- **Range:** -49.15% to +41.88%
- **Null Pattern:** 42.18% nulls
- **Distribution:** 3,291 unique values
- **Use Case:** Monthly performance metric

## Query Considerations

### **Optimal Filtering Columns:**
- `symbol` - Filter by specific ETF or geographic market
- `exchange` - Filter by trading venue (though limited to 2 values)
- `date` - Time-based filtering (range queries, specific periods)
- `current_volume` - Filter for liquid trading days (e.g., > 1 million shares)

### **Good Grouping/Aggregation Columns:**
- `symbol` - Aggregate metrics by ETF
- `date` - Time-series aggregations (daily, monthly, yearly)
- `exchange` - Compare performance across venues
- Date extracts (YEAR, MONTH, QUARTER) - Temporal aggregations

### **Potential Join Keys:**
- `symbol` - Join with ETF metadata, holdings, expense ratios
- `date` - Join with market indices, economic indicators, events
- `exchange` - Join with exchange metadata or trading hours

### **Data Quality Considerations:**

1. **Handle Nulls Appropriately:**
   - Percentage change fields have 23-47% nulls - use COALESCE or filter WHERE IS NOT NULL
   - Intraday high/low have ~11% nulls - consider whether analysis requires complete intraday data
   - Historical metrics (1yr, 9mo, etc.) have increasing nulls for older timeframes

2. **Time Period Awareness:**
   - Early date records may lack sufficient lookback data for longer-term metrics
   - Percentage change calculations require complete historical periods
   - Consider date-based filtering to ensure data completeness

3. **Volatility Metric Usage:**
   - `std_diff_*` fields are nearly complete and more reliable than percentage changes
   - Standardized deviation increases with shorter timeframes (1mo > 3mo > 6mo > 9mo > 1yr)

4. **Volume Considerations:**
   - Extreme volume outliers exist - consider log transformations or percentile-based filtering
   - Very low volumes (< 1000) may indicate data quality issues or illiquid periods

5. **Price Consistency:**
   - Current price should fall within current_high and current_low when both are present
   - Use for data validation queries

## Keywords

International ETFs, Exchange-Traded Funds, Market Analysis, Time Series, Stock Prices, Trading Volume, Price Returns, Performance Metrics, Volatility Analysis, Standard Deviation, Geographic Markets, Emerging Markets, ARCX, XNAS, NYSE Arca, NASDAQ, 52-Week High, 52-Week Low, Intraday Prices, Historical Returns, Percentage Change, Price Range, Multi-Timeframe Analysis, Daily Trading Data, Financial Markets, Global Equities, Market Performance, Investment Returns, Risk Metrics

## Table and Column Documentation

**Table Comment:** Not provided

**Column Comments:** No column-level comments are present in the schema.