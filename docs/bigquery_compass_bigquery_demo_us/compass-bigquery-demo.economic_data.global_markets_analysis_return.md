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
# Data Summary: Global Markets Analysis Return Table

## Overall Dataset Characteristics

**Total Rows:** 2,197

**Data Quality:** The dataset exhibits high quality for operational columns with 0% null values across all primary fields. However, there are two distinct column groups:
- **Active columns** (26 columns): Complete data with no nulls, representing historical market performance metrics
- **Inactive columns** (20 columns): 100% null values, likely placeholders for future data or deprecated fields

**Time Range:** Data spans from 2012 to 2026 (15 years), with monthly granularity organized into 169 unique month periods and 57 quarters.

**Geographic Coverage:** The dataset tracks 13 global market ETF symbols representing various international markets and emerging economies.

**Table Comment:** Not provided.

---

## Column Details

### Dimension Columns

#### **exchange** (STRING)
- **Purpose:** Trading exchange identifier
- **Values:** Only 2 exchanges - ARCX (NYSE Arca) and XNAS (NASDAQ)
- **Quality:** Complete (0% null)
- **Usage:** Filter by exchange, useful for exchange-specific analysis

#### **symbol** (STRING)
- **Purpose:** ETF ticker symbol
- **Values:** 13 unique symbols including ACWI (global), EEM (emerging markets), country-specific ETFs (EWA, EWG, EWJ, EWQ, EWU, EWW, EWY, EPI)
- **Quality:** Complete (0% null)
- **Usage:** Primary dimension for ETF-specific queries, join key for ETF reference data

#### **year_month** (STRING)
- **Purpose:** Period identifier in YYYY-MM format
- **Values:** 169 unique months from 2012-06 to 2025-06
- **Quality:** Complete (0% null)
- **Usage:** Time-based filtering and grouping at monthly level

#### **month_date** (DATE)
- **Purpose:** First day of the month representation
- **Values:** 169 unique dates
- **Quality:** Complete (0% null)
- **Usage:** Date-based filtering, time series analysis, preferred for date range queries

#### **year_quarter** (STRING)
- **Purpose:** Quarter identifier in YYYY-QX format
- **Values:** 57 unique quarters from 2012-Q1 through 2025+
- **Quality:** Complete (0% null)
- **Usage:** Quarterly aggregation and filtering

#### **quarter_num** (INT64)
- **Purpose:** Quarter number within year
- **Range:** 1 to 4
- **Quality:** Complete (0% null)
- **Usage:** Seasonal analysis, quarter-based filtering

#### **year_val** (INT64)
- **Purpose:** Year as integer
- **Range:** 2012 to 2026 (15 unique years)
- **Quality:** Complete (0% null)
- **Usage:** Year-over-year comparisons, annual aggregations

---

### Monthly Metrics (Complete Data)

#### **monthly_avg_close** (FLOAT64)
- **Range:** $8.99 to $142.49
- **Uniqueness:** 2,185 unique values (high variability)
- **Quality:** Complete (0% null)
- **Usage:** Primary price metric for monthly performance analysis

#### **monthly_avg_open** (FLOAT64)
- **Range:** $8.99 to $142.77
- **Quality:** Complete (0% null)
- **Usage:** Opening price analysis, gap analysis

#### **monthly_avg_high** (FLOAT64)
- **Range:** $9.03 to $142.95
- **Quality:** Complete (0% null)
- **Usage:** High price analysis, volatility metrics

#### **monthly_avg_low** (FLOAT64)
- **Range:** $8.94 to $141.49
- **Quality:** Complete (0% null)
- **Usage:** Low price analysis, support levels

#### **monthly_avg_volume** (FLOAT64)
- **Range:** 93,155 to 112,784,014 shares
- **High Variability:** 2,197 unique values (all unique)
- **Quality:** Complete (0% null)
- **Usage:** Liquidity analysis, trading activity patterns

---

### Quarterly Aggregated Metrics (Complete Data)

#### **quarterly_avg_close** (FLOAT64)
- **Range:** $9.17 to $142.49
- **Uniqueness:** 740 unique values
- **Quality:** Complete (0% null)
- **Usage:** Quarterly performance benchmarking

#### **quarterly_avg_open** (FLOAT64)
- **Range:** $9.17 to $142.77
- **Uniqueness:** 741 unique values
- **Quality:** Complete (0% null)
- **Usage:** Quarterly opening analysis

#### **quarterly_avg_high** (FLOAT64)
- **Range:** $9.21 to $142.95
- **Uniqueness:** 740 unique values
- **Quality:** Complete (0% null)
- **Usage:** Quarterly peak analysis

#### **quarterly_avg_low** (FLOAT64)
- **Range:** $9.14 to $141.49
- **Uniqueness:** 741 unique values
- **Quality:** Complete (0% null)
- **Usage:** Quarterly trough analysis

#### **quarterly_avg_volume** (FLOAT64)
- **Range:** 137,927 to 96,886,293 shares
- **Uniqueness:** 741 unique values
- **Quality:** Complete (0% null)
- **Usage:** Quarterly liquidity trends

---

### Forward-Looking Performance Metrics

#### **pct_change_q1_forward** (FLOAT64)
- **Purpose:** Percentage change one quarter ahead
- **Range:** -32.92% to +188.32%
- **Null Percentage:** 2.37% (52 rows)
- **Uniqueness:** 624 unique values
- **Usage:** Next quarter performance prediction, forward returns analysis
- **Note:** Nulls likely represent most recent data where future quarter is unknown

#### **pct_change_q2_forward** (FLOAT64)
- **Purpose:** Percentage change two quarters ahead
- **Range:** -40.39% to +320.35%
- **Null Percentage:** 4.14% (91 rows)
- **Uniqueness:** 645 unique values
- **Usage:** 6-month forward returns analysis

#### **pct_change_q3_forward** (FLOAT64)
- **Purpose:** Percentage change three quarters ahead
- **Range:** -39.40% to +339.59%
- **Null Percentage:** 5.92% (130 rows)
- **Uniqueness:** 649 unique values
- **Usage:** 9-month forward returns analysis

#### **pct_change_q4_forward** (FLOAT64)
- **Purpose:** Percentage change four quarters ahead
- **Range:** -46.23% to +354.65%
- **Null Percentage:** 7.69% (169 rows)
- **Uniqueness:** 638 unique values
- **Usage:** 12-month (annual) forward returns analysis
- **Note:** Increasing null percentages in forward metrics indicate data recency constraints

---

### Inactive/Placeholder Columns (100% Null)

The following 20 columns contain no data and should be excluded from queries:

**Current Snapshot Metrics:**
- `date`, `current_price`, `current_high`, `current_low`, `current_volume`

**Historical Lookback Metrics (1-year):**
- `high_1yr`, `low_1yr`, `std_diff_1yr`, `pct_change_1yr`

**Historical Lookback Metrics (9-month):**
- `high_9mo`, `low_9mo`, `std_diff_9mo`, `pct_change_9mo`

**Historical Lookback Metrics (6-month):**
- `high_6mo`, `low_6mo`, `std_diff_6mo`, `pct_change_6mo`

**Historical Lookback Metrics (3-month):**
- `high_3mo`, `low_3mo`, `std_diff_3mo`, `pct_change_3mo`

**Historical Lookback Metrics (1-month):**
- `high_1mo`, `low_1mo`, `std_diff_1mo`, `pct_change_1mo`

---

## Query Considerations

### Optimal Filtering Columns
1. **symbol**: Primary filter for specific ETF analysis (13 values)
2. **exchange**: Exchange-specific queries (2 values)
3. **year_val**: Annual filtering and comparisons (2012-2026)
4. **year_quarter**: Quarterly analysis
5. **quarter_num**: Seasonal pattern analysis (1-4)
6. **month_date** or **year_month**: Time range filtering

### Optimal Grouping/Aggregation Columns
1. **symbol**: ETF-level aggregations
2. **year_val**: Annual trends
3. **year_quarter**: Quarterly trends
4. **quarter_num**: Cross-year seasonal patterns
5. **exchange**: Exchange-level comparisons

### Join Keys
- **symbol**: Join to ETF reference data (country, sector, asset class)
- **month_date** or **year_month**: Join to economic indicators, market indices
- **year_quarter**: Join to quarterly economic data

### Data Quality Considerations for Queries

1. **Forward Return Nulls**: Queries using `pct_change_qX_forward` columns should:
   - Filter out nulls or use `COALESCE` for aggregations
   - Understand that nulls increase with longer forward periods (2.37% → 7.69%)
   - Most recent periods will have incomplete forward returns

2. **Avoid Null Columns**: Explicitly exclude the 20 columns with 100% nulls

3. **Price Range Awareness**: Wide price ranges ($8.99 to $142.49) suggest different ETF price points; percentage-based comparisons more appropriate than absolute price comparisons

4. **Volume Variability**: Extremely wide volume ranges (93K to 112M) indicate different ETF liquidity profiles; volume metrics should be analyzed relative to each symbol's baseline

5. **Time Period Coverage**: While data spans 2012-2026, verify actual date ranges per symbol as not all symbols may have complete coverage

6. **Forward Returns Distribution**: Extreme positive returns (up to +354%) suggest some high-volatility periods or emerging market exposures; consider outlier handling in statistical analyses

---

## Keywords

Global markets, ETF analysis, international equities, market returns, forward returns, quarterly performance, monthly averages, trading volume, OHLC data, emerging markets, country ETFs, ACWI, EEM, stock exchange data, NASDAQ, NYSE Arca, time series analysis, percentage change, market forecasting, investment returns, quarterly metrics, monthly metrics, market volatility, trading activity, price performance, global equity funds, iShares, regional ETFs, Asia Pacific markets, European markets, Latin American markets, market aggregations, financial returns

---

## Table and Column Documentation

**Table Comment:** Not provided

**Column Comments:** Not provided for any columns