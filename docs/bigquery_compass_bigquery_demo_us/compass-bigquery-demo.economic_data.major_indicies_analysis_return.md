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
- month_date (DATE)
- monthly_avg_close (FLOAT64)
- monthly_avg_high (FLOAT64)
- monthly_avg_low (FLOAT64)
- monthly_avg_open (FLOAT64)
- monthly_avg_volume (FLOAT64)
- pct_change_1mo (FLOAT64)
- pct_change_1yr (FLOAT64)
- pct_change_3mo (FLOAT64)
- pct_change_6mo (FLOAT64)
- pct_change_9mo (FLOAT64)
- pct_change_q1_forward (FLOAT64)
- pct_change_q2_forward (FLOAT64)
- pct_change_q3_forward (FLOAT64)
- pct_change_q4_forward (FLOAT64)
- quarter_num (INT64)
- quarterly_avg_close (FLOAT64)
- quarterly_avg_high (FLOAT64)
- quarterly_avg_low (FLOAT64)
- quarterly_avg_open (FLOAT64)
- quarterly_avg_volume (FLOAT64)
- std_diff_1mo (FLOAT64)
- std_diff_1yr (FLOAT64)
- std_diff_3mo (FLOAT64)
- std_diff_6mo (FLOAT64)
- std_diff_9mo (FLOAT64)
- symbol (STRING)
- year_month (STRING)
- year_quarter (STRING)
- year_val (INT64)
schema_hash: 91d6707310c607dd4be98ffa932c6e84cbe6494ca58762d292141382235612b2

---
# Table Documentation Summary: major_indicies_analysis_return

## Overall Dataset Characteristics

**Total Rows:** 845

**General Description:**
This table contains historical time-series analysis of major market indices and ETFs with monthly and quarterly aggregations. The dataset spans from 2012 to 2026 (with future projections), tracking 5 different financial instruments across 169 unique months and 57 quarters.

**Data Quality Observations:**
- Core data fields (symbol, exchange, dates, price averages) have 100% completeness
- Forward-looking percentage change metrics have 2-8% null values (expected for most recent periods)
- Volume data has ~7% null values, primarily for the VIX index (which is an index, not a traded security)
- Multiple columns (26 total) related to current prices and trailing period metrics are 100% null, suggesting these are placeholder columns not yet populated or calculated

**Notable Patterns:**
- Data is structured for both monthly and quarterly analysis with parallel metric sets
- Forward-looking return calculations (pct_change_q1/q2/q3/q4_forward) suggest this table is used for predictive modeling or performance tracking
- Price ranges vary significantly across symbols (VIX: ~10-40, ETFs: ~85-686)

## Column Details

### Identification & Taxonomy Columns

**symbol (STRING)**
- No null values (100% complete)
- 5 unique values: DIA, IWM, QQQ, SPY, VIX.INDX
- Represents major market indices/ETFs:
  - SPY: S&P 500 ETF
  - QQQ: NASDAQ-100 ETF
  - DIA: Dow Jones Industrial Average ETF
  - IWM: Russell 2000 ETF
  - VIX.INDX: Volatility Index
- **Usage:** Primary filtering column for symbol-specific queries

**exchange (STRING)**
- No null values (100% complete)
- 3 unique values: ARCX, INDX, XNAS
- Exchange codes where instruments are listed
- **Usage:** Can filter by exchange or join with exchange reference tables

### Temporal Columns

**month_date (DATE)**
- No null values (100% complete)
- 169 unique values spanning 2012-2026
- Represents the first day of each month
- **Usage:** Primary date filter for monthly analysis, trending, and time-series queries

**year_month (STRING)**
- No null values (100% complete)
- 169 unique values
- Format: "YYYY-MM" (e.g., "2014-09")
- **Usage:** Human-readable date grouping, alternative to month_date for filtering

**year_quarter (STRING)**
- No null values (100% complete)
- 57 unique values
- Format: "YYYY-QN" (e.g., "2015-Q4")
- **Usage:** Quarterly aggregation and filtering

**quarter_num (INT64)**
- No null values (100% complete)
- Values: 1, 2, 3, 4
- **Usage:** Seasonality analysis, quarter-specific filtering

**year_val (INT64)**
- No null values (100% complete)
- Range: 2012-2026 (15 unique years)
- **Usage:** Year-over-year comparisons, annual aggregations

### Monthly Price Metrics

**monthly_avg_close (FLOAT64)**
- No null values (100% complete)
- 844 unique values
- Range: 10.1255 to 683.6027
- Average closing price for each month
- **Usage:** Primary metric for monthly performance analysis

**monthly_avg_open (FLOAT64)**
- No null values (100% complete)
- 844 unique values
- Range: 10.1232 to 685.71
- **Usage:** Opening price analysis, gap analysis

**monthly_avg_low (FLOAT64)**
- No null values (100% complete)
- 845 unique values (more unique than rows - suggests high precision)
- Range: 9.7365 to 681.0538
- **Usage:** Support level analysis, volatility calculations

**monthly_avg_high (FLOAT64)**
- No null values (100% complete)
- 845 unique values
- Range: 10.6259 to 686.87
- **Usage:** Resistance level analysis, trading range calculations

**monthly_avg_volume (FLOAT64)**
- **6.98% null values** (59 nulls out of 845)
- 677 unique values
- Range: 0.0 to 269,395,925.0
- Nulls likely correspond to VIX.INDX (not a traded instrument)
- **Usage:** Liquidity analysis, volume-price relationships (exclude VIX or handle nulls)

### Quarterly Price Metrics

**quarterly_avg_close (FLOAT64)**
- No null values (100% complete)
- 285 unique values
- Range: 10.3102 to 683.17
- **Usage:** Quarterly trend analysis, longer-term performance metrics

**quarterly_avg_open (FLOAT64)**
- No null values (100% complete)
- 285 unique values
- Range: 10.2771 to 685.71

**quarterly_avg_high (FLOAT64)**
- No null values (100% complete)
- 285 unique values
- Range: 10.8594 to 686.87

**quarterly_avg_low (FLOAT64)**
- No null values (100% complete)
- 285 unique values
- Range: 9.8672 to 679.82

**quarterly_avg_volume (FLOAT64)**
- **6.86% null values**
- 229 unique values
- Range: 0.0 to 169,119,830.0
- Similar null pattern to monthly volume

### Forward-Looking Return Metrics

**pct_change_q1_forward (FLOAT64)**
- **2.37% null values** (20 nulls)
- 254 unique values
- Range: -32.56% to 118.72%
- Percentage change one quarter forward
- **Usage:** Predictive modeling, performance forecasting

**pct_change_q2_forward (FLOAT64)**
- **4.14% null values** (35 nulls)
- 260 unique values
- Range: -35.93% to 147.85%
- Two quarters forward performance

**pct_change_q3_forward (FLOAT64)**
- **5.92% null values** (50 nulls)
- 258 unique values
- Range: -40.11% to 116.27%
- Three quarters forward performance

**pct_change_q4_forward (FLOAT64)**
- **7.69% null values** (65 nulls)
- 252 unique values
- Range: -47.66% to 127.57%
- Four quarters (1 year) forward performance
- **Usage:** All forward metrics useful for return prediction, backtesting strategies

### Placeholder/Unpopulated Columns (100% NULL)

The following 26 columns are entirely null and appear to be reserved for future calculations:
- **date** (DATE)
- **current_price, current_high, current_low, current_volume** (FLOAT64)
- **high_1yr, low_1yr, pct_change_1yr, std_diff_1yr** (FLOAT64) - 1-year metrics
- **high_9mo, low_9mo, pct_change_9mo, std_diff_9mo** (FLOAT64) - 9-month metrics
- **high_6mo, low_6mo, pct_change_6mo, std_diff_6mo** (FLOAT64) - 6-month metrics
- **high_3mo, low_3mo, pct_change_3mo, std_diff_3mo** (FLOAT64) - 3-month metrics
- **high_1mo, low_1mo, pct_change_1mo, std_diff_1mo** (FLOAT64) - 1-month metrics

**Note:** These columns should be excluded from queries or require special handling to avoid null-related issues.

## Potential Query Considerations

### Optimal Filtering Columns
- **symbol**: Essential for instrument-specific analysis
- **year_val**: Efficient for year-based filtering
- **year_quarter**: Natural for quarterly analysis
- **month_date**: Best for date range queries
- **exchange**: For exchange-specific queries

### Grouping/Aggregation Columns
- **symbol**: Group by instrument
- **year_val**: Annual aggregations
- **year_quarter** or **quarter_num**: Quarterly patterns
- **year_month**: Monthly trends
- Combination groupings (e.g., symbol + year) for comparative analysis

### Join Considerations
- **symbol + exchange**: Potential join key to instrument master tables
- **month_date** or **year_month**: Time-based joins to other economic data
- No apparent foreign key relationships defined in this analysis

### Data Quality Considerations for Queries

1. **Volume Handling**: ~7% null values in volume columns
   - Filter out VIX.INDX when analyzing volume
   - Use COALESCE or NULL-safe functions
   - Example: `WHERE monthly_avg_volume IS NOT NULL`

2. **Forward Returns**: Increasing null percentages (2.37% to 7.69%)
   - Most recent periods naturally lack forward-looking data
   - Use appropriate WHERE clauses or LAG/LEAD functions
   - Consider filtering: `WHERE pct_change_q1_forward IS NOT NULL`

3. **Null Columns**: 26 columns are 100% null
   - Exclude from SELECT statements
   - Do not use in WHERE, GROUP BY, or ORDER BY clauses

4. **Date Handling**: Multiple date representations
   - Choose appropriate format: DATE (month_date) vs STRING (year_month)
   - DATE type preferred for arithmetic and range comparisons

5. **Price Scale Variance**: 
   - VIX ranges 10-40 (volatility index)
   - ETFs range 85-686 (price levels)
   - Consider symbol-specific normalization for cross-instrument comparisons

### Example Query Patterns

**Best for time-series trending:**
```sql
WHERE symbol = 'SPY' 
  AND month_date BETWEEN '2020-01-01' AND '2023-12-31'
ORDER BY month_date
```

**Best for quarterly performance:**
```sql
WHERE year_quarter = '2023-Q2'
GROUP BY symbol
```

**Best for forward-looking analysis:**
```sql
WHERE pct_change_q1_forward IS NOT NULL
  AND symbol IN ('SPY', 'QQQ')
```

## Keywords

market indices, ETF, stock market, SPY, QQQ, DIA, IWM, VIX, volatility index, time series, monthly data, quarterly data, financial analysis, returns, performance metrics, forward returns, predictive analysis, S&P 500, NASDAQ, Dow Jones, Russell 2000, price data, OHLC, open high low close, volume, trading volume, exchange data, ARCX, XNAS, INDX, historical prices, market trends, seasonality, quarterly performance, annual returns, backtesting, forecasting, economic data, market indicators

## Table and Column Documentation

**Table Comment:** Not provided in the analysis

**Column Comments:** No column-level comments were provided in the original analysis. The column names are self-documenting (e.g., monthly_avg_close, pct_change_q1_forward), suggesting this is a derived/analytical table rather than a source system table.