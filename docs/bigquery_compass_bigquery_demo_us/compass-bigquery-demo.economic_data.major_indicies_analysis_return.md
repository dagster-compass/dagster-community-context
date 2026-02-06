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
# Table Summary: major_indicies_analysis_return

## Overall Dataset Characteristics

This table contains **17,652 rows** of historical financial data tracking major market indices and ETFs over time. The dataset tracks 5 different securities (SPY, DIA, QQQ, IWM, and VIX.INDX) across approximately 3,567 unique dates, providing comprehensive time-series data for technical and fundamental analysis.

**Data Quality Observations:**
- Core identifiers (symbol, exchange, date, current_price) have 0% null values, indicating excellent data integrity for key fields
- Significant null percentages (22-47%) exist in percentage change and high/low metrics for various time periods, likely due to insufficient historical data for recent entries or early dataset records
- Standard deviation metrics (std_diff_*) have minimal nulls (~0.06%), showing consistent volatility calculations
- Volume data has moderate nulls (6.96%), possibly from non-trading days or data collection issues

**Notable Patterns:**
- The dataset spans multiple years (2013-2021 visible in samples), enabling long-term trend analysis
- Current high/low metrics show ~26.58% nulls, while volume shows only 6.96% nulls, suggesting these may be calculated differently
- Percentage change metrics show increasing null percentages from 1-month (~42%) to 9-month (~47%) periods, consistent with edge cases at dataset boundaries

## Column Details

### Identifier Columns

**symbol** (STRING)
- No null values (100% complete)
- 5 unique securities tracked: SPY, DIA, QQQ, IWM, VIX.INDX
- Represents major market indices/ETFs tracking different market segments
- SPY: S&P 500, DIA: Dow Jones, QQQ: NASDAQ-100, IWM: Russell 2000, VIX.INDX: Volatility Index

**exchange** (STRING)
- No null values (100% complete)
- 3 unique exchanges: ARCX (NYSE Arca), XNAS (NASDAQ), INDX (Index)
- Maps to security types: ETFs trade on ARCX/XNAS, VIX is an index (INDX)

**date** (DATE)
- No null values (100% complete)
- 3,567 unique dates spanning multiple years
- Represents trading days, essential for time-series analysis

### Price and Volume Metrics

**current_price** (FLOAT64)
- No null values (100% complete)
- Range: $9.14 to $695.16
- 15,191 unique values indicating high price granularity
- Core metric for all calculations

**current_low** (FLOAT64)
- 26.58% null values
- Range: $51.77 to $691.35
- 12,668 unique values
- Represents intraday low price

**current_high** (FLOAT64)
- 26.58% null values (same as current_low)
- Range: $52.35 to $696.09
- 12,659 unique values
- Represents intraday high price

**current_volume** (FLOAT64)
- 6.96% null values
- Range: 0 to 507,244,281 shares
- 14,059 unique values
- Zero values present (possibly non-trading periods or VIX index)

### 1-Year Metrics

**high_1yr** (FLOAT64)
- 22.22% null values
- Range: $52.35 to $696.09
- 2,026 unique values
- 52-week high price

**low_1yr** (FLOAT64)
- 22.22% null values
- Range: $51.77 to $493.86
- 1,004 unique values
- 52-week low price

**std_diff_1yr** (FLOAT64)
- 0.06% null values (excellent coverage)
- Range: 0.0071 to 7.5789
- 13,284 unique values
- Likely represents standard deviation or volatility measure

**pct_change_1yr** (FLOAT64)
- 26.85% null values
- Range: -76.07% to +479.47%
- 6,350 unique values
- Shows extreme values, capturing major market movements

### 9-Month Metrics

**high_9mo** (FLOAT64)
- 23.35% null values
- Range: $52.35 to $696.09
- 2,057 unique values

**low_9mo** (FLOAT64)
- 23.35% null values
- Range: $51.77 to $541.52
- 963 unique values

**std_diff_9mo** (FLOAT64)
- 0.06% null values
- Range: 0.0071 to 8.1189
- 13,629 unique values

**pct_change_9mo** (FLOAT64)
- 46.66% null values (highest null rate for percentage changes)
- Range: -71.81% to +460.61%
- 4,930 unique values

### 6-Month Metrics

**high_6mo** (FLOAT64)
- 24.40% null values
- Range: $52.35 to $696.09
- 2,177 unique values

**low_6mo** (FLOAT64)
- 24.40% null values
- Range: $51.77 to $619.29
- 1,288 unique values

**std_diff_6mo** (FLOAT64)
- 0.06% null values
- Range: 0.0071 to 9.1109
- 13,598 unique values

**pct_change_6mo** (FLOAT64)
- 43.80% null values
- Range: -67.33% to +492.76%
- 4,476 unique values

### 3-Month Metrics

**high_3mo** (FLOAT64)
- 25.47% null values
- Range: $52.35 to $696.09
- 2,586 unique values

**low_3mo** (FLOAT64)
- 25.47% null values
- Range: $51.77 to $650.85
- 2,003 unique values

**std_diff_3mo** (FLOAT64)
- 0.06% null values
- Range: 0.0071 to 11.42 (highest std_diff value)
- 13,670 unique values

**pct_change_3mo** (FLOAT64)
- 23.26% null values
- Range: -66.0% to +572.82%
- 4,503 unique values

### 1-Month Metrics

**high_1mo** (FLOAT64)
- 26.18% null values
- Range: $52.35 to $696.09
- 3,528 unique values

**low_1mo** (FLOAT64)
- 26.18% null values
- Range: $51.77 to $676.57
- 2,741 unique values

**std_diff_1mo** (FLOAT64)
- 0.06% null values
- Range: 0.0071 to 17.7022 (highest std_diff across all periods)
- 13,933 unique values (most unique among std_diff metrics)

**pct_change_1mo** (FLOAT64)
- 42.20% null values
- Range: -57.04% to +397.17%
- 3,172 unique values

## Potential Query Considerations

### Filtering Recommendations

**Strong Filter Columns:**
- `symbol`: Perfect for filtering by specific securities (5 distinct values, no nulls)
- `exchange`: Good for exchange-level analysis (3 distinct values, no nulls)
- `date`: Essential for time-based queries (date ranges, specific periods)
- `current_price`: Reliable for price-based filtering (no nulls)

**Caution with Filtering:**
- Percentage change columns have 23-47% nulls - use with NULL handling
- High/low metrics have 22-27% nulls - may exclude significant data
- Always consider NULL values when using WHERE clauses on these columns

### Grouping/Aggregation Recommendations

**Primary Grouping Columns:**
- `symbol`: Group by security for comparative analysis
- `exchange`: Less useful due to limited variation
- `date` (by year/month/quarter): Excellent for temporal aggregations

**Aggregation Targets:**
- `current_price`, `current_volume`: Clean aggregation candidates
- `std_diff_*`: Volatility analysis across time periods
- `pct_change_*`: Performance analysis (use COUNT/AVG with NULL awareness)

### Join Key Potential

**Primary Keys:**
- Composite key: (`symbol`, `date`) - likely unique identifier
- `symbol` alone: Can join to other symbol-reference tables
- `exchange` + `symbol`: Alternative join strategy

**Relationship Indicators:**
- Single symbol appears across multiple dates (time-series structure)
- Exchange-symbol relationship is stable (each symbol trades on one exchange)

### Data Quality Considerations

**For Accurate Queries:**

1. **NULL Handling Critical:** Many analytical columns have significant nulls
   - Use `COALESCE()` or `IFNULL()` for default values
   - Consider `WHERE column IS NOT NULL` to exclude incomplete records
   - Document assumptions when excluding nulls

2. **Volume = 0 Cases:** Investigate whether these represent:
   - Non-trading days (holidays, weekends)
   - Index values (VIX.INDX has no volume)
   - Data collection gaps

3. **Percentage Change Patterns:** Higher null rates for longer periods suggest:
   - Edge cases at dataset start/end dates
   - Queries spanning multiple time periods should account for decreasing sample sizes

4. **Standard Deviation Reliability:** Near-complete coverage (~99.94%) makes std_diff metrics highly reliable for volatility analysis

5. **Price Range Validation:** Extreme values (VIX: $9-$80+ range vs SPY: $100-$400+) require symbol-aware analysis

## Keywords

Market indices, ETF analysis, S&P 500 (SPY), Dow Jones (DIA), NASDAQ (QQQ), Russell 2000 (IWM), VIX volatility index, stock prices, trading volume, technical indicators, price volatility, percentage returns, high-low ranges, time series financial data, NYSE Arca (ARCX), NASDAQ exchange (XNAS), 52-week highs/lows, standard deviation, market performance metrics, historical stock data, intraday trading, financial analytics, securities analysis

## Table and Column Documentation

**Table Comment:** Not provided in the analysis report.

**Column Comments:** No column-level comments were provided in the analysis report. The column names are self-descriptive, following a consistent pattern:
- Base metrics: `current_*` for intraday values
- Time-period metrics: `*_1yr`, `*_9mo`, `*_6mo`, `*_3mo`, `*_1mo` for rolling window calculations
- Metric types: `high`, `low`, `std_diff`, `pct_change` consistently applied across time periods