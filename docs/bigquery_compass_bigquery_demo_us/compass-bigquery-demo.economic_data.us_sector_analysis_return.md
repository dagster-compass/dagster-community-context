---
columns:
- exchange (STRING)
- month_date (DATE)
- monthly_avg_close (FLOAT64)
- monthly_avg_high (FLOAT64)
- monthly_avg_low (FLOAT64)
- monthly_avg_open (FLOAT64)
- monthly_avg_volume (FLOAT64)
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
- symbol (STRING)
- year_month (STRING)
- year_quarter (STRING)
- year_val (INT64)
schema_hash: ca13aab0a3e34c6baa11c8cbd6bdf61ed004c023101b0570d9cbd2c31d7bdf9d

---
# Table Summary: US Sector Analysis Return

## Overall Dataset Characteristics

This table contains **1,343 rows** of financial market data tracking US sector ETF performance over time. The dataset spans from **2012 to 2025** (14 years) and covers **11 sector ETFs** traded on the ARCX exchange. 

**Data Quality:** Excellent overall quality with 0% null values for core columns. Forward-looking percentage change columns show increasing null percentages (2.46% to 9.83%) which is expected for more distant future quarters, particularly for recent data where future quarters haven't occurred yet.

**Key Patterns:**
- Monthly granularity with 168 unique months across ~14 years
- Each sector ETF has consistent time-series coverage
- Quarterly aggregations and forward-looking returns are pre-calculated
- Volume ranges significantly from ~2.5M to ~93M, suggesting varying liquidity across sectors and time periods

## Column Details

### Temporal Columns

**year_month** (STRING)
- Primary time identifier in YYYY-MM format
- 168 unique values representing complete monthly coverage
- No null values, consistent formatting
- Useful for time-based filtering and ordering

**month_date** (DATE)
- Date representation of the first day of each month
- 168 unique values matching year_month
- Enables proper date-based calculations and filtering

**year_quarter** (STRING)
- Formatted as YYYY-Q# (e.g., "2019-Q2")
- 56 unique quarters spanning the dataset period
- Useful for quarterly aggregations and grouping

**year_val** (INT64)
- Integer year values from 2012 to 2025
- 14 unique years
- Ideal for year-over-year comparisons

**quarter_num** (INT64)
- Quarter number within year (1-4)
- Useful for seasonal analysis and quarter-based filtering

### Security Identifiers

**symbol** (STRING)
- 11 unique sector ETF symbols
- Values: XLB (Materials), XLC (Communication), XLE (Energy), XLF (Financials), XLI (Industrials), XLK (Technology), XLP (Consumer Staples), XLRE (Real Estate), XLU (Utilities), XLV (Healthcare)
- No null values - essential join/filter key

**exchange** (STRING)
- Single value: "ARCX" (NYSE Arca)
- Indicates all ETFs trade on the same exchange
- Not useful for filtering but provides context

### Monthly Price Metrics

**monthly_avg_close** (FLOAT64)
- Range: $23.73 to $289.54
- 1,342 unique values (nearly one per row)
- Average closing price for the month
- Key metric for price trend analysis

**monthly_avg_open** (FLOAT64)
- Range: $23.74 to $289.94
- Similar distribution to close prices
- Useful for gap analysis and intraday movement

**monthly_avg_high** (FLOAT64)
- Range: $23.93 to $291.74
- Represents average high prices during the month
- Useful for volatility and range analysis

**monthly_avg_low** (FLOAT64)
- Range: $23.49 to $287.35
- Represents average low prices during the month
- Combined with high for range calculations

**monthly_avg_volume** (FLOAT64)
- Range: 2.5M to 93.2M shares
- 1,343 unique values (one per row)
- Significant variation suggests differing sector popularity
- Important for liquidity analysis

### Quarterly Aggregated Metrics

**quarterly_avg_close** (FLOAT64)
- Range: $24.06 to $264.96
- 451 unique values
- Pre-aggregated quarterly average closing prices
- Useful for smoothed trend analysis

**quarterly_avg_open/high/low** (FLOAT64)
- Similar ranges and patterns to quarterly_avg_close
- 450-451 unique values
- Pre-calculated quarterly aggregations

**quarterly_avg_volume** (FLOAT64)
- Range: 2.9M to 93.2M
- 451 unique values
- Quarterly averaged trading volumes

### Forward-Looking Performance Metrics

**pct_change_q1_forward** (FLOAT64)
- **Null Percentage: 2.46%** (33 rows)
- Range: -22.34% to +32.94%
- Percentage change to the next quarter
- Most recent data naturally has nulls

**pct_change_q2_forward** (FLOAT64)
- **Null Percentage: 4.91%** (66 rows)
- Range: -37.42% to +50.80%
- Two-quarter forward return

**pct_change_q3_forward** (FLOAT64)
- **Null Percentage: 7.37%** (99 rows)
- Range: -40.22% to +61.82%
- Three-quarter forward return

**pct_change_q4_forward** (FLOAT64)
- **Null Percentage: 9.83%** (132 rows)
- Range: -41.97% to +64.03%
- Four-quarter (one-year) forward return

## Query Considerations

### Ideal Filtering Columns
- **symbol**: Filter by specific sector ETFs
- **year_val**: Year-based filtering for trend analysis
- **year_quarter**: Quarterly time period filtering
- **quarter_num**: Seasonal pattern analysis (Q1 vs Q4 performance)
- **month_date**: Precise date range filtering

### Ideal Grouping/Aggregation Columns
- **symbol**: Compare performance across sectors
- **year_val**: Annual performance comparisons
- **year_quarter**: Quarterly trends
- **quarter_num**: Seasonal pattern identification

### Potential Join Keys
- **symbol**: Join with other ETF/security tables
- **year_month** or **month_date**: Join with economic indicators or market data
- **year_quarter**: Join with quarterly financial data

### Data Quality Considerations
1. **Forward-looking nulls**: Queries using pct_change columns should handle nulls appropriately or filter to complete periods
2. **Time series completeness**: Verify continuous monthly coverage when analyzing trends
3. **Volume variations**: Wide range suggests some periods/sectors may have thin trading
4. **Price normalization**: Prices vary significantly across sectors; percentage returns are more comparable than absolute prices
5. **Recent data**: 2025 data appears to be present (possibly projected), verify data currency for analysis

### Recommended Query Patterns
- Time-series analysis with ORDER BY month_date
- Sector comparison using GROUP BY symbol
- Seasonal analysis using quarter_num
- Forward return prediction using historical pct_change columns
- Volatility analysis using (high - low) calculations
- Volume-weighted analyses for liquidity considerations

## Keywords

US sector ETFs, SPDR sectors, XLB, XLC, XLE, XLF, XLI, XLK, XLP, XLRE, XLU, XLV, sector rotation, monthly returns, quarterly returns, forward returns, stock market performance, sector analysis, NYSE Arca, ARCX, time series financial data, ETF performance, trading volume, price momentum, quarterly forecasting, sector trends, materials sector, communication sector, energy sector, financial sector, industrial sector, technology sector, consumer staples, real estate sector, utilities sector, healthcare sector

## Table and Column Documentation

**Table Comment:** Not provided in the analysis report.

**Column Comments:** Not provided in the analysis report.