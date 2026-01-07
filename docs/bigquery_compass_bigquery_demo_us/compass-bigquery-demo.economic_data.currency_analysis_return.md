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
# Currency Analysis Return Table Documentation

## Overall Dataset Characteristics

**Total Rows:** 23,282

**General Description:** This table contains historical currency exchange-traded fund (ETF) and cryptocurrency performance data with daily price snapshots and rolling time-period analytics. The dataset tracks 8 different currency-related securities across 3 exchanges over approximately 3,524 distinct trading dates (roughly 10 years of data based on sample dates from 2013-2024).

**Data Quality Observations:**
- Core fields (date, symbol, exchange, current_price, current_volume) have 100% completeness
- Significant null percentages in percentage change columns (ranging from 23% to 47%)
- Current high/low values have 13.43% nulls
- Rolling period high/low values show increasing null percentages with shorter timeframes
- Very low null percentage (0.07%) in standard deviation metrics
- Data appears well-structured with consistent formatting across numeric fields

**Notable Patterns:**
- Trading volume varies dramatically (0 to 168M), suggesting different liquidity profiles
- Price ranges span from ~$5 to $580, indicating diverse asset types
- Percentage changes show extreme volatility, particularly in cryptocurrency assets (ranging from -94.5% to +692%)
- Standard deviation metrics are consistently populated, enabling volatility analysis

## Column Details

### Identifiers and Temporal Data

**date (DATE)**
- Format: YYYY-MM-DD
- Complete coverage (0% nulls)
- Spans approximately 2013-2024
- 3,524 unique dates suggests daily trading data with some gaps
- **Query Use:** Primary temporal filter, grouping by date/time periods

**symbol (STRING)**
- 8 distinct securities tracked:
  - **CEW**: Currency Shares Emerging Markets ETF
  - **ETHE**: Grayscale Ethereum Trust
  - **FXA**: Australian Dollar ETF
  - **FXB**: British Pound ETF  
  - **FXC**: Canadian Dollar ETF
  - **FXE**: Euro Currency ETF
  - **FXY**: Japanese Yen ETF
  - **IBIT.INDX**: Bitcoin-related index
- **Query Use:** Essential grouping field, join key for security master tables

**exchange (STRING)**
- 3 distinct values:
  - **ARCX**: NYSE Arca (most currency ETFs)
  - **OTCM**: OTC Markets (ETHE)
  - **INDX**: Index (IBIT.INDX)
- **Query Use:** Filtering by market type, regulatory analysis

### Current Day Price/Volume Data

**current_price (FLOAT64)**
- Range: $4.72 to $580.00
- Complete data (0% nulls)
- High precision decimal values
- Wide range suggests mix of traditional currency ETFs (lower prices) and crypto assets (higher prices)
- **Query Use:** Price-based filtering, current valuation calculations

**current_volume (FLOAT64)**
- Range: 0 to 168,213,523
- Complete data (0% nulls)
- Zero volume days present (illiquid periods or data artifacts)
- Extreme variance indicates very different liquidity profiles
- **Query Use:** Liquidity analysis, volume-weighted calculations

**current_high (FLOAT64)**
- Range: $4.84 to $169.06
- 13.43% nulls (likely for INDX exchange or specific symbols)
- Intraday high price
- **Query Use:** Intraday volatility analysis, high/low spreads

**current_low (FLOAT64)**
- Range: $4.62 to $168.76
- 13.43% nulls (matches current_high pattern)
- Intraday low price
- **Query Use:** Intraday volatility analysis, support/resistance levels

### 1-Year Rolling Metrics

**high_1yr (FLOAT64)**
- Range: $8.69 to $169.06
- 5.76% nulls (early data points lacking full year history)
- 52-week high
- **Query Use:** Comparing current price to 52-week range

**low_1yr (FLOAT64)**
- Range: $4.62 to $156.65
- 5.76% nulls
- 52-week low
- **Query Use:** Price range analysis, support levels

**pct_change_1yr (FLOAT64)**
- Range: -89.47% to +623.26%
- 28.02% nulls (highest among return metrics)
- Extreme positive values suggest cryptocurrency assets
- **Query Use:** Annual performance ranking, volatility screening

**std_diff_1yr (FLOAT64)**
- Range: 0.0 to 259.17
- Only 0.07% nulls (most complete metric)
- Standard deviation from mean price
- **Query Use:** Volatility analysis, risk metrics

### 9-Month Rolling Metrics

**high_9mo (FLOAT64)**
- Range: $8.69 to $169.06
- 7.74% nulls
- **Query Use:** Medium-term resistance levels

**low_9mo (FLOAT64)**
- Range: $4.62 to $159.90
- 7.74% nulls
- **Query Use:** Medium-term support levels

**std_diff_9mo (FLOAT64)**
- Range: 0.0 to 259.17
- 0.07% nulls
- **Query Use:** Medium-term volatility comparison

**pct_change_9mo (FLOAT64)**
- Range: -93.29% to +518.56%
- 47.34% nulls (highest null percentage)
- **Query Use:** 3-quarter performance analysis

### 6-Month Rolling Metrics

**high_6mo (FLOAT64)**
- Range: $8.69 to $169.06
- 9.61% nulls
- **Query Use:** Semi-annual price range analysis

**low_6mo (FLOAT64)**
- Range: $4.62 to $162.24
- 9.61% nulls
- **Query Use:** Semi-annual support levels

**pct_change_6mo (FLOAT64)**
- Range: -94.5% to +692.44%
- 44.25% nulls
- Contains most extreme positive return (692.44%)
- **Query Use:** Semi-annual performance screening

**std_diff_6mo (FLOAT64)**
- Range: 0.0 to 259.17
- 0.07% nulls
- **Query Use:** Semi-annual volatility metrics

### 3-Month Rolling Metrics

**high_3mo (FLOAT64)**
- Range: $8.69 to $169.06
- 11.50% nulls
- **Query Use:** Quarterly resistance analysis

**low_3mo (FLOAT64)**
- Range: $4.62 to $164.38
- 11.50% nulls
- **Query Use:** Quarterly support analysis

**std_diff_3mo (FLOAT64)**
- Range: 0.0 to 259.17
- 0.07% nulls
- **Query Use:** Short-term volatility analysis

**pct_change_3mo (FLOAT64)**
- Range: -92.95% to +369.62%
- 23.52% nulls
- **Query Use:** Quarterly performance tracking

### 1-Month Rolling Metrics

**high_1mo (FLOAT64)**
- Range: $6.55 to $169.06
- 12.77% nulls
- **Query Use:** Monthly price range analysis

**low_1mo (FLOAT64)**
- Range: $4.62 to $166.96
- 12.77% nulls
- **Query Use:** Monthly support levels

**std_diff_1mo (FLOAT64)**
- Range: 0.0 to 259.17
- 0.07% nulls
- **Query Use:** Monthly volatility screening

**pct_change_1mo (FLOAT64)**
- Range: -91.99% to +297.01%
- 42.29% nulls
- **Query Use:** Monthly momentum analysis

## Query Considerations

### Excellent Filtering Columns
- **symbol**: Essential for security-specific analysis
- **exchange**: Market segmentation
- **date**: Time-based filtering and trending
- **current_volume**: Liquidity screening (exclude zero/low volume)
- **pct_change_*** fields: Performance-based screening

### Good Grouping/Aggregation Columns
- **symbol**: Security-level aggregations
- **exchange**: Market-level summaries
- **date** (with DATE_TRUNC): Time-series aggregations
- Combined grouping (symbol + time period) for cohort analysis

### Potential Join Keys
- **(date, symbol)**: Composite key for joining with other financial datasets
- **symbol**: Join to security master tables for metadata
- **exchange**: Join to exchange/market reference data

### Data Quality Considerations

**High Null Percentage Fields:**
- Percentage change metrics have 23-47% nulls - use COALESCE or filter out nulls
- Consider that nulls may represent:
  - Insufficient historical data for calculation
  - Non-trading periods
  - Data collection gaps

**Zero Values:**
- current_volume can be 0 (consider filtering WHERE current_volume > 0)
- std_diff metrics can be 0 (no volatility periods)

**Extreme Values:**
- Cryptocurrency assets (ETHE, IBIT.INDX) show extreme percentage changes
- Consider separate analysis or outlier handling for crypto vs. traditional currency ETFs

**Time-Based Queries:**
- Early dates may have incomplete rolling metrics
- Consider WHERE clauses that ensure minimum data availability
- Account for market holidays/non-trading days in date-based aggregations

**Recommended Filters:**
```sql
-- For reliable percentage change analysis
WHERE pct_change_1yr IS NOT NULL

-- For liquid securities only  
WHERE current_volume > 1000

-- For complete daily data
WHERE current_high IS NOT NULL AND current_low IS NOT NULL

-- Exclude early bootstrap periods
WHERE date >= '2014-01-01'
```

## Keywords

currency exchange rates, ETF performance, forex, cryptocurrency, ETHE Ethereum, Bitcoin IBIT, currency pairs, FX trading, rolling returns, volatility analysis, standard deviation, price momentum, intraday trading, 52-week high/low, percentage returns, trading volume, liquidity analysis, Australian dollar FXA, British pound FXB, Canadian dollar FXC, Euro FXE, Japanese yen FXY, emerging markets CEW, time series analysis, financial markets, technical indicators, price ranges

## Table and Column Docs

**Table Comment:** Not provided

**Column Comments:** Not provided