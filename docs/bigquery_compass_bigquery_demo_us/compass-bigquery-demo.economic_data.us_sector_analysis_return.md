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

**Total Rows:** 28,154

**General Description:** This table contains comprehensive financial performance data for US sector ETFs traded on the NYSE Arca exchange. The dataset tracks 11 sector-specific ETFs across approximately 3,525 unique dates, providing detailed price movements, volatility metrics, and performance comparisons across multiple time horizons (1-month to 1-year).

**Data Quality Observations:**
- Core identifying columns (symbol, date, exchange) have no null values
- Variable null percentages across performance metrics, with higher nulls in percentage change columns (23-48%)
- Most recent time period metrics (1-month, 3-month) have higher null rates, likely due to data collection timing
- Price and volume data is complete (0% nulls)
- Standard deviation metrics are highly complete (0.08% nulls)

**Notable Patterns:**
- Data spans multiple years (2012-2026 based on sample dates)
- All trading occurs on ARCX (NYSE Arca) exchange
- Volume ranges dramatically (34 to 233M), suggesting varying liquidity periods
- Price ranges vary significantly by sector (20.61 to 304.13)

## Column Details

### Identifying Columns

**symbol (STRING)**
- Represents sector ETF ticker symbols
- 11 unique values covering major market sectors
- Values: XLB (Materials), XLC (Communication), XLE (Energy), XLF (Financials), XLI (Industrials), XLK (Technology), XLP (Consumer Staples), XLRE (Real Estate), XLU (Utilities), XLV (Healthcare)
- No nulls - reliable for filtering and grouping
- **Primary dimension for sector-based analysis**

**date (DATE)**
- Trading date with 3,525 unique values
- No nulls - complete date coverage
- Range includes historical data from 2012 through 2026
- **Primary time dimension for temporal analysis**

**exchange (STRING)**
- Single value: ARCX (NYSE Arca)
- No variation in dataset
- Not useful for filtering but provides context

### Current Trading Metrics

**current_price (FLOAT64)**
- Daily closing or current price
- Range: $20.61 to $304.13
- No nulls - complete price data
- 23,044 unique values indicating granular price movements
- **Key metric for current valuation**

**current_high (FLOAT64)**
- Intraday high price
- 6.89% nulls (1,939 records)
- Range: $22.02 to $305.99
- Slightly higher unique value count (23,393) than current_price

**current_low (FLOAT64)**
- Intraday low price
- 6.89% nulls (matching current_high)
- Range: $19.62 to $301.87
- 23,488 unique values

**current_volume (FLOAT64)**
- Daily trading volume
- No nulls - complete volume data
- Extreme range: 34 to 233,067,911 shares
- 28,033 unique values (nearly unique per row)
- **Key liquidity indicator**

### 1-Year Performance Metrics

**high_1yr (FLOAT64)**
- 52-week high price
- 2.33% nulls (656 records)
- Range: $22.09 to $305.99
- 2,832 unique values

**low_1yr (FLOAT64)**
- 52-week low price
- 2.33% nulls
- Range: $19.62 to $190.75
- 1,778 unique values

**std_diff_1yr (FLOAT64)**
- Standard deviation of price differences over 1 year
- Only 0.08% nulls (23 records) - highly complete
- Range: 0.0061 to 9.9359
- 13,001 unique values
- **Key volatility metric**

**pct_change_1yr (FLOAT64)**
- Percentage change over 1 year
- 28.91% nulls (8,140 records)
- Range: -62.03% to +120.25%
- **Important performance comparison metric**

### 9-Month Performance Metrics

**high_9mo, low_9mo (FLOAT64)**
- 3.50% nulls (985 records each)
- Similar ranges to 1-year metrics
- Intermediate timeframe for trend analysis

**std_diff_9mo (FLOAT64)**
- 0.08% nulls
- Range: 0.0061 to 11.2954
- 13,178 unique values

**pct_change_9mo (FLOAT64)**
- 47.83% nulls (13,463 records) - **highest null rate**
- Range: -60.23% to +99.43%
- Only 5,365 unique values

### 6-Month Performance Metrics

**high_6mo, low_6mo (FLOAT64)**
- 4.60% nulls (1,295 records each)
- Price ranges narrow compared to 1-year

**std_diff_6mo (FLOAT64)**
- 0.08% nulls
- Range: 0.0061 to 13.3179
- Higher volatility range than 9-month

**pct_change_6mo (FLOAT64)**
- 44.57% nulls (12,549 records)
- Range: -59.7% to +85.57%

### 3-Month Performance Metrics

**high_3mo, low_3mo (FLOAT64)**
- 5.72% nulls (1,610 records each)
- More unique values (4,223 and 3,708) due to shorter timeframe

**std_diff_3mo (FLOAT64)**
- 0.08% nulls
- Range: 0.0061 to 18.7177 - **widest volatility range**
- 13,371 unique values

**pct_change_3mo (FLOAT64)**
- 23.72% nulls (6,678 records)
- Range: -59.95% to +75.18%

### 1-Month Performance Metrics

**high_1mo, low_1mo (FLOAT64)**
- 6.46% nulls (1,819 records each)
- Highest unique value counts (6,212 and 5,422)
- Most granular short-term price tracking

**std_diff_1mo (FLOAT64)**
- 0.08% nulls
- Range: 0.0061 to 32.604 - **extreme volatility range**
- Most unique values (13,426)

**pct_change_1mo (FLOAT64)**
- 42.32% nulls (11,913 records)
- Range: -52.85% to +44.74%
- Only 2,674 unique values - **most constrained percentage change metric**

## Query Considerations

### Optimal Filtering Columns
- **symbol**: Perfect for sector-specific analysis (11 distinct sectors)
- **date**: Essential for time-based filtering and trend analysis
- **current_volume**: For liquidity-based filtering
- **pct_change_*** columns: For performance-based filtering (mind the null rates)

### Optimal Grouping/Aggregation Columns
- **symbol**: Primary grouping dimension for sector comparisons
- **date** (with time bucketing): For temporal aggregations
- Consider date ranges (year, quarter, month) for trend analysis

### Potential Join Keys
- **symbol + date**: Composite key for joining with other financial datasets
- **symbol**: For joining with sector metadata or company constituent tables
- **exchange**: Less useful given single value, but could join with exchange information tables

### Data Quality Considerations for Queries

1. **Null Handling Critical:**
   - Percentage change columns have 23-48% nulls - always use `IS NOT NULL` filters or COALESCE
   - 9-month percentage change has highest null rate (47.83%)
   - Current price columns (high/low) have 6.89% nulls - recent data may be incomplete
   - Standard deviation metrics are nearly complete (0.08% nulls) - most reliable volatility measures

2. **Timeframe Analysis:**
   - Longer timeframes (1yr) have better data completeness for pct_change metrics
   - Shorter timeframes (1mo, 3mo) have higher null percentages - may indicate rolling calculation windows

3. **Volatility Analysis:**
   - std_diff columns are highly complete and show increasing ranges for shorter periods
   - 1-month std_diff has extreme range (0.0061 to 32.604) - consider outlier handling

4. **Volume Considerations:**
   - Extreme volume range suggests periods of high/low liquidity
   - Consider log transformations for volume-based analysis

5. **Date Range:**
   - Dataset includes future dates (2026) - verify if these are projections or data errors
   - Historical depth goes back to at least 2012

## Keywords
sector ETFs, XL sectors, SPDR sectors, stock market performance, financial returns, volatility analysis, price movements, trading volume, percentage change, standard deviation, time series data, 52-week high/low, NYSE Arca, ARCX, XLK technology, XLV healthcare, XLF financials, XLE energy, XLI industrials, XLB materials, XLP consumer staples, XLU utilities, XLRE real estate, XLC communication, sector rotation, market analysis, ETF performance, investment returns, historical prices

## Table and Column Documentation

**Table Comment:** Not provided in the analysis report.

**Column Comments:** No specific column comments were provided in the analysis report. The column names are self-descriptive following a consistent naming pattern for timeframe-based metrics.