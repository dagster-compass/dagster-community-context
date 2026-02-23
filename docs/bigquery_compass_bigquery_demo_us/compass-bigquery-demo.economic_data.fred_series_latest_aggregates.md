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
# Comprehensive Table Summary: fred_series_latest_aggregates

## Overall Dataset Characteristics

### General Information
- **Total Rows**: 253 records
- **Dataset Type**: Economic time series data from Federal Reserve Economic Data (FRED)
- **Data Quality**: Excellent - minimal null values (only 0.40% in one column)
- **Time Range**: Data spans from April 2025 to February 2026 (11 distinct months)
- **Purpose**: Latest aggregated economic indicators with historical percentage changes

### Notable Patterns
- Contains a mix of economic indicators at different reporting frequencies (Daily, Weekly, Monthly, Quarterly)
- Multiple series may share the same reporting month but represent different economic measures
- The dataset appears to be a "latest snapshot" view of various economic series with their recent historical changes
- Values span an enormous range (from negative thousands to hundreds of millions), indicating diverse types of economic measurements (indices, rates, dollar amounts, percentages)

## Column Details

### series_name (STRING)
- **Purpose**: Human-readable name of the economic indicator
- **Data Quality**: 100% populated, no nulls
- **Unique Values**: 126 distinct series names
- **Pattern**: Descriptive names for well-known economic indicators
- **Examples**: 
  - "S&P 500" (stock market index)
  - "Consumer Price Index for All Urban Consumers: All Items Less Food and Energy" (inflation measure)
  - "U.S. / U.K. Foreign Exchange Rate" (currency exchange)
  - "Gross Domestic Product"
  - "Personal Income"
- **Query Consideration**: Ideal for human-readable filtering and display; use for user-facing queries

### series_code (STRING)
- **Purpose**: Official FRED series identifier/ticker symbol
- **Data Quality**: 100% populated, no nulls
- **Unique Values**: 128 distinct codes (slightly more than series names, suggesting some series may have multiple entries)
- **Format**: Standardized FRED ticker codes (e.g., "GDP", "DJIA", "BOPGSTB", "PERMIT", "TCU")
- **Query Consideration**: Primary identifier for joining with other FRED data sources; more reliable than series_name for programmatic queries

### month (DATE)
- **Purpose**: Reference month/period for the economic data point
- **Data Quality**: 100% populated, no nulls
- **Unique Values**: 11 distinct months
- **Range**: 2025-04-01 to 2026-02-01
- **Pattern**: All dates are set to the 1st of the month regardless of actual reporting frequency
- **Distribution**: Covers approximately 10 months of data
- **Query Consideration**: Primary temporal dimension for time-series analysis, filtering, and trending

### current_value (FLOAT64)
- **Purpose**: The actual value of the economic indicator for the given month
- **Data Quality**: 100% populated, no nulls
- **Unique Values**: 243 distinct values (high cardinality)
- **Range**: -56,825.0 to 212,166,000.0
- **Magnitude Variation**: Extreme range indicates diverse measurement types (percentages, indices, dollar amounts in millions/billions)
- **Examples**: 
  - Small values: -0.21, 6.1025 (likely rates or percentages)
  - Medium values: 159,626.0 (possibly indices or small dollar amounts)
  - Large values: 30,485.7285, 48,090.6731, 212,166,000.0 (GDP, market indices, large economic aggregates)
- **Query Consideration**: Use for aggregations, comparisons; be aware of scale differences when analyzing multiple series together

### pct_change_3m (FLOAT64)
- **Purpose**: Percentage change over 3-month period
- **Data Quality**: 100% populated, no nulls
- **Unique Values**: 50 distinct values
- **Range**: -2.64 to 7.41
- **Format**: Decimal representation (e.g., 0.05 = 5% increase, -0.15 = 15% decrease)
- **Query Consideration**: Useful for identifying short-term trends and volatility; good for filtering recent movers

### pct_change_6m (FLOAT64)
- **Purpose**: Percentage change over 6-month period
- **Data Quality**: 100% populated, no nulls
- **Unique Values**: 50 distinct values
- **Range**: -21.84 to 2.23
- **Pattern**: Generally smaller absolute values than 3m changes, showing more stable medium-term trends
- **Query Consideration**: Balance between short and long-term trend analysis

### pct_change_1y (FLOAT64)
- **Purpose**: Percentage change over 1-year period
- **Data Quality**: 99.60% populated (1 null value - only column with nulls)
- **Unique Values**: 51 distinct values
- **Range**: -1.4 to 812.6 (extreme outlier at 812.6 suggests potential data issue or extraordinary event)
- **Pattern**: Widest range of percentage changes; one null value suggests data may not be available for all series
- **Query Consideration**: Best for year-over-year comparisons; handle null gracefully; investigate extreme outliers

### date_grain (STRING)
- **Purpose**: Indicates the native reporting frequency of the economic series
- **Data Quality**: 100% populated, no nulls
- **Unique Values**: 4 distinct values
- **Possible Values**: Daily, Monthly, Quarterly, Weekly
- **Distribution**: Mix of reporting frequencies reflecting different data collection methodologies
- **Query Consideration**: Essential for understanding data freshness and appropriate aggregation periods; useful for filtering series by update frequency

## Potential Query Considerations

### Good Columns for Filtering
- **series_code**: Exact match queries for specific economic indicators
- **series_name**: Text search for finding relevant series (supports LIKE patterns)
- **month**: Time-based filtering (recent data, specific periods, date ranges)
- **date_grain**: Filter by reporting frequency (e.g., only daily updated series)
- **pct_change_* columns**: Filter for high/low performers or significant movers

### Good Columns for Grouping/Aggregation
- **date_grain**: Group to compare behavior across different reporting frequencies
- **month**: Time-series grouping for trend analysis
- **series_code/series_name**: Group to analyze multiple indicators together

### Potential Join Keys
- **series_code**: Primary key for joining with detailed FRED series data
- **month + series_code**: Composite key for time-series joins
- Could join with other FRED tables containing series metadata, historical values, or category information

### Data Quality Considerations
1. **Scale Variation**: The enormous range in `current_value` means queries should consider the type of economic indicator being analyzed
2. **Percentage Format**: The pct_change columns use decimal format (not multiplied by 100)
3. **Extreme Outlier**: The 812.6 value in pct_change_1y should be investigated or filtered
4. **Single Null**: The one null in pct_change_1y suggests new series or data availability issues
5. **Date Normalization**: All dates are normalized to the 1st of the month regardless of actual reporting date
6. **Duplicate Potential**: 128 series_codes vs 126 series_names suggests possible data duplication or variant series

### Recommended Query Patterns
- **Time-series trending**: ORDER BY month, filter by series_code
- **Cross-sectional analysis**: Compare multiple series for same month
- **Performance ranking**: Order by pct_change columns to find top/bottom movers
- **Frequency-based analysis**: Group by date_grain to understand reporting patterns
- **Value normalization**: Consider percentage changes rather than absolute values when comparing different series types

## Keywords
FRED, Federal Reserve, economic data, time series, economic indicators, GDP, inflation, CPI, employment, S&P 500, Dow Jones, DJIA, stock market, interest rates, exchange rates, percentage change, monthly data, quarterly data, daily data, economic aggregates, macroeconomic indicators, financial data, labor statistics, consumer prices, personal income, savings rate, job openings, JOLTS, economic trends, year-over-year, month-over-month, economic snapshot

## Table and Column Documentation
*No table comment or column comments were provided in the source data.*