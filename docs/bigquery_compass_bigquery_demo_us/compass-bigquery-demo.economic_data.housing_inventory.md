---
columns:
- category_code (STRING)
- data_code (STRING)
- error_data (STRING)
- plot_grouping (STRING)
- seasonally_adj (STRING)
- series_name (STRING)
- series_value (FLOAT64)
- time (STRING)
- time_date (DATE)
schema_hash: cdff1fdea61709022bcdef7cfa503f821143fb7c2e4f8425a44671b25263533d

---
# Housing Inventory Dataset Summary

## Overall Dataset Characteristics

**Total Rows:** 2,148

**General Description:** This table contains U.S. housing market inventory data spanning from 1999 to 2023 (approximately 24 years), organized by quarters. The dataset tracks various housing metrics including occupancy rates, vacancy rates, and different categories of housing units. The data appears to be from a government or official statistical source, likely the U.S. Census Bureau's Housing Vacancy Survey.

**Data Quality:** Excellent - 0% null values across all columns, indicating complete and well-maintained data. The dataset includes both primary estimates and error measurements for quality assessment.

**Notable Patterns:**
- Quarterly time series data (105 unique quarters)
- Mix of absolute counts (housing units) and percentage rates
- Includes both seasonally adjusted and non-seasonally adjusted series
- Organized into 5 logical groupings for analysis

## Column Details

### data_code (STRING)
- **Type:** Categorical identifier/code
- **Null Values:** None (0%)
- **Unique Values:** 21 distinct codes
- **Description:** Short codes representing different housing metrics
- **Common Codes:** 
  - HOR, HVR, RVR (rates)
  - OCC, OCCUSE, OWNOCC (occupancy types)
  - RENT, OFFMAR, OTH (vacancy categories)
  - SAHOR prefix indicates seasonally adjusted series
- **Purpose:** Primary key for metric type identification

### category_code (STRING)
- **Type:** Binary categorical
- **Values:** ESTIMATE, RATE
- **Null Values:** None
- **Distribution:** Splits data into two main types:
  - ESTIMATE: Absolute housing unit counts
  - RATE: Percentage values (vacancy rates, homeownership rates)
- **Query Consideration:** Critical filter for distinguishing between count metrics and percentage metrics

### seasonally_adj (STRING)
- **Type:** Binary categorical
- **Values:** "yes", "no"
- **Null Values:** None
- **Purpose:** Indicates whether the data has been seasonally adjusted
- **Use Case:** Important for time-series analysis to choose appropriate series

### series_value (FLOAT64)
- **Type:** Numeric (decimal)
- **Null Values:** None
- **Range:** 0.1 to 146,888.0
- **Distribution:** Wide range due to mixing:
  - Small values (0.1-100): Represents rates/percentages
  - Large values (1,000-146,888): Represents housing unit counts in thousands
- **Interpretation:** Context-dependent on category_code
- **Query Consideration:** Filter by category_code before performing aggregations

### error_data (STRING)
- **Type:** Binary categorical flag
- **Values:** "yes", "no"
- **Null Values:** None
- **Purpose:** Distinguishes error measurements from primary estimates
- **Distribution:** Predominantly "no" (actual data values)
- **Query Consideration:** Filter out "yes" values for primary analysis; include for data quality assessment

### time (STRING)
- **Type:** Temporal identifier (formatted string)
- **Format:** "YYYY-QN" (e.g., "1999-Q1", "2023-Q4")
- **Null Values:** None
- **Unique Values:** 105 quarters
- **Range:** 1999-Q1 to 2023-Q4 (approximately)
- **Query Consideration:** Use for human-readable period labels

### time_date (DATE)
- **Type:** Date (normalized)
- **Format:** First day of quarter (YYYY-MM-DD)
- **Null Values:** None
- **Unique Values:** 105 dates
- **Pattern:** Quarters start on: 01-01, 04-01, 07-01, 10-01
- **Query Consideration:** PRIMARY temporal field for date-based filtering, sorting, and time-series operations

### series_name (STRING)
- **Type:** Categorical descriptor
- **Null Values:** None
- **Unique Values:** 21 distinct series
- **Description:** Human-readable names for housing metrics
- **Categories Include:**
  - Vacancy rates (Homeowner, Rental)
  - Occupancy types (Owner Occupied, Renter Occupied)
  - Vacant inventory categories (Off Market, Occasional Use)
  - Total housing metrics
  - Error series
- **Query Consideration:** Use for filtering specific metrics in analysis

### plot_grouping (STRING)
- **Type:** Categorical grouping
- **Null Values:** None
- **Unique Values:** 5 groups
- **Values:**
  - "Total Housing Units"
  - "Occupied Inventory"
  - "Vacant Inventory"
  - "Rates"
  - "Error"
- **Purpose:** High-level categorization for visualization and analysis
- **Query Consideration:** Excellent for GROUP BY operations and filtered aggregations

## Query Considerations

### Recommended Filtering Columns:
1. **time_date** - Primary temporal filter for date ranges
2. **plot_grouping** - Quick filtering by major category
3. **category_code** - Distinguish between counts and rates
4. **seasonally_adj** - Select adjusted/unadjusted series
5. **error_data** - Exclude error measurements (filter where error_data = 'no')
6. **data_code** or **series_name** - Specific metric selection

### Recommended Grouping/Aggregation:
- **Time-series analysis:** GROUP BY time_date or time
- **Cross-sectional analysis:** GROUP BY plot_grouping, series_name
- **Trend comparisons:** GROUP BY seasonally_adj, data_code
- **AVG/SUM considerations:** Only meaningful within same category_code

### Potential Join Keys:
- **time/time_date** - Join with other economic time-series data
- **data_code** - Join with metadata/definition tables

### Data Quality Considerations:
1. **Mixed Units:** Series_value contains both percentages and thousands of units - always filter by category_code first
2. **Error Records:** Filter error_data = 'no' unless analyzing data quality
3. **Seasonal Adjustment:** Choose appropriate series (adjusted vs. unadjusted) based on analysis needs
4. **Quarterly Granularity:** No monthly or annual breakdowns; all data is quarterly
5. **Complete Time Series:** 105 consecutive quarters with no gaps

### Common Query Patterns:
```sql
-- Time-series of specific metric
WHERE series_name = 'Homeownership Rate' 
  AND error_data = 'no'
  AND seasonally_adj = 'no'
ORDER BY time_date

-- Compare occupancy types over time
WHERE plot_grouping = 'Occupied Inventory'
  AND error_data = 'no'
GROUP BY time_date, series_name

-- Latest quarterly snapshot
WHERE time_date = (SELECT MAX(time_date) FROM table)
  AND error_data = 'no'
```

## Keywords

Housing inventory, vacancy rates, homeownership rate, rental vacancy, occupied housing units, vacant housing units, quarterly data, time series, seasonal adjustment, housing market, U.S. housing, Census data, economic indicators, real estate statistics, housing stock, off-market housing, owner-occupied, renter-occupied, housing estimates

## Table and Column Documentation

**Table Comment:** Not provided in the analysis report.

**Column Comments:** Not provided in the analysis report.