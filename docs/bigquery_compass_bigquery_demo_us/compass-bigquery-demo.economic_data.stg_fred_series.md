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
# Table Summary: compass-bigquery-demo.economic_data.stg_fred_series

## Overall Dataset Characteristics

This table contains **243,969 rows** of economic time series data from the Federal Reserve Economic Data (FRED) system. The data represents various economic indicators tracked over time, with observations spanning multiple decades (earliest sample date: 1986-06-01, latest: 2024-08-01).

**Data Quality:**
- Excellent overall quality with 0% null values in most critical columns
- Only the `literal` column has nulls (2.74%), which is acceptable for numeric economic data
- High data completeness across all identifying and categorical fields

**Notable Patterns:**
- The dataset covers 136 distinct economic series
- Data is categorized into only 2 main economic categories: Growth and Inflation
- The `value` column is stored as STRING (likely to preserve precision and handle special values)
- The `literal` column provides the numeric float representation of values
- Wide range in literal values (-136,419 to 111+ trillion) suggests different scales/units across series

## Column Details

### date (DATE)
- **Type:** DATE format
- **Nulls:** 0% - fully populated
- **Cardinality:** 26,636 unique dates
- **Range:** 1986-06-01 to 2024-08-01 (38+ years of data)
- **Pattern:** Time series data with varying frequencies (daily, weekly, monthly, quarterly observations implied by unique date count)
- **Query Use:** Primary column for time-based filtering and time series analysis

### series_code (STRING)
- **Type:** STRING identifier
- **Nulls:** 0% - fully populated
- **Cardinality:** 136 unique codes
- **Examples:** A191RL1Q225SBEA, AAA10Y, BAA10Y, BAMLC0A0CM, BUSLOANS, CAPUTLG2211S
- **Pattern:** Alphanumeric codes following FRED naming conventions
- **Query Use:** Primary key for joining to series metadata; essential for filtering specific economic indicators

### series_name (STRING)
- **Type:** STRING description
- **Nulls:** 0% - fully populated
- **Cardinality:** 134 unique names (slightly less than codes, suggesting some codes may share names)
- **Examples:**
  - Interest rates: "10 year Treasury Rate", "30-Year Fixed Rate Mortgage Average"
  - Inflation metrics: "10-Year Breakeven Inflation Rate", "5-Year Breakeven Inflation Rate"
  - Yield curve indicators: "10-Year Treasury Constant Maturity Minus 2-Year Treasury Constant Maturity"
- **Query Use:** Human-readable labels for display; can be used for text-based filtering

### category (STRING)
- **Type:** STRING categorical
- **Nulls:** 0% - fully populated
- **Cardinality:** Only 2 values
- **Values:** "Growth", "Inflation"
- **Distribution:** Both categories well-represented based on samples
- **Query Use:** High-level filtering and grouping; useful for broad economic analysis

### value (STRING)
- **Type:** STRING representation of numeric values
- **Nulls:** 0% - fully populated
- **Cardinality:** 72,726 unique values
- **Examples:** "5.82", "7.26", "3.91"
- **Pattern:** Decimal numbers stored as strings (likely for precision preservation)
- **Query Use:** Display purposes; may need CAST to FLOAT64 for calculations, though `literal` column is preferred for numeric operations

### literal (FLOAT64)
- **Type:** FLOAT64 numeric
- **Nulls:** 2.74% - mostly populated
- **Cardinality:** 68,589 unique values
- **Range:** -136,419.0 to 111,252,997,846,886.0
- **Pattern:** Extreme range suggests different measurement units across series (percentages, basis points, absolute values, indices)
- **Query Use:** Primary column for numeric calculations, aggregations, and comparisons; nulls should be handled in calculations

## Potential Query Considerations

### Filtering Columns:
- **date**: Essential for time-range queries (e.g., WHERE date BETWEEN '2020-01-01' AND '2023-12-31')
- **series_code**: For specific indicator selection (e.g., WHERE series_code = 'AAA10Y')
- **category**: For broad economic category filtering (WHERE category = 'Inflation')
- **series_name**: For text-based searches (WHERE series_name LIKE '%Treasury%')

### Grouping/Aggregation Columns:
- **series_code** + **series_name**: Group by series for multi-series analysis
- **category**: High-level aggregation by economic category
- **date** (with DATE_TRUNC): Time-based aggregation (monthly, quarterly, yearly averages)

### Join Keys:
- **series_code**: Likely primary key for joining to series metadata tables
- Potential relationships with other economic data tables using series_code or date

### Data Quality Considerations:

1. **String vs Numeric Values:**
   - `value` is STRING but `literal` is FLOAT64
   - Queries should use `literal` for calculations
   - Handle 2.74% nulls in `literal` with COALESCE or NULL-safe operations

2. **Scale Differences:**
   - Values range from negative thousands to trillions
   - Different series have different units (percentages vs. absolute values)
   - Comparisons across series require understanding of units
   - Consider filtering by series_code before performing calculations

3. **Time Series Gaps:**
   - With 136 series and 26,636 dates, not all series have observations for all dates
   - Some series may have different frequencies (daily vs. monthly vs. quarterly)
   - Use LEFT JOINs or handle missing dates when comparing series

4. **Recommended Query Patterns:**
   ```sql
   -- Filter by specific series and date range
   WHERE series_code = 'AAA10Y' 
   AND date >= '2020-01-01'
   
   -- Use literal for calculations
   SELECT AVG(literal) FROM table WHERE literal IS NOT NULL
   
   -- Group by series for multi-series comparison
   GROUP BY series_code, series_name
   ```

## Keywords

economic data, FRED, Federal Reserve, time series, interest rates, inflation, treasury rates, GDP, economic indicators, financial data, macroeconomic data, yield curve, mortgage rates, breakeven inflation, economic growth, monthly data, quarterly data, market rates, bond yields, financial metrics, economic analysis, stagflation analysis

## Table and Column Documentation

**Table Comment:** Not provided

**Column Comments:**
- date: Not provided
- series_code: Not provided
- series_name: Not provided
- category: Not provided
- value: Not provided
- literal: Not provided

*Note: This table appears to be a staging table (prefix: stg_) for FRED economic data, likely part of a larger data warehouse or analytics pipeline. The lack of column comments suggests this may be an intermediate transformation layer.*