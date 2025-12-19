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
# Currency Summary Table Documentation

## Overall Dataset Characteristics

**Total Rows:** 41

**General Description:** This table contains historical performance metrics for currency-related financial instruments (primarily ETFs and some stocks) across different time periods. The dataset tracks various trading performance indicators including returns, volatility, and price movements.

**Data Quality Observations:**
- Approximately 19.51% of rows have NULL values in several columns (asset_type, name, total_return_pct, volatility_pct, period_start_price, period_end_price)
- These NULL values appear consistently across the same rows, suggesting incomplete data for certain records
- All core identifier columns (exchange, symbol, time_period) have 100% completeness
- Date ranges span from December 2020 to December 2025, indicating both historical and potentially projected data

**Notable Patterns:**
- Data is organized by currency trading instruments with multiple time period analyses per symbol
- Time periods analyzed include: 12_weeks, 6_months, 1_year, and 5_years
- Trading instruments primarily represent currency ETFs (Australian Dollar, British Pound, Canadian Dollar, Euro, Japanese Yen, Emerging Markets) plus cryptocurrency exposure (Bitcoin)
- Single-day records (trading_days = 1) have NULL volatility values, which makes sense as volatility requires multiple data points

---

## Column Details

### **exchange** (STRING)
- **Description:** Trading exchange where the instrument is listed
- **Values:** ARCX (NYSE Arca), INDX (Index), OTCM (OTC Markets)
- **Null Pattern:** 0% - fully populated
- **Usage:** Good for filtering by exchange, particularly to distinguish between exchange-traded and OTC instruments

### **asset_type** (STRING)
- **Description:** Classification of the financial instrument
- **Values:** ETF, Stock, or NULL
- **Null Pattern:** 19.51% - appears to be missing for certain records (possibly INDX-listed items)
- **Usage:** Filter by instrument type; note NULL handling needed in queries

### **time_period** (STRING)
- **Description:** The analytical time window for performance metrics
- **Values:** "12_weeks", "6_months", "1_year", "5_years"
- **Null Pattern:** 0% - fully populated
- **Usage:** Essential grouping dimension for period-based analysis; enables trend analysis across different timeframes

### **symbol** (STRING)
- **Description:** Ticker symbol of the trading instrument
- **Values:** FXA, FXB, FXC, FXE, FXY (Invesco Currency ETFs), CEW (WisdomTree), ETHE (Grayscale Ethereum), IBIT.INDX (iShares Bitcoin)
- **Null Pattern:** 0% - fully populated
- **Usage:** Primary identifier for filtering specific instruments; potential join key with other financial tables

### **name** (STRING)
- **Description:** Full legal name of the fund or instrument
- **Null Pattern:** 19.51% - missing for some records
- **Notable:** Includes various currency trusts (Australian Dollar, British Pound, Canadian Dollar, Euro, Japanese Yen), cryptocurrency trusts, and emerging market strategies
- **Usage:** Human-readable identifier; use for display purposes

### **period_start_date** (DATE)
- **Description:** Beginning date of the analysis period
- **Range:** 2020-12-18 to 2025-09-25
- **Null Pattern:** 0% - fully populated
- **Usage:** Temporal filtering; calculate actual period lengths; note some dates extend into future (potential projections)

### **period_end_date** (DATE)
- **Description:** Ending date of the analysis period
- **Range:** 2024-12-16 to 2025-12-16
- **Null Pattern:** 0% - fully populated
- **Usage:** Temporal filtering; paired with start_date for range queries

### **trading_days** (INT64)
- **Description:** Number of trading days in the analysis period
- **Range:** 1 to 1,005 days
- **Common Values:** 1 (single day), 57-68 (quarterly), 123 (semi-annual), 236 (annual), 1004-1005 (5-year)
- **Null Pattern:** 0% - fully populated
- **Usage:** Normalization factor for aggregations; filter for minimum data requirements

### **positive_days** (INT64)
- **Description:** Count of days with positive price movement
- **Range:** 0 to 322 days
- **Null Pattern:** 0% - fully populated
- **Usage:** Performance metric; calculate success rates

### **negative_days** (INT64)
- **Description:** Count of days with negative price movement
- **Range:** 0 to 333 days
- **Null Pattern:** 0% - fully populated
- **Usage:** Risk metric; pair with positive_days for performance analysis

### **neutral_days** (INT64)
- **Description:** Count of days with no price change
- **Range:** 0 to 90 days
- **Common Values:** 0-7, with outliers at 12 and 16
- **Null Pattern:** 0% - fully populated
- **Usage:** Market activity indicator; typically low values

### **total_return_pct** (FLOAT64)
- **Description:** Total percentage return over the period
- **Range:** -35.33% to +67.12%
- **Null Pattern:** 19.51% - matches other price-related NULL patterns
- **Usage:** Primary performance metric; good for ranking and comparison queries

### **avg_daily_return_pct** (FLOAT64)
- **Description:** Average daily percentage return
- **Range:** -2.0475% to +0.0871%
- **Null Pattern:** 0% - fully populated
- **Usage:** Normalized performance metric; comparable across different time periods

### **volatility_pct** (FLOAT64)
- **Description:** Standard deviation of returns (volatility measure)
- **Range:** 3.01% to 58.92%
- **Null Pattern:** 19.51% - NULL for single-day periods and incomplete records
- **Usage:** Risk assessment; filter for high/low volatility instruments

### **total_price_change** (FLOAT64)
- **Description:** Absolute price change in currency units
- **Range:** -$12.39 to +$15.22
- **Null Pattern:** 0% - fully populated
- **Usage:** Dollar-amount performance tracking

### **win_rate_pct** (FLOAT64)
- **Description:** Percentage of trading days with positive returns
- **Range:** 0.0% to 100.0%
- **Null Pattern:** 0% - fully populated
- **Usage:** Success rate metric; typically ranges 30-50% for currency instruments

### **avg_daily_price_change** (FLOAT64)
- **Description:** Average daily price change in currency units
- **Range:** -$0.69 to +$0.1063
- **Null Pattern:** 0% - fully populated
- **Usage:** Absolute daily movement metric

### **worst_day_change** (FLOAT64)
- **Description:** Largest single-day price decline (or smallest gain)
- **Range:** -$4.07 to +$0.11
- **Null Pattern:** 0% - fully populated
- **Usage:** Maximum drawdown risk assessment

### **best_day_change** (FLOAT64)
- **Description:** Largest single-day price gain
- **Range:** -$0.69 to +$5.53
- **Null Pattern:** 0% - fully populated
- **Usage:** Maximum upside potential assessment

### **period_start_price** (FLOAT64)
- **Description:** Price at the beginning of the analysis period
- **Range:** $17.97 to $129.28
- **Null Pattern:** 19.51% - matches incomplete record pattern
- **Usage:** Calculate returns; establish baseline values

### **period_end_price** (FLOAT64)
- **Description:** Price at the end of the analysis period
- **Range:** $18.05 to $129.35
- **Null Pattern:** 19.51% - matches incomplete record pattern
- **Usage:** Current/ending valuations; calculate returns

---

## Potential Query Considerations

### **Good Filtering Columns:**
- `symbol` - Filter specific currency instruments
- `time_period` - Analyze specific timeframes
- `exchange` - Distinguish between exchange types
- `asset_type` - Separate ETFs from stocks (handle NULLs)
- Date ranges using `period_start_date` and `period_end_date`
- Performance thresholds on `total_return_pct`, `volatility_pct`, `win_rate_pct`

### **Good Grouping/Aggregation Columns:**
- `symbol` - Aggregate performance across time periods
- `time_period` - Compare short vs long-term performance
- `exchange` - Compare performance by exchange
- `asset_type` - Compare ETFs vs stocks (WHERE asset_type IS NOT NULL)

### **Potential Join Keys:**
- `symbol` - Primary key for joining with other financial instrument tables
- `exchange` - Join with exchange reference data
- Combination of `symbol` + `time_period` - Unique identifier within this table

### **Data Quality Considerations:**
1. **NULL Handling:** ~20% of records have NULLs in price and return columns - always use IS NULL checks or COALESCE
2. **Volatility Calculation:** NULL for single-day periods (trading_days = 1) - filter appropriately
3. **Future Dates:** Some records extend to 2025 - may be projections; verify data source
4. **Single-Day Records:** 7 unique records with trading_days = 1 have limited analytical value
5. **Price Consistency:** Verify period_end_price - period_start_price ≈ total_price_change for data validation
6. **Time Period Alignment:** Different symbols may have different date ranges for the same time_period label

### **Recommended Query Patterns:**
```sql
-- Always include NULL handling for incomplete records
WHERE total_return_pct IS NOT NULL

-- Filter minimum trading days for meaningful analysis
WHERE trading_days >= 60

-- Compare performance across time periods
GROUP BY symbol, time_period

-- Rank by risk-adjusted returns
ORDER BY (total_return_pct / NULLIF(volatility_pct, 0)) DESC
```

---

## Keywords

currency trading, ETF performance, foreign exchange, FX analysis, currency pairs, Invesco CurrencyShares, trading metrics, volatility analysis, win rate, return on investment, ROI, price analysis, cryptocurrency, Bitcoin ETF, Ethereum ETF, Australian Dollar, British Pound, Canadian Dollar, Euro, Japanese Yen, emerging markets, time series analysis, trading days, financial instruments, market performance, risk metrics, NYSE ARCA, ARCX, OTC Markets, index funds, total return, daily returns, drawdown, best day, worst day, historical performance, multi-period analysis

---

## Table and Column Documentation

**Table Comment:** Not provided in the source data.

**Column Comments:** No explicit column comments were provided in the source data. Column descriptions above are inferred from data patterns and standard financial terminology.