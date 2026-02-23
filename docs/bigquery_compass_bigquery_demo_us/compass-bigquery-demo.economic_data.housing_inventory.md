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
# Comprehensive Summary: Housing Inventory Data

## Overall Dataset Characteristics

- **Total Rows**: 2,168 records
- **Data Quality**: Excellent - no null values detected in any column
- **Time Period**: Quarterly data spanning from 1999-Q1 to 2023-Q3 (105 unique quarters)
- **Data Structure**: Time-series housing inventory data with multiple metrics tracked over time
- **Notable Patterns**: 
  - Data is organized by quarters (Q1-Q4)
  - Contains both estimates and rates
  - Includes error/validation flags
  - Covers both seasonal and non-seasonal adjustments
  - Values range significantly from 0.1 (likely rates/percentages) to 147,947 (likely unit counts)

## Column Details

### 1. **seasonally_adj** (STRING)
- **Purpose**: Indicates whether seasonal adjustment has been applied
- **Values**: Binary ("yes", "no")
- **Pattern**: 100% complete, evenly split between adjusted and non-adjusted data
- **Query Use**: Essential filter for comparing seasonal vs. non-seasonal trends

### 2. **category_code** (STRING)
- **Purpose**: Distinguishes between absolute estimates and calculated rates
- **Values**: "ESTIMATE" (housing unit counts) and "RATE" (percentage/ratio metrics)
- **Pattern**: Two distinct measurement types
- **Query Use**: Critical for filtering numeric interpretations (units vs. percentages)

### 3. **data_code** (STRING)
- **Purpose**: Abbreviated identifier for each housing metric
- **Unique Values**: 21 distinct codes
- **Examples**: 
  - SALE, RENT, OCC (Occupied units)
  - HOR, HVR, RVR (Various vacancy/ownership rates)
  - OFFMAR, RNTSLD (Off-market and rental/sale status)
- **Query Use**: Primary key for joining or filtering specific housing metrics

### 4. **series_value** (FLOAT64)
- **Purpose**: The actual measurement value
- **Range**: 0.1 to 147,947
- **Pattern**: 316 unique values suggesting aggregated/rounded data
- **Interpretation**: 
  - Large values (>1000): Housing unit counts in thousands
  - Small values (<10): Percentages or rates
- **Query Use**: Primary numeric field for aggregations, trends, and calculations

### 5. **error_data** (STRING)
- **Purpose**: Flags whether the row contains error/margin-of-error data
- **Values**: Binary ("yes", "no")
- **Pattern**: Primarily "no" values
- **Query Use**: Filter to exclude error calculations from main analyses

### 6. **series_name** (STRING)
- **Purpose**: Human-readable description of the metric
- **Unique Values**: 21 distinct series names
- **Examples**:
  - "Total Occupied housing Units"
  - "Homeowner Vacancy Rate"
  - "Rented or Sold, Not Yet Occupied Vacant Housing Units"
  - "Held Off the Market Vacant Housing Units"
- **Query Use**: Ideal for display labels and filtering by metric type

### 7. **time** (STRING)
- **Purpose**: Quarter identifier in text format
- **Format**: "YYYY-Q#" (e.g., "2013-Q2", "2019-Q4")
- **Unique Values**: 105 quarters
- **Range**: 1999-Q1 to 2023-Q3
- **Query Use**: Time filtering, but time_date is more suitable for date operations

### 8. **plot_grouping** (STRING)
- **Purpose**: High-level categorization for visualization/analysis
- **Categories** (5 types):
  - "Total Housing Units"
  - "Occupied Inventory"
  - "Vacant Inventory"
  - "Rates"
  - "Error"
- **Query Use**: Excellent for grouping related metrics in analyses

### 9. **time_date** (DATE)
- **Purpose**: Standardized date representation (first day of quarter)
- **Format**: YYYY-MM-DD (01-01, 04-01, 07-01, 10-01)
- **Unique Values**: 105 dates matching quarters
- **Query Use**: Preferred field for time-based filtering, ordering, and date calculations

## Potential Query Considerations

### Best Columns for Filtering:
- **time_date**: For time range queries (most common)
- **category_code**: To separate estimates from rates
- **plot_grouping**: For broad metric categories
- **seasonally_adj**: To get consistent seasonal treatment
- **error_data**: To exclude margin-of-error records
- **data_code**: For specific metric selection

### Best Columns for Grouping/Aggregation:
- **time_date** or **time**: For time-series analysis
- **plot_grouping**: For category-level summaries
- **series_name**: For metric-specific breakdowns
- **seasonally_adj**: For comparing adjusted vs. unadjusted data

### Potential Join Keys:
- **data_code** + **series_name**: Could link to metadata tables
- **time_date**: For joining with other time-series economic data
- No obvious internal relationships (appears to be a single fact table)

### Data Quality Considerations:
- **No null handling needed**: Perfect data completeness
- **Mixed units**: series_value contains both counts (thousands) and rates (percentages) - must filter by category_code
- **Duplicate awareness**: Same time period may have multiple rows for different metrics
- **Time consistency**: Quarterly data only - no monthly or annual aggregations present
- **Error records**: Remember to filter out error_data='yes' unless specifically analyzing margins of error

## Keywords
housing inventory, vacancy rates, homeownership, rental units, occupied housing, vacant units, quarterly data, economic data, real estate statistics, housing stock, time series, seasonal adjustment, US housing market, residential inventory, homeowner vacancy, rental vacancy, off-market housing, housing estimates

## Table and Column Documentation

**Table Comment**: Not provided

**Column Comments**: Not provided