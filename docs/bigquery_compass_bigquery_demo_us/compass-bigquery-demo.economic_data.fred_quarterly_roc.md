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
# Table Summary: fred_quarterly_roc

## Overall Dataset Characteristics

**Total Rows:** 75,492

**General Description:** This table contains economic time series data from FRED (Federal Reserve Economic Data), tracking rate of change (ROC) for various economic indicators on a monthly basis. The dataset spans from 1913 to approximately 2022, covering over a century of economic data.

**Data Quality:** 
- Excellent overall data quality with minimal null values
- Only `pct_change_period` has any nulls (0.18% - approximately 136 rows)
- All other columns are complete (0% null)
- Contains both actual reported values and interpolated data points

**Notable Patterns:**
- Historical span: 1913 to 2022+ (1,397 unique months)
- 136 different economic series tracked
- Mix of actual and interpolated data sources
- Wide range of value magnitudes across different series
- Percentage changes can be extreme (including infinite values in some cases)

## Column Details

### year_month (STRING)
**Format:** YYYY-M or YYYY-MM (e.g., "1913-1", "2021-5")
- Complete data (0% null)
- 1,397 unique values representing individual months
- Spans from 1913 to 2022+
- Inconsistent formatting (single vs. double digit months)
- **Use Case:** Good for filtering by time periods, but may require string parsing

### data_source (STRING)
**Values:** "Actual" or "Interpolated"
- Complete data (0% null)
- Only 2 unique values
- Indicates whether the data point is reported or calculated/estimated
- **Use Case:** Critical for data quality filtering; users may want to distinguish between actual vs. interpolated values

### series_code (STRING)
**Format:** Alphanumeric codes (e.g., "DFF", "NFCICREDIT", "CE16OV")
- Complete data (0% null)
- 136 unique series codes
- Standard FRED database series identifiers
- Examples: GDP deflator (GDPDEF), Federal Funds Rate (DFF), Employment Level (CE16OV)
- **Use Case:** Primary key for joining with other FRED data or filtering specific economic indicators

### series_name (STRING)
**Format:** Descriptive text names
- Complete data (0% null)
- 134 unique names (note: 136 codes but 134 names suggests some codes may share names)
- Human-readable descriptions of economic indicators
- Examples: "Federal Funds Effective Rate", "Gross Domestic Product: Implicit Price Deflator", "Employment Level"
- Includes detailed descriptors like location, adjustment type (seasonally adjusted), and units
- **Use Case:** User-friendly filtering and display; better for non-technical queries

### month_date (TIMESTAMP)
**Format:** UTC timestamp, first day of each month at 00:00:00
- Complete data (0% null)
- 1,397 unique dates matching year_month cardinality
- Spans 1913-01-01 to 2022+ 
- Consistent format: always the 1st of the month
- **Use Case:** Optimal for time-based filtering, sorting, and date range queries; preferred over year_month for date operations

### pct_change_period (FLOAT64)
**Description:** Percentage change from previous period
- 0.18% null (136 rows) - likely first values in series or data gaps
- 6,747 unique values
- Range: -∞ to +∞ (includes infinite values indicating extreme changes or division by zero scenarios)
- Represents rate of change (ROC) - the key metric in this table
- Sample values show typical ranges from -15.91% to +12.46%
- **Use Case:** Primary metric for analysis; useful for trend detection, volatility analysis; requires null handling and infinite value filtering

### avg_value (FLOAT64)
**Description:** Average value of the economic indicator for the period
- Complete data (0% null)
- 31,606 unique values
- Extremely wide range: -136,419 to 110,982,661,180,013
- Different series have vastly different scales (e.g., rates in single digits, dollar amounts in trillions)
- **Use Case:** Actual values of indicators; requires series-specific interpretation due to scale differences; useful for absolute value analysis rather than comparative analysis across series

## Potential Query Considerations

### Good Filtering Columns:
1. **series_code / series_name**: Filter for specific economic indicators
2. **month_date**: Time range filtering (preferred over year_month)
3. **data_source**: Distinguish actual vs. interpolated data
4. **year_month**: Period-specific queries (requires string matching)

### Good Grouping/Aggregation Columns:
1. **series_code**: Aggregate metrics by economic indicator
2. **year_month** or **month_date**: Time-based aggregations (monthly, quarterly, yearly)
3. **data_source**: Compare actual vs. interpolated data quality

### Potential Join Keys:
- **series_code**: Standard FRED identifier for joining with other economic datasets
- **month_date**: For time-series joins with other temporal data
- Combination of **series_code + month_date**: Composite key for precise record matching

### Data Quality Considerations:

1. **Scale Differences**: Different series have vastly different value ranges - avoid comparing avg_value across series without normalization

2. **Infinite Values**: pct_change_period contains infinite values - queries should filter these when calculating aggregates:
   ```sql
   WHERE pct_change_period IS NOT NULL 
   AND pct_change_period != 'inf' 
   AND pct_change_period != '-inf'
   ```

3. **Date Format Inconsistency**: year_month has inconsistent formatting - use month_date for reliable date operations

4. **Interpolated Data**: Consider filtering by data_source = 'Actual' for analysis requiring only reported values

5. **Historical Gaps**: Some series may not span the entire time range; check data availability for specific series

6. **First Period Values**: pct_change_period will be null for the first observation of each series (no prior period for comparison)

## Keywords

FRED, Federal Reserve, economic data, time series, rate of change, ROC, quarterly data, monthly data, economic indicators, GDP, employment, inflation, interest rates, financial conditions, treasury rates, corporate bonds, consumer price index, CPI, labor force, mortgage rates, breakeven inflation, yield curve, economic statistics, macroeconomic data, financial metrics, percentage change, historical economic data, interpolated data, seasonally adjusted, US economy

## Table and Column Documentation

**Table Comment:** Not provided

**Column Comments:** Not provided