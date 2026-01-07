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
# Currency Analysis Return Table - Comprehensive Summary

## Overall Dataset Characteristics

**Total Rows:** 1,120

**General Description:** This table contains aggregated currency/ETF trading data with monthly and quarterly metrics, including forward-looking percentage change indicators. The dataset spans from 2012 to 2026 with 169 unique months of data across 8 different currency-related symbols traded on 3 exchanges.

**Data Quality Observations:**
- Core trading data (prices, volumes, dates) has 0% null values and is highly reliable
- Forward-looking percentage change metrics have moderate nulls (2.95% to 9.38%), increasing with longer time horizons
- Approximately half of the columns (26 out of 49) are completely empty (100% null), suggesting these are placeholder columns for future use or deprecated fields
- High cardinality in price fields (1,116-1,119 unique values) indicates detailed, granular data

**Notable Patterns:**
- Data is organized hierarchically: monthly aggregations feed into quarterly aggregations
- Forward-looking metrics (pct_change_q1_forward through q4_forward) suggest this is used for predictive/forecasting analysis
- Price ranges vary significantly by symbol (from ~$5 to ~$261), indicating diverse currency pairs or asset types

## Column Details

### Identification & Categorization Columns

**exchange (STRING)**
- Three exchange types: ARCX (NYSE Arca), INDX (Index), OTCM (OTC Markets)
- No nulls - reliable for filtering and grouping
- Primary categorization dimension

**symbol (STRING)**
- 8 unique currency/crypto ETF symbols
- Includes: CEW, ETHE (Ethereum), FXA (Australian Dollar), FXB (British Pound), FXC (Canadian Dollar), FXE (Euro), FXY (Japanese Yen), IBIT.INDX (Bitcoin Index)
- No nulls - excellent join key and filter dimension

### Temporal Dimensions

**year_month (STRING)**
- Format: "YYYY-MM" (e.g., "2024-12")
- 169 unique months spanning the dataset
- No nulls - reliable for time-based filtering

**month_date (DATE)**
- First day of each month
- Parallel to year_month but in DATE format
- Better for date arithmetic and SQL date functions

**year_quarter (STRING)**
- Format: "YYYY-QN" (e.g., "2024-Q3")
- 57 unique quarters
- Useful for quarterly aggregations and comparisons

**year_val (INT64)**
- Range: 2012-2026 (15 years)
- No nulls - good for year-over-year analysis

**quarter_num (INT64)**
- Values: 1, 2, 3, 4
- Represents quarter within year
- Useful for seasonal analysis

### Monthly Trading Metrics

**monthly_avg_close (FLOAT64)**
- Range: $5.72 to $171.27
- 1,118 unique values
- Average closing price for the month
- No nulls - reliable for analysis

**monthly_avg_open (FLOAT64)**
- Range: $5.80 to $210.90
- 1,119 unique values
- Note: Maximum significantly higher than close, suggesting volatility

**monthly_avg_low (FLOAT64)**
- Range: $5.59 to $167.79
- Lowest average price in month

**monthly_avg_high (FLOAT64)**
- Range: $5.91 to $261.45
- Highest value across all price metrics
- Critical for understanding price volatility

**monthly_avg_volume (FLOAT64)**
- Range: 1.0 to 75,840,296
- Extremely wide range indicates different liquidity levels across symbols
- ETHE and IBIT.INDX likely have highest volumes (crypto ETFs)

### Quarterly Trading Metrics

**quarterly_avg_close (FLOAT64)**
- Range: $7.46 to $171.27
- 380 unique values
- Aggregated from monthly data

**quarterly_avg_high (FLOAT64)**
- Range: $7.71 to $261.45
- Mirrors monthly high patterns

**quarterly_avg_open (FLOAT64)**
- Range: $7.42 to $210.90

**quarterly_avg_low (FLOAT64)**
- Range: $7.18 to $165.56

**quarterly_avg_volume (FLOAT64)**
- Range: 1.0 to 65,968,849
- Slightly lower maximum than monthly (expected with averaging)

### Forward-Looking Percentage Changes

**pct_change_q1_forward (FLOAT64)**
- 2.95% nulls (33 missing values)
- Range: -75.36% to +125.22%
- Represents 1-quarter forward return
- Lowest null rate among forward metrics

**pct_change_q2_forward (FLOAT64)**
- 5.09% nulls (57 missing values)
- Range: -81.87% to +285.32%
- Widest range - most volatile forward metric
- 2-quarter forward return

**pct_change_q3_forward (FLOAT64)**
- 7.23% nulls (81 missing values)
- Range: -86.16% to +169.62%
- 3-quarter forward return

**pct_change_q4_forward (FLOAT64)**
- 9.38% nulls (105 missing values)
- Range: -80.40% to +222.00%
- Highest null rate - limited by data horizon
- 4-quarter (1-year) forward return

### Deprecated/Unused Columns (100% NULL)

The following columns contain no data and should be excluded from queries:
- date, current_price, current_high, current_low, current_volume
- All historical lookback metrics: low_1yr, high_1yr, std_diff_1yr, pct_change_1yr
- 9-month lookback: low_9mo, high_9mo, pct_change_9mo, std_diff_9mo
- 6-month lookback: high_6mo, low_6mo, std_diff_6mo, pct_change_6mo
- 3-month lookback: high_3mo, low_3mo, pct_change_3mo, std_diff_3mo
- 1-month lookback: high_1mo, low_1mo, std_diff_1mo, pct_change_1mo

## Query Considerations

### Optimal Filtering Columns
- **symbol**: Filter by specific currency/ETF (8 options)
- **exchange**: Filter by trading venue (3 options)
- **year_val**: Year-based filtering (2012-2026)
- **year_quarter**: Quarterly analysis
- **month_date**: Date range queries using standard SQL date functions

### Grouping/Aggregation Opportunities
- **symbol**: Compare performance across currencies
- **exchange**: Analyze by trading venue
- **year_val**: Year-over-year trends
- **quarter_num**: Seasonal patterns
- **year_quarter**: Quarterly performance analysis

### Potential Join Keys
- **symbol + exchange**: Unique identifier for instrument
- **symbol + month_date**: Time-series joins
- **year_quarter**: Join with other quarterly economic data

### Data Quality Considerations
1. **Forward-looking metrics**: Nulls increase with time horizon - use COALESCE or WHERE clauses to handle
2. **Empty columns**: 26 columns are 100% null - avoid in SELECT statements
3. **Volume outliers**: Crypto ETFs (ETHE, IBIT.INDX) have 1000x+ volume vs currency ETFs
4. **Price scales**: Wide price ranges ($5-$261) - consider percentage changes rather than absolute values
5. **Time coverage**: Not all symbols have data for all time periods - verify data availability for specific date ranges

### Analytical Use Cases
- **Performance analysis**: Compare returns across currency pairs using pct_change metrics
- **Volatility studies**: Use high/low spreads and volume patterns
- **Forecasting validation**: Compare quarterly averages against forward-looking percentage changes
- **Seasonal patterns**: Group by quarter_num to identify seasonal trends
- **Liquidity analysis**: Volume metrics by symbol and time period

## Keywords

Currency ETFs, forex, foreign exchange, Bitcoin ETF, Ethereum ETF, cryptocurrency, ARCX, NYSE Arca, trading analysis, quarterly returns, monthly averages, forward returns, percentage change, price analysis, volume analysis, FXA Australian Dollar, FXB British Pound, FXC Canadian Dollar, FXE Euro, FXY Japanese Yen, IBIT Bitcoin, ETHE Ethereum, CEW currency basket, time series data, economic data, financial markets, technical analysis, predictive metrics, return forecasting, trading volume, OHLC data (open high low close)

## Table and Column Documentation

**Table Comment:** Not provided in the analysis report.

**Column Comments:** No individual column comments were provided in the analysis report. The column names are self-descriptive, following standard financial data conventions (avg for average, pct for percentage, q1/q2/q3/q4 for quarters, mo for month, yr for year).