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
# Table Documentation: major_indicies_analysis_return

## Keywords
stock market, financial indices, ETF data, market analysis, technical indicators, price movements, volatility, VIX, SPY, QQQ, DIA, IWM, time series data, trading volume, percentage changes, standard deviation, high-low ranges, NASDAQ, ARCX, market returns

---

## Overall Dataset Characteristics

**Total Rows:** 17,652

**Description:** This table contains comprehensive time-series analysis data for major market indices and ETFs, tracking daily price movements and various technical indicators across multiple timeframes (1 month to 1 year). The dataset spans from 2014 to 2024, covering approximately 3,567 unique trading dates.

**Data Quality Observations:**
- Core price data (current_price, date, symbol, exchange) has 100% completeness
- Significant null percentages in percentage change columns (23-47% missing)
- High/low price data for various timeframes show 22-26% null values
- Volume data is 93% complete (6.96% nulls)
- Standard deviation metrics are nearly complete (99.94%)
- The VIX index shows distinctive null patterns for high/low/volume fields

**Notable Patterns:**
- 5 major market symbols tracked: SPY, QQQ, DIA, IWM (ETFs) and VIX.INDX (volatility index)
- VIX.INDX systematically lacks high/low/volume data (explains some null percentages)
- Data spans across 3 exchanges: ARCX (NYSE Arca), XNAS (NASDAQ), INDX (Index)
- Comprehensive multi-timeframe analysis (1mo, 3mo, 6mo, 9mo, 1yr)

---

## Table and Column Documentation

**Table Comment:** Not provided in the source data.

**Column Comments:** No column-level comments were provided in the source data.

---

## Column Details

### Identification Columns

**exchange (STRING)**
- **Type:** Categorical identifier
- **Null Percentage:** 0% (complete)
- **Unique Values:** 3
- **Values:** ARCX, INDX, XNAS
- **Usage:** Identifies the exchange where the security trades
- **Notes:** ARCX = NYSE Arca (ETF marketplace), XNAS = NASDAQ, INDX = Index data

**symbol (STRING)**
- **Type:** Categorical identifier
- **Null Percentage:** 0% (complete)
- **Unique Values:** 5
- **Values:** DIA, IWM, QQQ, SPY, VIX.INDX
- **Usage:** Primary security identifier
- **Notes:** 
  - SPY = S&P 500 ETF
  - QQQ = NASDAQ-100 ETF
  - DIA = Dow Jones Industrial Average ETF
  - IWM = Russell 2000 ETF
  - VIX.INDX = CBOE Volatility Index

**date (DATE)**
- **Type:** Temporal dimension
- **Null Percentage:** 0% (complete)
- **Unique Values:** 3,567 trading days
- **Range:** Approximately 2014-2024 (10 years)
- **Sample Values:** 2022-05-04, 2022-03-04, 2024-04-29
- **Usage:** Primary time dimension for time-series analysis

### Current Day Metrics

**current_price (FLOAT64)**
- **Type:** Numeric (price)
- **Null Percentage:** 0% (complete)
- **Unique Values:** 15,191
- **Range:** 9.14 to 695.16
- **Usage:** Closing or current price for the trading day
- **Notes:** High uniqueness indicates precise pricing data

**current_high (FLOAT64)**
- **Type:** Numeric (price)
- **Null Percentage:** 26.58%
- **Unique Values:** 12,659
- **Range:** 52.35 to 696.09
- **Usage:** Intraday high price
- **Notes:** Nulls primarily from VIX.INDX which doesn't track intraday highs

**current_low (FLOAT64)**
- **Type:** Numeric (price)
- **Null Percentage:** 26.58%
- **Unique Values:** 12,668
- **Range:** 51.77 to 691.35
- **Usage:** Intraday low price
- **Notes:** Matching null pattern with current_high

**current_volume (FLOAT64)**
- **Type:** Numeric (volume)
- **Null Percentage:** 6.96%
- **Unique Values:** 14,059
- **Range:** 0.0 to 507,244,281
- **Usage:** Trading volume for the day
- **Notes:** Wide range indicates different liquidity levels across instruments; VIX has no volume

### 1-Year Lookback Metrics

**high_1yr (FLOAT64)**
- **Null Percentage:** 22.22%
- **Range:** 52.35 to 696.09
- **Unique Values:** 2,026

**low_1yr (FLOAT64)**
- **Null Percentage:** 22.22%
- **Range:** 51.77 to 493.86
- **Unique Values:** 1,004

**pct_change_1yr (FLOAT64)**
- **Null Percentage:** 26.85%
- **Range:** -76.07% to +479.47%
- **Unique Values:** 6,350
- **Usage:** Year-over-year percentage change
- **Notes:** Extreme values suggest high volatility periods

**std_diff_1yr (FLOAT64)**
- **Null Percentage:** 0.06% (nearly complete)
- **Range:** 0.0071 to 7.5789
- **Unique Values:** 13,284
- **Usage:** Standard deviation metric for 1-year period

### 9-Month Lookback Metrics

**high_9mo (FLOAT64)**
- **Null Percentage:** 23.35%
- **Range:** 52.35 to 696.09
- **Unique Values:** 2,057

**low_9mo (FLOAT64)**
- **Null Percentage:** 23.35%
- **Range:** 51.77 to 541.52
- **Unique Values:** 963

**pct_change_9mo (FLOAT64)**
- **Null Percentage:** 46.66% (highest among percentage changes)
- **Range:** -71.81% to +460.61%
- **Unique Values:** 4,930

**std_diff_9mo (FLOAT64)**
- **Null Percentage:** 0.06%
- **Range:** 0.0071 to 8.1189
- **Unique Values:** 13,629

### 6-Month Lookback Metrics

**high_6mo (FLOAT64)**
- **Null Percentage:** 24.40%
- **Range:** 52.35 to 696.09
- **Unique Values:** 2,177

**low_6mo (FLOAT64)**
- **Null Percentage:** 24.40%
- **Range:** 51.77 to 619.29
- **Unique Values:** 1,288

**pct_change_6mo (FLOAT64)**
- **Null Percentage:** 43.80%
- **Range:** -67.33% to +492.76%
- **Unique Values:** 4,476

**std_diff_6mo (FLOAT64)**
- **Null Percentage:** 0.06%
- **Range:** 0.0071 to 9.1109
- **Unique Values:** 13,598

### 3-Month Lookback Metrics

**high_3mo (FLOAT64)**
- **Null Percentage:** 25.47%
- **Range:** 52.35 to 696.09
- **Unique Values:** 2,586

**low_3mo (FLOAT64)**
- **Null Percentage:** 25.47%
- **Range:** 51.77 to 650.85
- **Unique Values:** 2,003

**pct_change_3mo (FLOAT64)**
- **Null Percentage:** 23.26%
- **Range:** -66.0% to +572.82%
- **Unique Values:** 4,503

**std_diff_3mo (FLOAT64)**
- **Null Percentage:** 0.06%
- **Range:** 0.0071 to 11.42
- **Unique Values:** 13,670

### 1-Month Lookback Metrics

**high_1mo (FLOAT64)**
- **Null Percentage:** 26.18%
- **Range:** 52.35 to 696.09
- **Unique Values:** 3,528

**low_1mo (FLOAT64)**
- **Null Percentage:** 26.18%
- **Range:** 51.77 to 676.57
- **Unique Values:** 2,741

**pct_change_1mo (FLOAT64)**
- **Null Percentage:** 42.20%
- **Range:** -57.04% to +397.17%
- **Unique Values:** 3,172

**std_diff_1mo (FLOAT64)**
- **Null Percentage:** 0.06%
- **Range:** 0.0071 to 17.7022
- **Unique Values:** 13,933
- **Notes:** Highest std_diff range indicates short-term volatility can exceed long-term

---

## Query Considerations

### Optimal Filtering Columns
- **symbol**: Perfect for filtering by specific ETF/index (5 distinct values)
- **exchange**: Useful for exchange-specific analysis (3 distinct values)
- **date**: Essential for time-series filtering and range queries
- **Current metrics**: Good for threshold-based filtering (price > X, volume > Y)

### Optimal Grouping/Aggregation Columns
- **symbol**: Primary grouping for cross-security analysis
- **date**: Time-series aggregations (daily, monthly, yearly trends)
- **exchange**: Exchange-level comparisons
- **Time-based aggregations**: Can extract YEAR(), MONTH(), QUARTER() from date

### Potential Join Keys
- **(symbol, date)**: Composite key for joining with other market data tables
- **symbol**: Can join with reference tables for ETF metadata
- **exchange**: Could join with exchange information tables
- **date**: Can join with economic indicators or market event tables

### Data Quality Considerations for Queries

1. **Null Handling Strategy:**
   - VIX.INDX systematically lacks high/low/volume data - filter out when analyzing these metrics
   - Percentage change columns have high null rates (23-47%) - use COALESCE or filter non-nulls
   - Always include null checks when using pct_change fields
   - std_diff columns are nearly complete and reliable for volatility analysis

2. **Symbol-Specific Behavior:**
   - VIX requires special handling due to its index nature (no volume, no intraday range)
   - Consider separate queries for VIX vs ETFs when analyzing trading metrics

3. **Timeframe Analysis:**
   - Longer timeframes (1yr) have better data completeness than shorter ones
   - Standard deviation columns are most reliable across all timeframes
   - Percentage change columns should include WHERE clauses to handle nulls

4. **Volume Analysis:**
   - Exclude VIX when analyzing volume metrics
   - Volume ranges vary dramatically (0 to 507M) - consider log scale or relative metrics

5. **Temporal Considerations:**
   - Dataset spans 10 years - ensure date filters account for data availability
   - Early dates may have limited lookback data (first year lacks full 1yr metrics)
   - Consider data recency when querying recent dates

6. **Price Range Considerations:**
   - Wide price ranges (9.14 to 695.16) across symbols - use symbol-specific comparisons
   - Percentage changes more meaningful than absolute price changes for cross-symbol analysis

7. **Volatility Metrics:**
   - std_diff columns increase with shorter timeframes (1mo > 3mo > 6mo > 1yr)
   - This is expected behavior and useful for volatility regime analysis