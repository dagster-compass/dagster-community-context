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
# Table Summary: currency_analysis_return

## Overall Dataset Characteristics

**Total Rows:** 1,112

**General Description:** This table contains monthly and quarterly aggregated financial data for currency-related ETFs and financial instruments, spanning from 2012 to 2025 (approximately 14 years). The dataset tracks 8 different currency symbols across 3 exchanges, with 168 unique monthly observations.

**Data Quality:** The dataset demonstrates excellent data quality with zero null values in all primary fields. However, the forward-looking percentage change columns (`pct_change_q1_forward` through `pct_change_q4_forward`) contain some null values (2.25% to 8.72%), likely representing recent periods where future data is not yet available.

**Notable Patterns:**
- Complete time series data with no gaps in temporal fields
- Multiple aggregation levels: monthly and quarterly metrics
- Forward-looking predictive features with increasing null percentages (indicating recency)
- Wide range of values in volume data suggesting different liquidity profiles across instruments

## Column Details

### Temporal Columns

**month_date (DATE)**
- Primary date field with no nulls
- 168 unique monthly observations
- Covers period from 2012 to 2025
- Key field for time-based filtering and analysis

**year_month (STRING)**
- String representation of year-month (e.g., "2024-07")
- 168 unique values matching month_date
- Useful for string-based date operations

**year_quarter (STRING)**
- Quarterly period identifier (e.g., "2024-Q3")
- 56 unique quarters
- Format: YYYY-Q#

**quarter_num (INT64)**
- Quarter number within year (1-4)
- Complete coverage of all quarters
- Useful for seasonal analysis

**year_val (INT64)**
- Year as integer (2012-2025)
- 14 unique years
- Supports year-over-year comparisons

### Identifier Columns

**symbol (STRING)**
- 8 unique currency/financial instruments
- Values: CEW, ETHE, FXA, FXB, FXC, FXE, FXY, IBIT.INDX
- No nulls, indicating complete symbol coverage
- Primary grouping key for instrument-level analysis

**exchange (STRING)**
- 3 exchanges: ARCX, INDX, OTCM
- No nulls
- ARCX appears to be the most common (sample data suggests ETF listings)

### Monthly Aggregated Price Metrics

**monthly_avg_close (FLOAT64)**
- Range: 5.72 to 171.27
- 1,110 unique values (high granularity)
- No nulls
- Primary price indicator for monthly performance

**monthly_avg_open (FLOAT64)**
- Range: 5.80 to 210.90
- 1,111 unique values
- Notable: Maximum open (210.90) significantly higher than max close (171.27)

**monthly_avg_high (FLOAT64)**
- Range: 5.91 to 261.45
- 1,110 unique values
- Expected higher maximum than close prices

**monthly_avg_low (FLOAT64)**
- Range: 5.59 to 167.79
- 1,111 unique values
- Expected lower values than close prices

**monthly_avg_volume (FLOAT64)**
- Range: 1.0 to 75,840,296
- 1,108 unique values
- Extremely wide range indicating vastly different liquidity levels
- Critical for understanding trading activity

### Quarterly Aggregated Price Metrics

**quarterly_avg_close (FLOAT64)**
- Range: 7.46 to 171.27
- 372 unique values
- Higher-level aggregation of monthly closes

**quarterly_avg_open (FLOAT64)**
- Range: 7.42 to 210.90
- 372 unique values

**quarterly_avg_high (FLOAT64)**
- Range: 7.71 to 261.45
- 372 unique values

**quarterly_avg_low (FLOAT64)**
- Range: 7.18 to 165.56
- 372 unique values

**quarterly_avg_volume (FLOAT64)**
- Range: 1.0 to 66,568,938
- 372 unique values
- Quarterly aggregation of trading volume

### Forward-Looking Performance Metrics

**pct_change_q1_forward (FLOAT64)**
- Null Percentage: 2.25%
- Range: -75.36% to 125.22%
- 313 unique values
- Represents percentage change one quarter forward

**pct_change_q2_forward (FLOAT64)**
- Null Percentage: 4.41%
- Range: -81.87% to 285.32%
- 327 unique values
- Two quarters forward performance
- Notable extreme values (285.32% gain possible)

**pct_change_q3_forward (FLOAT64)**
- Null Percentage: 6.56%
- Range: -86.16% to 169.62%
- 333 unique values
- Three quarters forward performance

**pct_change_q4_forward (FLOAT64)**
- Null Percentage: 8.72%
- Range: -80.40% to 222.00%
- 320 unique values
- Four quarters (one year) forward performance

## Potential Query Considerations

### Good Filtering Columns:
- **symbol**: For instrument-specific analysis (8 discrete values)
- **exchange**: For exchange-level comparisons (3 values)
- **year_val**: For year-based filtering and trending
- **quarter_num**: For seasonal pattern analysis
- **month_date / year_month**: For date range queries

### Good Grouping/Aggregation Columns:
- **symbol**: Primary grouping for performance comparisons
- **exchange**: Exchange-level aggregations
- **year_val**: Year-over-year analysis
- **quarter_num**: Seasonal analysis
- **year_quarter**: Quarterly performance tracking

### Potential Join Keys:
- **symbol**: Could join to reference tables with instrument metadata
- **exchange**: Could join to exchange reference data
- **month_date / year_month**: Time-series joins to economic indicators or other market data

### Data Quality Considerations:

1. **Forward-looking metrics**: Increasing null percentages indicate recent data where future outcomes aren't yet known. Queries should handle nulls appropriately or filter to complete records.

2. **Volume variability**: The extreme range (1 to 75+ million) suggests using logarithmic scales or filtering outliers for meaningful comparisons.

3. **Price ranges**: Different instruments have vastly different price scales (5.72 to 261.45), requiring percentage-based comparisons rather than absolute values.

4. **Temporal completeness**: No nulls in date fields suggests complete time series, but verify continuity for specific symbols if needed.

5. **Calculated fields**: Monthly and quarterly averages are pre-aggregated, eliminating need for complex averaging queries but requiring understanding of the underlying calculation period.

## Keywords

currency, ETF, exchange-traded funds, forex, FX, financial instruments, monthly returns, quarterly returns, price data, OHLC (open-high-low-close), volume, trading volume, time series, ARCX, forward returns, percentage change, performance metrics, FXA, FXB, FXC, FXE, FXY, CEW, ETHE, IBIT, seasonal analysis, market data, cryptocurrency, bitcoin, ethereum

## Table and Column Documentation

**Table Comment:** Not provided in the analysis report.

**Column Comments:** No column-level comments were provided in the analysis report. The column names are self-descriptive, following standard financial data conventions (avg_close, avg_open, avg_high, avg_low for OHLC data; pct_change for performance metrics; monthly/quarterly prefixes for aggregation levels).