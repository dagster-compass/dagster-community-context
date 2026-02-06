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
# Table Summary: us_sector_analysis_return

## Overall Dataset Characteristics

**Total Rows:** 28,253

**General Description:**
This table contains historical price and return analysis data for US sector ETFs traded on the ARCX exchange. The data spans from 2012 to 2025, tracking 11 different sector ETFs with daily price metrics and multi-period performance statistics (1-month, 3-month, 6-month, 9-month, and 1-year lookback periods).

**Data Quality Observations:**
- Core identification fields (exchange, date, symbol) have no null values
- Price and volume data are complete (0% nulls)
- High/low price fields have 6.87% nulls for current period, increasing slightly for historical periods
- Percentage change fields have significant nulls: 1-month (42.29%), 3-month (23.71%), 6-month (44.57%), 9-month (47.85%), 1-year (28.92%)
- Standard deviation fields are nearly complete with only 0.08% nulls
- Null patterns suggest data is missing for early trading periods or calculation limitations

**Notable Patterns:**
- 11 sector ETFs tracked consistently across ~3,534 trading dates
- Daily granularity with approximately 8 records per trading day (11 symbols / trading days)
- All data from single exchange (ARCX)
- Price ranges vary significantly by sector (from ~$20 to ~$305)
- Volume ranges from 34 to 233 million shares traded

## Column Details

### Identification Columns

**exchange (STRING)**
- Single value: "ARCX" (NYSE Arca exchange)
- No nulls, serves as constant identifier
- Not useful for filtering or grouping

**date (DATE)**
- 3,534 unique dates covering trading days from 2012 to 2025
- No nulls, complete coverage
- Primary time dimension for analysis
- Key column for time-series queries and trend analysis

**symbol (STRING)**
- 11 unique sector ETF symbols: XLB, XLC, XLE, XLF, XLI, XLK, XLP, XLRE, XLU, XLV, XLY
- No nulls, complete coverage
- Represents different economic sectors (e.g., XLE=Energy, XLF=Financials, XLK=Technology)
- Primary dimension for sector comparison queries

### Current Trading Metrics

**current_price (FLOAT64)**
- Range: $20.61 to $304.13
- No nulls, complete daily pricing
- Daily closing price for each ETF
- Key metric for valuation queries

**current_volume (FLOAT64)**
- Range: 34 to 233,067,911 shares
- 28,128 unique values (highly variable)
- No nulls
- Indicator of trading liquidity and market interest

**current_low (FLOAT64)**
- Range: $19.62 to $301.87
- 6.87% nulls (1,940 records)
- Intraday low price
- Useful for volatility analysis

**current_high (FLOAT64)**
- Range: $22.02 to $305.99
- 6.87% nulls (matches current_low)
- Intraday high price
- Pairs with current_low for daily range analysis

### 1-Year Performance Metrics

**high_1yr (FLOAT64)**
- Range: $22.09 to $305.99
- 2.32% nulls (655 records)
- 52-week high price
- Key reference for performance benchmarking

**low_1yr (FLOAT64)**
- Range: $19.62 to $190.75
- 2.32% nulls
- 52-week low price
- Pairs with high_1yr for annual volatility

**pct_change_1yr (FLOAT64)**
- Range: -62.03% to +120.25%
- 28.92% nulls (8,169 records)
- Year-over-year percentage return
- Critical for long-term performance analysis
- Nulls likely represent insufficient historical data

**std_diff_1yr (FLOAT64)**
- Range: 0.0061 to 9.9359
- Only 0.08% nulls (23 records)
- Standard deviation metric (likely price distance from mean)
- Nearly complete data, useful for volatility filtering

### 9-Month Performance Metrics

**high_9mo (FLOAT64)**
- Range: $22.09 to $305.99
- 3.49% nulls (986 records)
- 9-month period high

**low_9mo (FLOAT64)**
- Range: $19.62 to $190.75
- 3.49% nulls
- 9-month period low

**pct_change_9mo (FLOAT64)**
- Range: -60.23% to +99.43%
- 47.85% nulls (13,518 records)
- High null percentage limits usability

**std_diff_9mo (FLOAT64)**
- Range: 0.0061 to 11.2954
- 0.08% nulls
- Volatility metric with good coverage

### 6-Month Performance Metrics

**high_6mo (FLOAT64)**
- Range: $22.09 to $305.99
- 4.58% nulls (1,294 records)

**low_6mo (FLOAT64)**
- Range: $19.62 to $238.29
- 4.58% nulls

**pct_change_6mo (FLOAT64)**
- Range: -59.7% to +85.57%
- 44.57% nulls (12,592 records)

**std_diff_6mo (FLOAT64)**
- Range: 0.0061 to 13.3443
- 0.08% nulls

### 3-Month Performance Metrics

**high_3mo (FLOAT64)**
- Range: $22.09 to $305.99
- 5.70% nulls (1,610 records)

**low_3mo (FLOAT64)**
- Range: $19.62 to $260.19
- 5.70% nulls

**pct_change_3mo (FLOAT64)**
- Range: -59.95% to +75.18%
- 23.71% nulls (6,696 records)
- Better coverage than 6/9-month metrics

**std_diff_3mo (FLOAT64)**
- Range: 0.0061 to 18.7594
- 0.08% nulls

### 1-Month Performance Metrics

**high_1mo (FLOAT64)**
- Range: $22.09 to $305.99
- 6.44% nulls (1,819 records)

**low_1mo (FLOAT64)**
- Range: $19.62 to $280.29
- 6.44% nulls

**pct_change_1mo (FLOAT64)**
- Range: -52.85% to +44.74%
- 42.29% nulls (11,946 records)
- High null rate despite short lookback period

**std_diff_1mo (FLOAT64)**
- Range: 0.0061 to 32.604
- 0.08% nulls

## Potential Query Considerations

### Excellent Filtering Columns
- **date**: Time-series filtering, date ranges, specific periods
- **symbol**: Sector-specific analysis, multi-sector comparisons
- **current_price**: Price range filtering
- **std_diff_[period]**: Volatility-based filtering (nearly complete data)

### Excellent Grouping/Aggregation Columns
- **symbol**: Sector-level aggregations
- **date** (by year/month/quarter): Temporal aggregations
- Price/volume metrics: Statistical aggregations (AVG, MIN, MAX)

### Join Keys
- **date + symbol**: Composite key for joining with other market data
- **symbol**: Join to sector metadata or company listings
- **date**: Join to broader market indices or economic indicators

### Data Quality Considerations

**High-Quality Queries:**
- Use current_price, current_volume, std_diff_* columns (complete data)
- Symbol and date-based filtering always reliable
- Volatility analysis using std_diff metrics

**Queries Requiring NULL Handling:**
- **Percentage change calculations**: 23-48% nulls depending on period
  - Use COALESCE or WHERE IS NOT NULL clauses
  - Consider filtering to dates with sufficient historical data
- **High/low price analysis**: 2-7% nulls
  - Current high/low: 6.87% nulls
  - Historical periods: 2-6% nulls increase with lookback period
- **Early date ranges**: More nulls in percentage changes for older dates

**Best Practices:**
- Filter by date >= '2013-01-01' for more complete pct_change data
- Use std_diff metrics instead of pct_change when completeness matters
- Consider data availability windows for each metric period
- Account for trading holidays and non-trading days in date-based queries

## Keywords

sector ETFs, ARCX, NYSE Arca, XLB materials, XLC communications, XLE energy, XLF financials, XLI industrials, XLK technology, XLP consumer staples, XLRE real estate, XLU utilities, XLV healthcare, XLY consumer discretionary, stock returns, price analysis, volatility metrics, standard deviation, percentage change, historical highs, historical lows, trading volume, time series, sector performance, market analysis, rolling returns, 52-week high, intraday prices, sector rotation, investment analysis

## Table and Column Documentation

**Table Comment:** Not provided

**Column Comments:** Not provided