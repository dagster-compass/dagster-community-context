---
columns:
- data_source (STRING)
- date (TIMESTAMP)
- period_diff (FLOAT64)
- series_code (STRING)
- series_name (STRING)
- value (FLOAT64)
schema_hash: 17b7a7e19d49d4928b28d7aee79c2599fa3a70e8d7187e98275be5a200105e29

---
# Comprehensive Data Summary: FRED Monthly Difference Table

## Overall Dataset Characteristics

**Total Rows:** 85,646

**Dataset Type:** Economic time series data from the Federal Reserve Economic Data (FRED) database, tracking month-over-month changes across various economic indicators.

**Time Range:** Historical data spanning from 1913 to present (approximately 1,474 unique months)

**Data Quality:** 
- Excellent overall data quality with minimal null values
- Only the `period_diff` column shows any null values (0.16%, or ~137 rows)
- Multiple data filling methodologies employed (Actual, Backward Filled, Forward Filled, Interpolated) to ensure data completeness
- Well-structured with consistent timestamp formatting

**Notable Patterns:**
- Contains 134-136 distinct economic series covering various categories (interest rates, housing, employment, inflation, monetary policy, etc.)
- The `period_diff` column captures month-over-month changes, making this particularly useful for trend analysis
- Wide value ranges indicating diverse economic metrics (from percentage rates to absolute dollar amounts)

## Column Details

### series_name (STRING)
**Purpose:** Human-readable description of the economic indicator

**Characteristics:**
- 134 unique series names
- No null values (100% populated)
- Categories include:
  - Interest rates and treasury yields (1-Year, 10-Year Treasury rates, mortgage rates)
  - Inflation metrics (Breakeven Inflation Rates)
  - Yield curve indicators (Treasury maturity spreads)
  - Housing metrics (mortgage rates, permits, prices)
  - Labor market data (participation rates)
  - Monetary aggregates (M1 Money Stock)

**Query Considerations:** Ideal for filtering by specific economic indicators; useful for user-friendly result displays

### series_code (STRING)
**Purpose:** FRED standardized identifier for each economic series

**Characteristics:**
- 136 unique codes (slightly more than series names, suggesting some naming variations)
- No null values
- Examples: CIVPART, PCECC96, PERMIT, MSPUS, PSAVERT, EMRATIO
- Alphanumeric codes of varying lengths

**Query Considerations:** Primary identifier for precise series selection; essential for joins with other FRED datasets

### date (TIMESTAMP)
**Purpose:** Month reference date for each observation

**Characteristics:**
- 1,474 unique monthly timestamps
- Spans from January 1913 to recent data
- Formatted as first day of each month (e.g., "1913-01-01 00:00:00+00:00")
- Timezone-aware (UTC indicated by +00:00)
- No null values

**Query Considerations:** 
- Critical for time-based filtering and ordering
- Ideal for time series analysis, trend identification, and period comparisons
- Can be used for date range filtering, monthly/yearly aggregations
- Extract functions (YEAR, MONTH) would be useful for grouping

### data_source (STRING)
**Purpose:** Indicates methodology used to generate the data point

**Characteristics:**
- 4 distinct values:
  - **Actual:** Original reported data
  - **Backward Filled:** Missing values filled using previous observations
  - **Forward Filled:** Missing values filled using future observations
  - **Interpolated:** Missing values estimated between known points
- No null values
- Distribution varies by series and time period

**Query Considerations:** 
- Important for data quality filtering (e.g., excluding filled/interpolated values)
- Useful for understanding data reliability in queries
- Should be considered when performing statistical analysis

### value (FLOAT64)
**Purpose:** The actual measurement value for the economic indicator at the given date

**Characteristics:**
- 30,997 unique values
- Extremely wide range: -136,419.0 to 110,982,661,180,013.0
- Scale varies dramatically by series (percentages vs. absolute dollar amounts)
- No null values
- Examples: 7.2 (likely percentage), 1,638.0 (possibly index value), 1,680.63 (precise measurement)

**Query Considerations:**
- Essential for aggregation functions (AVG, SUM, MIN, MAX)
- Requires series context for meaningful interpretation
- May need normalization or filtering by series type for cross-series comparisons
- Large range suggests need for careful handling of outliers

### period_diff (FLOAT64)
**Purpose:** Month-over-month change in the value

**Characteristics:**
- 9,083 unique values
- 0.16% null values (~137 rows, likely first observations for each series)
- Range: -4,432,974,813,784.89 to 12,227,714,229,744.7
- Represents calculated differences between consecutive months
- Examples: 12.0, 0.09, 0.24, 6.18, -54.0, 0.7, -1,469.5

**Query Considerations:**
- Key metric for trend analysis and momentum indicators
- Null values likely represent series start dates (no prior period for comparison)
- Useful for identifying growth rates, volatility, and turning points
- Consider filtering out nulls when calculating statistics

## Potential Query Considerations

### Optimal Filtering Columns:
1. **series_code/series_name:** Filter to specific economic indicators
2. **date:** Time range selections, recent data queries
3. **data_source:** Quality-based filtering (actual vs. interpolated)
4. **period_diff:** Identifying significant changes (WHERE period_diff > threshold)

### Grouping/Aggregation Opportunities:
1. **By series:** Analyze individual economic indicators over time
2. **By date periods:** Monthly, quarterly, yearly aggregations using date extraction
3. **By data_source:** Compare reliability of different data methodologies
4. **Cross-series analysis:** Compare multiple indicators within time windows

### Potential Join Keys:
1. **series_code:** Primary key for joining with other FRED metadata tables
2. **date:** Time-based joins with other temporal economic datasets
3. **Composite key (series_code + date):** Unique record identifier

### Data Quality Considerations:
1. **Scale normalization:** Value ranges differ dramatically by series; normalize for cross-series comparisons
2. **Null handling:** period_diff nulls indicate series start dates
3. **Data source awareness:** Consider filtering by "Actual" for most reliable analysis
4. **Time series completeness:** Use data_source to identify gaps vs. filled values
5. **Outlier detection:** Extreme values in both value and period_diff columns may need validation

### Common Query Patterns:
- Time series analysis for specific indicators
- Period-over-period change analysis using period_diff
- Multi-indicator comparisons across same time periods
- Trend identification (consecutive positive/negative period_diff)
- Historical data retrieval for backtesting economic models
- Volatility analysis using period_diff standard deviations

## Keywords

FRED, Federal Reserve Economic Data, economic indicators, time series, monthly data, interest rates, treasury rates, inflation, housing data, employment statistics, labor force, mortgage rates, monetary policy, yield curve, economic trends, period over period, month over month change, M1 money supply, GDP, consumer spending, building permits, producer price index, housing prices, participation rate, breakeven inflation, treasury maturity, forward rates, economic analysis, financial metrics, macroeconomic data

## Table and Column Documentation

**Table Comment:** Not provided in the source analysis.

**Column Comments:** No column-level comments were provided in the source analysis.