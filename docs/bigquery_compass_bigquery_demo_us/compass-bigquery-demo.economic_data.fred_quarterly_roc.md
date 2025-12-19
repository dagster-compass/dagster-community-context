---
columns:
- avg_value (FLOAT64)
- data_source (STRING)
- month_date (TIMESTAMP)
- pct_change_period (FLOAT64)
- series_code (STRING)
- series_name (STRING)
- year_month (STRING)
schema_hash: e0a39e0dfbc771a6277d3878a4bd190773bfcb6e99464a4d416e39f97c078907

---
# Table Summary: FRED Quarterly Rate of Change Economic Data

## Overall Dataset Characteristics

This table contains **75,334 rows** of economic time series data from the Federal Reserve Economic Data (FRED) database, tracking various economic indicators and their rate of change over time. The data spans from 1913 to recent periods (approximately 1,396 unique months), covering **136 distinct economic series** across categories like interest rates, employment, prices, production, and more.

**Data Quality:** The dataset exhibits high quality with minimal null values (only 0.18% in `pct_change_period`). The data includes both actual reported values and interpolated values for periods with missing data. Some extreme values and infinite values in `pct_change_period` suggest significant economic events or data calculation artifacts.

**Notable Patterns:**
- Time series data organized by month with 136 different economic indicators tracked simultaneously
- Mix of actual and interpolated data sources
- Wide range of measurement scales (from small decimals to trillions)
- Presence of infinite values in percentage change suggests major economic disruptions or series transitions

## Column Details

### year_month (STRING)
- **Format:** YYYY-M pattern (e.g., "1913-1", "2020-12")
- **Nulls:** None (0.00%)
- **Coverage:** 1,396 unique months from 1913 to present
- **Purpose:** Primary time identifier in string format
- **Pattern:** Single-digit months (1-9) not zero-padded, double-digit months (10-12) as-is

### series_code (STRING)
- **Format:** Alphanumeric codes (e.g., "TB3MS", "CPIAUCNS", "INDPRO")
- **Nulls:** None (0.00%)
- **Values:** 136 unique FRED series identifiers
- **Examples:** 
  - Interest rates: TB3MS, AAA10Y, BAA10Y
  - Employment: USCONS
  - Prices: CPIAUCNS, WPU01
  - Production: INDPRO
- **Purpose:** Official FRED database series identifier for joining with external FRED data

### series_name (STRING)
- **Format:** Human-readable economic indicator descriptions
- **Nulls:** None (0.00%)
- **Values:** 134 unique names (slight consolidation from 136 codes)
- **Examples:**
  - "3-Month Treasury Constant Maturity Rate"
  - "Consumer Price Index for All Urban Consumers"
  - "Industrial Production Index"
  - "Labor Force Participation Rate"
- **Purpose:** Descriptive label for understanding what each series measures

### data_source (STRING)
- **Format:** Categorical with 2 values
- **Nulls:** None (0.00%)
- **Distribution:**
  - "Actual": Direct reported/measured data
  - "Interpolated": Gap-filled or estimated data
- **Purpose:** Data quality indicator showing whether values are observed or calculated

### month_date (TIMESTAMP)
- **Format:** UTC timestamp (first day of each month at 00:00:00)
- **Nulls:** None (0.00%)
- **Range:** 1913-01-01 to recent periods
- **Values:** 1,396 unique timestamps
- **Purpose:** Standardized date format for time-based queries and sorting

### avg_value (FLOAT64)
- **Format:** Decimal numbers with wide range
- **Nulls:** None (0.00%)
- **Range:** -136,419.0 to 111,252,997,846,886.0 (111+ trillion)
- **Values:** 31,556 unique values
- **Characteristics:**
  - Extremely wide range due to different measurement scales
  - Negative values present (deficits, losses, rate decreases)
  - Large values likely represent absolute economic metrics (GDP, total employment, etc.)
  - Small values likely represent rates, percentages, or indices
- **Purpose:** The actual measurement value for each indicator at each time period

### pct_change_period (FLOAT64)
- **Format:** Percentage change values
- **Nulls:** 0.18% (137 null values) - likely first observations per series
- **Range:** Includes -inf to +inf (infinite values present)
- **Values:** 6,775 unique values
- **Characteristics:**
  - Shows period-over-period percentage change
  - Infinite values suggest division by zero or major discontinuities
  - Nulls at series starts where no prior period exists
  - Captures rate of change for trend analysis
- **Purpose:** Period-over-period growth rate calculation

## Potential Query Considerations

### Good for Filtering:
- **series_code**: Filter to specific economic indicators (e.g., unemployment rate, GDP)
- **series_name**: More readable filtering with keyword searches
- **data_source**: Exclude interpolated data for analysis requiring actual measurements
- **year_month** or **month_date**: Time range filtering (e.g., "last 10 years", "2008 financial crisis")
- **pct_change_period**: Find periods of extreme change (WHERE pct_change_period > 10)

### Good for Grouping/Aggregation:
- **series_code** or **series_name**: Aggregate across time for specific indicators
- **year_month** (extracted year): Annual aggregations
- **data_source**: Compare actual vs. interpolated data quality
- Time-based aggregations: Quarterly, yearly summaries from monthly data

### Potential Join Keys:
- **series_code**: Join with FRED metadata tables for additional series information
- **month_date**: Join with other time-series economic tables
- **year_month**: Text-based joins if other tables use same format

### Data Quality Considerations:

1. **Infinite Values**: Handle `pct_change_period` carefully in calculations:
   - Filter out infinities: `WHERE pct_change_period NOT IN ('inf', '-inf') AND pct_change_period IS NOT NULL`
   - Consider using NULLIF or CASE statements

2. **Scale Differences**: `avg_value` ranges dramatically - normalize when comparing across series:
   - Use percentage changes rather than absolute values for comparisons
   - Consider LOG transformations for visualization

3. **Null Handling**: First observations per series lack percentage changes:
   - Use window functions with appropriate null handling
   - Consider COALESCE with 0 for certain analyses

4. **Data Source Awareness**: Mix of actual and interpolated data:
   - Filter to data_source = 'Actual' for regulatory/official reporting
   - Document when interpolated values are used

5. **Time Series Gaps**: Verify continuous sequences when expected:
   - Some series may have different start dates
   - Check for missing periods before trend analysis

6. **String Date Format**: year_month is string-based:
   - Use month_date for proper date arithmetic
   - Parse year_month carefully if needed (non-zero-padded months)

## Keywords

FRED, Federal Reserve, economic data, time series, interest rates, inflation, employment, GDP, treasury rates, consumer price index, CPI, unemployment, industrial production, labor force, economic indicators, monetary policy, fiscal data, quarterly data, monthly data, rate of change, percentage change, macroeconomic data, financial data, government statistics, US economy, economic analysis, recession indicators, market rates, bond yields, mortgage rates

## Table and Column Documentation

**Table Comment:** Not provided in source data.

**Column Comments:** No individual column comments provided in the source data. Column purposes and meanings are inferred from data patterns and standard FRED database conventions.