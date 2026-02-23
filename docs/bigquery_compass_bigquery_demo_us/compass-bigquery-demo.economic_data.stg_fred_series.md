---
columns:
- category (STRING)
- date (DATE)
- literal (FLOAT64)
- series_code (STRING)
- series_name (STRING)
- value (STRING)
schema_hash: cdac078c5d8da5a74e15a9d6046e1e0825106070556c8542b624e3494a5cad2b

---
# Comprehensive Data Summary: compass-bigquery-demo.economic_data.stg_fred_series

## Overall Dataset Characteristics

### Dataset Size and Quality
- **Total Rows**: 244,721 records
- **Data Source**: Federal Reserve Economic Data (FRED) series staging table
- **General Quality**: High-quality structured economic time series data with minimal null values (only 2.76% in the `literal` column)
- **Time Coverage**: Extensive temporal coverage with 26,688 unique dates spanning multiple economic indicators

### Notable Patterns
- **Multi-Series Structure**: Contains 136 different economic series (indicators) tracked over time
- **Categorical Organization**: Data is organized into 2 main categories (Growth and Inflation)
- **High Granularity**: Each series contains multiple observations over time, resulting in a high row count despite relatively few unique series
- **Data Redundancy**: Both string (`value`) and numeric (`literal`) representations of values are maintained

## Column-Level Details

### 1. date (DATE)
- **Type**: DATE
- **Completeness**: 100% populated (0% null)
- **Unique Values**: 26,688 distinct dates
- **Purpose**: Time dimension for economic time series data
- **Pattern**: Represents observation dates for economic indicators
- **Query Consideration**: Primary temporal filtering column; ideal for time-based analysis and trending

### 2. series_code (STRING)
- **Type**: STRING
- **Completeness**: 100% populated (0% null)
- **Unique Values**: 136 distinct series codes
- **Examples**: 
  - `FEDFUNDS` (Federal Funds Rate)
  - `T5YIE` (Treasury Inflation Expectations)
  - `VIXCLS` (VIX Volatility Index)
  - `A191RL1Q225SBEA`, `AAA10Y`, `BAA10Y`, `CAPUTLG2211S`
- **Purpose**: Official FRED series identifier codes
- **Pattern**: Alphanumeric codes following FRED naming conventions
- **Query Consideration**: Primary key component; essential for filtering specific economic indicators

### 3. value (STRING)
- **Type**: STRING
- **Completeness**: 100% populated (0% null)
- **Unique Values**: 72,982 distinct string values
- **Purpose**: String representation of economic values
- **Pattern**: Text format of numeric data (may include special characters or non-numeric indicators)
- **Query Consideration**: Use for display purposes; prefer `literal` column for numeric calculations

### 4. literal (FLOAT64)
- **Type**: FLOAT64
- **Completeness**: 97.24% populated (2.76% null)
- **Unique Values**: 68,839 distinct numeric values
- **Range**: -136,419.0 to 110,982,661,180,013.0
- **Purpose**: Numeric representation of economic values for calculations
- **Pattern**: 
  - Includes negative values (indicating declines, deficits, etc.)
  - Extremely wide range suggests different units/scales across series
  - Nulls may represent missing observations or non-reportable periods
- **Query Consideration**: Primary column for aggregations, calculations, and numeric filtering; handle nulls appropriately

### 5. series_name (STRING)
- **Type**: STRING
- **Completeness**: 100% populated (0% null)
- **Unique Values**: 134 distinct series names
- **Examples**:
  - "Federal Funds Effective Rate"
  - "10-Year Treasury Constant Maturity Rate"
  - "Consumer Price Index for All Urban Consumers"
  - "ICE BofA US Corporate Index Option-Adjusted Spread"
  - "10-Year Treasury Constant Maturity Minus 2-Year Treasury Constant Maturity"
- **Purpose**: Human-readable description of economic indicators
- **Pattern**: Descriptive names including measurement units and geographical scope
- **Query Consideration**: Use for display, reporting, and user-friendly filtering; may contain search keywords

### 6. category (STRING)
- **Type**: STRING
- **Completeness**: 100% populated (0% null)
- **Unique Values**: 2 categories
- **Values**: "Growth" and "Inflation"
- **Purpose**: High-level classification of economic indicators
- **Pattern**: Binary categorization of all economic series
- **Query Consideration**: Primary grouping/filtering dimension for categorical analysis

## Potential Query Considerations

### Optimal Filtering Columns
1. **series_code**: For specific indicator selection (e.g., `WHERE series_code = 'FEDFUNDS'`)
2. **category**: For broad economic category filtering (Growth vs. Inflation metrics)
3. **date**: For temporal filtering (date ranges, specific periods)
4. **series_name**: For text-based searches of indicator descriptions

### Optimal Grouping/Aggregation Columns
1. **series_code** + **series_name**: Group by specific indicators
2. **category**: High-level categorical aggregations
3. **date**: Time-based aggregations (monthly, quarterly, yearly trends)
4. **Temporal grouping**: Use date functions for period-based analysis (YEAR(date), QUARTER(date), etc.)

### Potential Join Keys
- **series_code**: Primary key for joining with FRED metadata tables
- **date** + **series_code**: Composite key for time-series joins
- **category**: For joining with category definition tables

### Data Quality Considerations

1. **NULL Handling**: 
   - 2.76% nulls in `literal` column require NULL-safe operations
   - Use COALESCE or NULL checks in calculations
   - Nulls may indicate data not available for specific date/series combinations

2. **Scale Variations**:
   - Extreme range in `literal` values (-136K to 110 trillion) indicates different measurement units
   - Consider normalization or percentage changes for cross-series comparisons
   - Be cautious with aggregations across different series

3. **String vs. Numeric Values**:
   - Maintain awareness of `value` (STRING) vs. `literal` (FLOAT64)
   - Always use `literal` for mathematical operations
   - `value` may contain non-numeric indicators (e.g., "N/A", "Not Available")

4. **Time Series Continuity**:
   - Check for gaps in date sequences for specific series
   - Not all series may have observations for all dates
   - Consider using date dimension tables for complete time coverage

5. **Code vs. Name Mismatch**:
   - 136 unique codes vs. 134 unique names suggests potential duplicate naming
   - Always use `series_code` as the unique identifier

## Keywords

economic data, FRED, Federal Reserve, time series, economic indicators, interest rates, inflation, GDP, unemployment, treasury rates, mortgage rates, federal funds rate, CPI, consumer price index, economic growth, monetary policy, financial data, macroeconomic indicators, Treasury yields, corporate spreads, volatility index, VIX, breakeven inflation, economic statistics, financial metrics, date series, temporal analysis, inflation measures, growth indicators

## Table and Column Documentation

**Table Comment**: Not provided in the analysis report.

**Column Comments**: No column-level comments were provided in the analysis report. The column names are self-descriptive, following standard economic data conventions where:
- `date`: Observation date
- `series_code`: FRED official series identifier
- `value`: String representation of the measurement
- `literal`: Numeric representation of the measurement
- `series_name`: Full descriptive name of the economic indicator
- `category`: Economic classification (Growth or Inflation)