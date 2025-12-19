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
# Table Summary: fred_monthly_diff

## Overall Dataset Characteristics

**Dataset Size:** 85,491 rows

**Purpose:** This table contains monthly economic time series data from FRED (Federal Reserve Economic Data), with calculated period-over-period differences. The data spans from 1913 to at least 2022, covering approximately 109 years of economic indicators.

**Data Quality:** 
- Excellent overall quality with minimal null values (only 0.16% nulls in period_diff column)
- All core columns (date, data_source, series_name, series_code, value) are complete with 0% nulls
- Data includes both actual measurements and imputed values (backward filled, forward filled, interpolated)

**Notable Patterns:**
- 136 unique economic series tracked over 1,474 distinct monthly timestamps
- Average of ~63 rows per month (85,491 / 1,474), suggesting not all series cover the full time range
- Value ranges are extremely wide (-136K to 111+ trillion), indicating diverse metric types (rates, percentages, absolute counts, dollar amounts)
- Four distinct data source types indicate sophisticated gap-filling methodology

## Column Details

### date (TIMESTAMP)
- **Type:** Timestamp with timezone (UTC)
- **Range:** 1913-01-01 to at least 2022-06-01
- **Completeness:** 100% (no nulls)
- **Cardinality:** 1,474 unique dates (monthly granularity)
- **Pattern:** First day of each month (consistent YYYY-MM-01 format)
- **Usage Notes:** Primary temporal dimension for time series analysis

### data_source (STRING)
- **Type:** Categorical string
- **Completeness:** 100% (no nulls)
- **Values:** 
  - "Actual" (observed/measured data)
  - "Backward Filled" (imputed using previous values)
  - "Forward Filled" (imputed using future values)
  - "Interpolated" (calculated between known values)
- **Distribution:** Actual values predominate in samples
- **Usage Notes:** Critical for filtering based on data quality requirements; use to exclude imputed data if needed

### series_name (STRING)
- **Type:** Descriptive text
- **Completeness:** 100% (no nulls)
- **Cardinality:** 134 unique series
- **Examples:**
  - Interest rates (Treasury rates, Federal Funds, mortgage rates)
  - Inflation measures (Breakeven Inflation Rate)
  - Yield curve indicators (10Y-2Y spread, 10Y-3M spread)
  - Employment metrics (Unemployed)
  - Price indices (CPI, PPI)
  - Banking metrics (Business Loans)
- **Usage Notes:** Human-readable names for economic indicators; use for reporting and filtering

### series_code (STRING)
- **Type:** FRED series identifier
- **Completeness:** 100% (no nulls)
- **Cardinality:** 136 unique codes (slightly more than series_names)
- **Format:** Alphanumeric codes (e.g., FEDFUNDS, UNEMPLOY, CPIFABSL)
- **Examples:** A191RL1Q225SBEA, AAA10Y, BAMLC0A0CM, BUSLOANS, CDSP
- **Usage Notes:** Official FRED identifiers; use for precise filtering and joining with external FRED data

### value (FLOAT64)
- **Type:** Numeric (double precision floating point)
- **Completeness:** 100% (no nulls)
- **Range:** -136,419 to 111,252,997,846,886 (extremely wide range)
- **Cardinality:** 30,942 unique values
- **Examples:** 5.45 (likely %), 113,282 (possibly thousands), 218.86 (possibly index)
- **Scale Considerations:** 
  - Percentages (rates): typically 0-20
  - Indices: typically 100-300
  - Absolute counts: thousands to millions
  - Dollar amounts: potentially billions to trillions
- **Usage Notes:** Mixed units require understanding of each series; avoid aggregating across different series types

### period_diff (FLOAT64)
- **Type:** Numeric (double precision floating point)
- **Completeness:** 99.84% (0.16% nulls - likely first observations per series)
- **Range:** -4,523,792,316,262 to 12,249,177,969,308
- **Cardinality:** 9,073 unique values
- **Purpose:** Month-over-month change in value
- **Examples:** 0.16, 0.0, 0.21, 0.5, -0.2
- **Null Pattern:** Expected nulls for first period of each time series
- **Usage Notes:** Pre-calculated difference; useful for trend analysis without needing LAG functions

## Potential Query Considerations

### Good Filtering Columns:
1. **series_code / series_name:** Filter to specific economic indicators
2. **date:** Time-based filtering (date ranges, specific months/years)
3. **data_source:** Filter by data quality (e.g., `WHERE data_source = 'Actual'`)
4. **value ranges:** Filter extreme values or specific thresholds

### Good Grouping/Aggregation Columns:
1. **date:** Time series aggregations (monthly, quarterly, yearly trends)
2. **series_code / series_name:** Aggregate statistics per indicator
3. **data_source:** Compare actual vs imputed data quality
4. **EXTRACT(YEAR FROM date):** Annual aggregations
5. **EXTRACT(MONTH FROM date):** Seasonal patterns

### Potential Join Keys:
- **series_code:** Join with FRED metadata tables
- **date:** Join with other temporal economic data
- **Composite key (series_code, date):** Unique identifier for specific observations

### Data Quality Considerations:

1. **Scale Normalization:** Values span 15+ orders of magnitude; percentages, indices, and absolute values require separate handling
2. **Missing Data Handling:** 
   - Consider filtering `data_source != 'Actual'` for analysis requiring real observations
   - period_diff nulls indicate series start points
3. **Time Series Gaps:** Not all series cover full date range; check data availability per series
4. **Outlier Detection:** Extreme values may be legitimate (e.g., GDP in trillions) or errors
5. **Rate vs Level:** Mix of rate measures (%) and level measures (absolute values)
6. **Seasonal Adjustments:** Unknown if data is seasonally adjusted; may need to account for seasonality

### Recommended Query Patterns:

1. **Single Series Analysis:**
   ```sql
   WHERE series_code = 'FEDFUNDS' 
   AND data_source = 'Actual'
   ORDER BY date
   ```

2. **Multiple Series Comparison:**
   ```sql
   WHERE series_code IN ('FEDFUNDS', 'UNEMPLOY')
   PIVOT on series_name
   ```

3. **Trend Analysis:**
   ```sql
   SELECT EXTRACT(YEAR FROM date), AVG(value)
   GROUP BY series_code, year
   ```

4. **Recent Data:**
   ```sql
   WHERE date >= DATE_SUB(CURRENT_DATE(), INTERVAL 12 MONTH)
   ```

## Keywords
FRED, Federal Reserve, economic data, time series, monthly data, interest rates, inflation, unemployment, CPI, PPI, Treasury rates, Federal Funds Rate, mortgage rates, yield curve, economic indicators, financial data, macroeconomic data, period difference, month-over-month change, backward fill, forward fill, interpolation, data imputation

## Table and Column Documentation

**Table Comment:** Not provided

**Column Comments:** Not provided