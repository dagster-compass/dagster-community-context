---
columns:
- number_of_households (FLOAT64)
- series_name (STRING)
- series_value (FLOAT64)
- time_date (DATE)
- year (INT64)
schema_hash: 47028a747be5120be35a64e9b949de265b115bb3d9e32aadead7034b94c6d1df

---
# Table Documentation Summary: housing_inventory_and_population

## Overall Dataset Characteristics

- **Total Rows**: 270 records
- **Time Span**: 2001-2025 (14 distinct years across 38 unique dates)
- **Data Quality**: Generally good with no nulls in active columns, though `number_of_households` is completely unpopulated
- **Structure**: Time-series data tracking housing inventory metrics across different occupancy categories
- **Notable Pattern**: Data appears to be quarterly snapshots (based on date samples like 2020-01-01, 2013-04-01, 2017-07-01) with 270 rows across 38 dates and 3 series suggests approximately 7-8 records per time period

## Column Details

### time_date (DATE)
- **Type**: DATE
- **Nulls**: 0% (Complete data)
- **Cardinality**: 38 unique dates
- **Pattern**: Quarterly snapshots (Q1, Q2, Q3, Q4 observations)
- **Sample Dates**: 2020-01-01, 2013-04-01, 2017-07-01
- **Usage**: Primary temporal dimension for time-series analysis

### series_name (STRING)
- **Type**: STRING (Categorical)
- **Nulls**: 0% (Complete data)
- **Cardinality**: 3 distinct categories
- **Categories**:
  1. Owner Occupied Units
  2. Renter Occupied Units
  3. Total Vacant Housing Units
- **Usage**: Key dimension for breaking down housing inventory by occupancy type
- **Note**: These three categories likely represent mutually exclusive housing classifications

### series_value (FLOAT64)
- **Type**: FLOAT64 (Numeric measure)
- **Nulls**: 0% (Complete data)
- **Range**: 15,262 to 86,839 units
- **Cardinality**: 45 unique values
- **Samples**: 72,565.0, 76,544.0, 17,684.0
- **Usage**: Primary metric representing housing unit counts
- **Interpretation**: Values likely represent thousands of housing units in a specific geographic area

### number_of_households (FLOAT64)
- **Type**: FLOAT64
- **Nulls**: 100% (Completely unpopulated)
- **Status**: Inactive column - no data present
- **Recommendation**: Exclude from queries as it contains no information

### year (INT64)
- **Type**: INT64
- **Nulls**: 0% (Complete data)
- **Range**: 2001-2025
- **Cardinality**: 14 distinct years
- **Sample Years**: 2001, 2003, 2005, 2006, 2010, 2011, 2013, 2016, 2017, 2020
- **Usage**: Simplified temporal dimension for year-over-year analysis
- **Note**: Extracted/derived from time_date for easier annual aggregations

## Query Considerations

### Good Filtering Columns
- **time_date**: Filter by specific dates, date ranges, quarters
- **year**: Filter by specific years or year ranges
- **series_name**: Filter by occupancy type (owner/renter/vacant)

### Good Grouping/Aggregation Columns
- **series_name**: Group by housing type to compare occupancy categories
- **year**: Group by year for annual trends
- **time_date**: Group by date for time-series analysis (can use DATE_TRUNC for quarterly/annual rollups)

### Aggregation Metrics
- **series_value**: Use SUM, AVG, MIN, MAX to analyze housing inventory levels
- Example calculations:
  - Total housing units = SUM(series_value)
  - Occupancy rate = (Owner + Renter) / (Owner + Renter + Vacant)
  - Year-over-year growth rates

### Potential Relationships
- No explicit foreign keys visible
- Could potentially join to:
  - Population tables (by time_date)
  - Economic indicator tables (by time_date, year)
  - Geographic/regional tables if region identifiers exist elsewhere

### Data Quality Considerations
1. **number_of_households** is completely null - ignore this column
2. **series_value ranges** suggest aggregate geographic level (county, metro area, or state level)
3. **Date granularity** appears quarterly - be aware when doing monthly analysis
4. **Future dates** present (up to 2025) may indicate projections or forecasts
5. **Year coverage gaps**: Non-continuous (2001, 2003, 2005... 2020) - check for data completeness when doing trend analysis

### Common Query Patterns
```sql
-- Time series by housing type
SELECT time_date, series_name, series_value
FROM table
ORDER BY time_date, series_name

-- Annual totals
SELECT year, series_name, SUM(series_value) as total_units
FROM table
GROUP BY year, series_name

-- Vacancy rate calculation
SELECT time_date,
  SUM(CASE WHEN series_name = 'Total Vacant Housing Units' THEN series_value END) /
  SUM(series_value) as vacancy_rate
FROM table
GROUP BY time_date
```

## Keywords
housing inventory, occupied units, vacant housing, owner occupied, renter occupied, housing units, time series, quarterly data, housing stock, occupancy rates, housing trends, real estate data, residential units, economic data, housing market, population housing, vacancy rates

## Table and Column Documentation
- **Table Comment**: Not provided
- **Column Comments**: Not provided