---
columns:
- asset_type (STRING)
- avg_daily_price_change (FLOAT64)
- avg_daily_return_pct (FLOAT64)
- best_day_change (FLOAT64)
- exchange (STRING)
- name (STRING)
- negative_days (INT64)
- neutral_days (INT64)
- period_end_date (DATE)
- period_end_price (FLOAT64)
- period_start_date (DATE)
- period_start_price (FLOAT64)
- positive_days (INT64)
- symbol (STRING)
- time_period (STRING)
- total_price_change (FLOAT64)
- total_return_pct (FLOAT64)
- trading_days (INT64)
- volatility_pct (FLOAT64)
- win_rate_pct (FLOAT64)
- worst_day_change (FLOAT64)
schema_hash: 2ac666c6ed8d128ac602e9d3c2a171bf3c10f062c25ee8960d7856019efb2f1f

---
# Table Summary: major_indicies_summary

## Overall Dataset Characteristics

This table contains **24 rows** of summarized financial performance data for major market indices and ETFs across different time periods. The dataset tracks performance metrics like returns, volatility, and price changes over various timeframes (12 weeks, 6 months, 1 year, and 5 years).

**Key Observations:**
- Data covers 5 different symbols: DIA, IWM, QQQ, SPY, and VIX.INDX
- 4 distinct time periods analyzed per symbol (creating 24 total rows)
- Significant null values (33.33%) in certain columns, particularly for VIX.INDX entries (which lack price/return data as it's a volatility index)
- Date ranges span from December 2020 to December 2025, with analysis periods ending between December 2024 and December 2025
- Generally high data quality for trading day counts and date fields (0% nulls)

## Column Details

### **Identifier Columns**

**time_period** (STRING)
- No nulls; 4 unique values
- Categorical time buckets: `12_weeks`, `6_months`, `1_year`, `5_years`
- Used to segment analysis periods
- Essential for filtering and grouping by time horizon

**symbol** (STRING)
- No nulls; 5 unique values
- Major market symbols: DIA (Dow Jones), IWM (Russell 2000), QQQ (Nasdaq 100), SPY (S&P 500), VIX.INDX (Volatility Index)
- Primary identifier for securities
- Key column for filtering and joining

**asset_type** (STRING)
- 33.33% nulls (8 out of 24 rows)
- Only value present: `ETF`
- Nulls correspond to VIX.INDX entries (which is an index, not an ETF)
- Limited utility for filtering; mostly descriptive

**exchange** (STRING)
- No nulls; 3 unique values
- Values: ARCX (NYSE Arca), INDX (Index), XNAS (Nasdaq)
- VIX.INDX uses INDX exchange designation
- Useful for exchange-based grouping

**name** (STRING)
- 33.33% nulls (matching asset_type pattern)
- Contains full names: "SPDR S&P 500 ETF Trust", "Invesco QQQ Trust Series 1", etc.
- Nulls for VIX.INDX entries
- Primarily for display/reporting purposes

### **Date Columns**

**period_end_date** (DATE)
- No nulls; 6 unique dates
- Range: 2024-12-16 to 2025-12-16
- Marks the end of each analysis period
- Critical for temporal filtering and trending

**period_start_date** (DATE)
- No nulls; 6 unique dates
- Range: 2020-12-18 to 2025-10-15
- Marks the beginning of each analysis period
- The 5-year periods start in December 2020

### **Trading Activity Columns**

**trading_days** (INT64)
- No nulls; 10 unique values
- Range: 1 to 1,013 days
- Represents actual trading days in the period
- 5-year periods show ~1,000+ days, 1-year ~250 days, 6-months ~125 days, 12-weeks ~60 days
- Essential for calculating daily averages

**neutral_days** (INT64)
- No nulls; 3 unique values (0, 1, 2)
- Days with minimal price movement
- Rare occurrences; most periods have 0-2 neutral days

**positive_days** (INT64)
- No nulls; 16 unique values
- Range: 0 to 548 days
- Days with positive price movement
- Higher counts in longer time periods

**negative_days** (INT64)
- No nulls; 16 unique values
- Range: 0 to 456 days
- Days with negative price movement
- Complements positive_days; sum with neutral_days equals trading_days

### **Performance Metrics**

**total_return_pct** (FLOAT64)
- 33.33% nulls (VIX.INDX entries)
- Range: -10.2% to +15.91%
- Total percentage return over the period
- Negative returns indicate losses; positive indicate gains
- Critical for performance comparison

**volatility_pct** (FLOAT64)
- 33.33% nulls (VIX.INDX entries)
- Range: 7.28% to 26.75%
- Annualized volatility measure
- Higher values indicate greater price fluctuation
- Important for risk assessment

**avg_daily_return_pct** (FLOAT64)
- 16.67% nulls (4 rows)
- Range: -0.6877% to +0.0963%
- Average daily percentage return
- Smaller values typical for short periods
- Useful for comparing normalized daily performance

**win_rate_pct** (FLOAT64)
- No nulls; 17 unique values
- Range: 0.0% to 100.0%
- Percentage of trading days that were positive
- Values around 50-56% typical for most periods
- 0% and 100% values likely from 1-day periods

### **Price Change Metrics**

**total_price_change** (FLOAT64)
- 16.67% nulls
- Range: -$37.78 to +$104.96
- Absolute dollar change from start to end
- Reflects actual price movement regardless of percentage

**best_day_change** (FLOAT64)
- 16.67% nulls
- Range: -$1.60 to +$55.18
- Largest single-day gain
- Higher values in higher-priced securities (e.g., QQQ, SPY)

**worst_day_change** (FLOAT64)
- 16.67% nulls
- Range: -$25.95 to +$0.10
- Largest single-day loss (negative values)
- Important for understanding downside risk

**avg_daily_price_change** (FLOAT64)
- 16.67% nulls
- Range: -$1.60 to +$0.3518
- Mean daily price movement
- Can be negative or positive depending on overall trend

**period_start_price** (FLOAT64)
- 33.33% nulls (VIX.INDX entries)
- Range: $208.44 to $657.94
- Opening price at period start
- Essential for calculating returns and changes

**period_end_price** (FLOAT64)
- 33.33% nulls (VIX.INDX entries)
- Range: $208.55 to $678.87
- Closing price at period end
- Used with start_price to validate total returns

## Potential Query Considerations

### **Good Filtering Columns:**
- `symbol`: Filter for specific indices/ETFs (e.g., "Show me SPY performance")
- `time_period`: Filter by time horizon (e.g., "5_years" for long-term analysis)
- `period_end_date`: Filter by recency (e.g., most recent periods)
- `exchange`: Filter by trading venue

### **Good Grouping/Aggregation Columns:**
- `symbol`: Group to compare across different indices
- `time_period`: Group to compare short vs long-term performance
- `exchange`: Group by trading venue

### **Potential Join Keys:**
- `symbol`: Can join to other tables with security/ticker information
- Combination of `symbol` + `period_end_date`: Unique identifier for each summary record

### **Data Quality Considerations:**

1. **Null Pattern for VIX.INDX**: 33.33% nulls in price-related columns are systematic - VIX is a volatility index without tradeable prices. Queries calculating returns should exclude VIX or handle nulls appropriately.

2. **Consistent 16.67% Nulls**: Four rows have nulls in daily metrics (avg_daily_return_pct, total_price_change, best/worst_day_change, avg_daily_price_change). These likely represent single-day periods or data quality issues.

3. **Derived Calculations**: Several metrics are derived from others:
   - `total_return_pct` ≈ (period_end_price - period_start_price) / period_start_price × 100
   - `trading_days` = positive_days + negative_days + neutral_days
   - Queries should validate these relationships

4. **Time Period Alignment**: Not all symbols have data for all time periods - verify data completeness when doing cross-symbol comparisons.

5. **Date Range Logic**: Use both start and end dates together to properly identify periods, as single dates may overlap across different time_period categories.

## Keywords

Market indices, ETF performance, stock market summary, trading statistics, volatility analysis, returns analysis, SPY, QQQ, DIA, IWM, VIX, financial metrics, price changes, win rate, trading days, bull/bear markets, market performance, investment analysis, portfolio analysis, time series analysis, economic indicators, market trends, risk metrics, daily returns, annualized returns

## Table and Column Documentation

**Table Comment:** Not provided

**Column Comments:** Not provided