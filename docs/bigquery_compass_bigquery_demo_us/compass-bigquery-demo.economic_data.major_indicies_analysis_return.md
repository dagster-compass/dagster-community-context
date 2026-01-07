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
# Table Analysis Summary: major_indicies_analysis_return

## Overall Dataset Characteristics

**Total Rows:** 17,608

**General Description:**
This table contains comprehensive financial analysis data for major market indices, tracking their performance metrics across multiple timeframes (1 year, 9 months, 6 months, 3 months, and 1 month). The dataset spans from approximately 2015 to 2025 with 3,558 unique dates.

**Data Quality Observations:**
- Core fields (symbol, exchange, date, current_price) have 100% completeness
- Significant null percentages in high/low values (~22-26%) and percentage changes (~23-47%)
- VIX.INDX specifically shows null patterns for high/low values (appears to be index vs traded security)
- Volume data has ~7% nulls, with some 0.0 values particularly for VIX.INDX
- Very high completeness for standard deviation metrics (~99.94%)

**Notable Patterns:**
- 5 distinct symbols representing major market indices
- Price ranges vary dramatically by symbol (9.14 to 691.81)
- Volume ranges from 0 to over 500 million shares
- Standard deviation increases with shorter timeframes (volatility measurement)

## Column Details

### **Identifier Columns**

**symbol** (STRING)
- 5 unique values: DIA, IWM, QQQ, SPY, VIX.INDX
- No nulls (0.00%)
- Represents major market indices:
  - DIA: Dow Jones Industrial Average ETF
  - IWM: Russell 2000 Small Cap ETF
  - QQQ: NASDAQ-100 ETF
  - SPY: S&P 500 ETF
  - VIX.INDX: Volatility Index

**exchange** (STRING)
- 3 unique values: ARCX (NYSE Arca), INDX (Index), XNAS (NASDAQ)
- No nulls (0.00%)
- ARCX: Used for DIA, IWM, SPY
- XNAS: Used for QQQ
- INDX: Used for VIX.INDX

**date** (DATE)
- 3,558 unique dates
- No nulls (0.00%)
- Time series data spanning approximately 10 years
- Sample dates range from 2015 to 2025

### **Current Trading Metrics**

**current_price** (FLOAT64)
- Range: 9.14 to 691.81
- No nulls (0.00%)
- 15,156 unique values
- Represents the closing or current price for the trading day

**current_high** (FLOAT64)
- Range: 52.35 to 692.32
- **26.60% nulls** (significant - primarily VIX.INDX)
- 12,625 unique values
- Daily high price

**current_low** (FLOAT64)
- Range: 51.77 to 689.27
- **26.60% nulls** (matches current_high pattern)
- 12,633 unique values
- Daily low price

**current_volume** (FLOAT64)
- Range: 0.0 to 507,244,281.0
- **6.93% nulls**
- 14,023 unique values
- Trading volume; 0.0 values appear for VIX.INDX

### **1-Year Performance Metrics**

**high_1yr** (FLOAT64)
- Range: 52.35 to 692.32
- **22.23% nulls**
- 2,014 unique values
- 52-week high

**low_1yr** (FLOAT64)
- Range: 51.77 to 493.86
- **22.23% nulls**
- 1,004 unique values
- 52-week low

**std_diff_1yr** (FLOAT64)
- Range: 0.0071 to 7.58
- **0.06% nulls** (excellent coverage)
- 13,248 unique values
- Standard deviation measure for 1-year volatility

**pct_change_1yr** (FLOAT64)
- Range: -76.07% to 479.47%
- **26.85% nulls**
- 6,346 unique values
- Year-over-year percentage change
- Wide range indicates significant market events

### **9-Month Performance Metrics**

**high_9mo** (FLOAT64)
- Range: 52.35 to 692.32
- **23.36% nulls**
- 2,045 unique values

**low_9mo** (FLOAT64)
- Range: 51.77 to 510.27
- **23.36% nulls**
- 958 unique values

**std_diff_9mo** (FLOAT64)
- Range: 0.0071 to 8.12
- **0.06% nulls**
- 13,595 unique values

**pct_change_9mo** (FLOAT64)
- Range: -71.81% to 460.61%
- **46.64% nulls** (highest null rate)
- 4,918 unique values

### **6-Month Performance Metrics**

**high_6mo** (FLOAT64)
- Range: 52.35 to 692.32
- **24.42% nulls**
- 2,165 unique values

**low_6mo** (FLOAT64)
- Range: 51.77 to 618.05
- **24.42% nulls**
- 1,286 unique values

**std_diff_6mo** (FLOAT64)
- Range: 0.0071 to 9.11
- **0.06% nulls**
- 13,568 unique values

**pct_change_6mo** (FLOAT64)
- Range: -67.33% to 492.76%
- **43.79% nulls** (high null rate)
- 4,474 unique values

### **3-Month Performance Metrics**

**high_3mo** (FLOAT64)
- Range: 52.35 to 692.32
- **25.49% nulls**
- 2,574 unique values

**low_3mo** (FLOAT64)
- Range: 51.77 to 650.85
- **25.49% nulls**
- 2,002 unique values

**std_diff_3mo** (FLOAT64)
- Range: 0.0071 to 11.42
- **0.06% nulls**
- 13,631 unique values
- Higher max indicates increased short-term volatility

**pct_change_3mo** (FLOAT64)
- Range: -66.0% to 572.82%
- **23.25% nulls**
- 4,501 unique values

### **1-Month Performance Metrics**

**high_1mo** (FLOAT64)
- Range: 52.35 to 692.32
- **26.20% nulls**
- 3,514 unique values (more granular)

**low_1mo** (FLOAT64)
- Range: 51.77 to 671.20
- **26.20% nulls**
- 2,738 unique values

**std_diff_1mo** (FLOAT64)
- Range: 0.0071 to 17.70
- **0.06% nulls**
- 13,899 unique values
- Highest max value indicating most short-term volatility

**pct_change_1mo** (FLOAT64)
- Range: -57.04% to 397.17%
- **42.23% nulls**
- 3,171 unique values

## Query Considerations

### **Ideal Filtering Columns:**
- `symbol`: Perfect for filtering by specific index (5 distinct values)
- `exchange`: Useful for grouping by exchange type
- `date`: Essential for time-series analysis and date range filters
- `current_price`: Range filtering for price thresholds

### **Good Aggregation/Grouping Columns:**
- `symbol`: Primary grouping dimension
- `exchange`: Secondary grouping
- `date` (by year/month/quarter): Temporal aggregations
- Time period columns can be used for trend analysis

### **Potential Join Keys:**
- `symbol` + `date`: Composite key for joining with other market data
- `symbol`: For joining with symbol reference/metadata tables
- `exchange`: For joining with exchange information tables

### **Data Quality Considerations:**

1. **Null Handling:**
   - VIX.INDX has systemic nulls for high/low values (it's an index, not a traded security)
   - Percentage change fields have 23-47% nulls - queries should use `IS NOT NULL` filters
   - Consider excluding early date ranges where historical data may be incomplete

2. **Volume Considerations:**
   - VIX.INDX shows 0.0 volume (not applicable for indices)
   - Filter volume > 0 for actual trading activity analysis

3. **Standard Deviation Reliability:**
   - Extremely low null rate (0.06%) makes these columns reliable
   - Progressive increase in max values (1.4x to 2.3x) from 1yr to 1mo reflects volatility measurement

4. **Time Period Analysis:**
   - Shorter time periods (1mo, 3mo) have more granular high/low data
   - Longer periods (1yr) have fewer unique high/low values (expected)
   - Percentage changes show extreme values suggesting need for outlier handling

5. **Recommended Query Patterns:**
   - Always filter by symbol for performance
   - Use date ranges to avoid full table scans
   - Consider COALESCE for null percentage changes
   - Use standard deviation fields for volatility analysis

## Keywords

financial data, stock market, indices, ETF, market analysis, time series, volatility, price analysis, trading volume, DIA, SPY, QQQ, IWM, VIX, NASDAQ, NYSE, returns analysis, performance metrics, price movements, historical prices, standard deviation, percentage change, market trends, investment analysis, portfolio analysis

## Table and Column Documentation

**Table Comment:** Not provided

**Column Comments:** No column-level comments were provided in the source data.