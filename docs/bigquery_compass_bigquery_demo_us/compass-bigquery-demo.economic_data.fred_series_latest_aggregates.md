---
columns:
- current_value (FLOAT64)
- date_grain (STRING)
- month (DATE)
- pct_change_1y (FLOAT64)
- pct_change_3m (FLOAT64)
- pct_change_6m (FLOAT64)
- series_code (STRING)
- series_name (STRING)
schema_hash: 8097db757443d6e29cddccdf6045baaf6e9b3d955e1ff198652ddedbe4d02d5e

---
# Table Summary: fred_series_latest_aggregates

## Overall Dataset Characteristics

- **Total Rows**: 128
- **Data Quality**: Excellent - no null values across any columns (0% null percentage for all fields)
- **Dataset Nature**: This appears to be a FRED (Federal Reserve Economic Data) economic indicators table containing time series data with current values and percentage changes over different time periods
- **Temporal Coverage**: Data points span from April 2025 through December 2025, with one anomalous future date in October 2035
- **Notable Pattern**: The table contains 126 unique series names but 128 unique series codes, suggesting some series may have slight variations or multiple time grain representations

## Column Details

### month (DATE)
- **Type**: Date field representing the reference period
- **Coverage**: 9 distinct months, primarily concentrated in 2025 (Apr, Jun, Jul, Aug, Sep, Oct, Nov, Dec) plus Oct 2035
- **Pattern**: Monthly granularity for reporting periods
- **Note**: The 2035-10-01 date appears to be an outlier or potentially represents forward-looking projections
- **Query Use**: Primary temporal filtering and grouping column

### series_name (STRING)
- **Type**: Descriptive name for economic indicators
- **Uniqueness**: 126 unique values out of 128 rows (slight duplication)
- **Purpose**: Human-readable identifier for economic series
- **Query Use**: Good for text-based searches and filtering by specific economic indicators

### series_code (STRING)
- **Type**: Unique identifier/code for FRED series
- **Uniqueness**: 128 unique values (one per row)
- **Purpose**: Standard FRED series identifier (e.g., GDP, UNRATE, CPI codes)
- **Query Use**: Primary key candidate, ideal for joins with other FRED data tables

### current_value (FLOAT64)
- **Type**: Numeric measurement of the economic indicator
- **Range**: Extremely wide range from -52,828 to 212,166,000
- **Uniqueness**: 126 unique values
- **Scale Variation**: Values span multiple orders of magnitude, indicating different units/scales across series
- **Query Use**: Primary metric for analysis, aggregations, comparisons
- **Note**: Negative values present, which is normal for economic indicators (e.g., trade deficits, changes)

### date_grain (STRING)
- **Type**: Categorical field indicating data frequency
- **Values**: 4 distinct values - Daily, Monthly, Quarterly, Weekly
- **Purpose**: Indicates the native frequency/granularity of each time series
- **Query Use**: Important for filtering by data frequency or understanding update cycles

### pct_change_6m (FLOAT64)
- **Type**: Six-month percentage change
- **Range**: -9.58% to 2.23%
- **Uniqueness**: 34 unique values (significant overlap across series)
- **Pattern**: Relatively constrained range suggesting moderate short-term volatility
- **Query Use**: Trend analysis, identifying growth/decline patterns over half-year periods

### pct_change_1y (FLOAT64)
- **Type**: One-year percentage change
- **Range**: -1.4% to 718.4% (extreme range)
- **Uniqueness**: 35 unique values
- **Pattern**: The 718.4% outlier suggests some series experienced dramatic year-over-year changes
- **Sample Values**: Many values near 0.0-0.01%, indicating stability in some series
- **Query Use**: Year-over-year trend analysis, volatility detection

### pct_change_3m (FLOAT64)
- **Type**: Three-month percentage change
- **Range**: -2.64% to 6.55%
- **Uniqueness**: 34 unique values
- **Pattern**: More volatile than 6-month changes but less extreme than 1-year
- **Query Use**: Short-term trend analysis, quarterly performance tracking

## Query Considerations

### Excellent Filtering Columns:
- **month**: Temporal filtering for specific periods or date ranges
- **series_code**: Precise filtering for specific economic indicators
- **date_grain**: Filtering by data frequency requirements
- **series_name**: Text-based searches for indicator types

### Excellent Grouping/Aggregation Columns:
- **date_grain**: Group by data frequency type
- **month**: Time-based aggregations and trending
- Statistical aggregations on **current_value** and percentage change columns

### Potential Join Keys:
- **series_code**: Primary key for joining with other FRED tables or economic databases
- **month + series_code**: Composite key for time-series joins

### Data Quality Considerations:
1. **Scale Normalization**: Current values span vastly different scales - queries comparing values across series should normalize or use percentage changes
2. **Temporal Anomaly**: The 2035-10-01 date should be investigated or filtered out for historical analysis
3. **Percentage Change Interpretation**: The extreme 718.4% one-year change suggests some series may need special handling or represent cumulative/index values
4. **Missing Sample Rows**: The empty sample rows array suggests data access may be restricted or require special handling
5. **Date Grain Awareness**: Queries should account for different update frequencies when comparing series

### Recommended Query Patterns:
- Filter by recent months (2025 range) to avoid the 2035 outlier
- Use series_code for precise indicator selection
- Group by date_grain when comparing series with different update frequencies
- Use percentage change columns for normalized comparisons across different-scaled series
- Consider windowing functions for time-series analysis within series_code groups

## Keywords

FRED, Federal Reserve Economic Data, economic indicators, time series, GDP, unemployment, CPI, inflation, economic metrics, percentage change, monthly data, quarterly data, year-over-year, growth rates, economic trends, financial data, macroeconomic indicators, series codes, temporal analysis, economic aggregates

## Table and Column Documentation

**Table Comment**: Not provided in the analysis report.

**Column Comments**: Not provided in the analysis report.