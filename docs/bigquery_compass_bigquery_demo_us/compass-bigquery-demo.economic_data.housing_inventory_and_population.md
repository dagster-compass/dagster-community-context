---
columns:
- number_of_households (FLOAT64)
- series_name (STRING)
- series_value (FLOAT64)
- time_date (DATE)
- year (INT64)
schema_hash: 47028a747be5120be35a64e9b949de265b115bb3d9e32aadead7034b94c6d1df

---
# Table Summary: housing_inventory_and_population

## Overall Dataset Characteristics

- **Total Rows**: 270
- **Data Quality**: Generally good quality with no null values in key columns, though `number_of_households` column is completely empty (100% null)
- **Time Period Coverage**: 2001 to 2025 (24-year span)
- **Data Granularity**: Quarterly observations based on date patterns (e.g., 2006-01-01, 2006-04-01)
- **Notable Patterns**: 
  - Contains 3 distinct housing series tracked over time
  - Each series has approximately 90 rows (270 rows ÷ 3 series)
  - Values range from ~15K to ~87K units, indicating this likely tracks a specific geographic region
  - Data appears to be time-series housing inventory data

## Column Details

### series_name (STRING)
- **Description**: Categorical identifier for the type of housing unit being measured
- **Data Type**: STRING (text)
- **Completeness**: 100% populated (0% null)
- **Cardinality**: 3 unique values (low cardinality)
- **Values**:
  - "Owner Occupied Units" - Housing units occupied by owners
  - "Renter Occupied Units" - Housing units occupied by renters
  - "Total Vacant Housing Units" - Unoccupied housing units
- **Query Use**: Excellent for filtering and grouping operations; primary dimension for analyzing different housing types

### time_date (DATE)
- **Description**: The observation date for the housing inventory measurement
- **Data Type**: DATE
- **Completeness**: 100% populated (0% null)
- **Cardinality**: 38 unique dates
- **Date Range**: 2001-01-01 to 2024-07-01 (with some 2025 dates)
- **Frequency**: Quarterly observations (dates appear on 01-01, 04-01, 07-01, 10-01)
- **Query Use**: Primary time dimension for temporal analysis, trending, and time-based filtering

### number_of_households (FLOAT64)
- **Description**: Appears intended to track household counts but is unused
- **Data Type**: FLOAT64 (decimal number)
- **Completeness**: 0% populated (100% null)
- **Status**: **DEFUNCT COLUMN** - Contains no data and should not be used in queries
- **Query Use**: None - column should be excluded from analysis

### series_value (FLOAT64)
- **Description**: The numeric measurement of housing units for each series
- **Data Type**: FLOAT64 (decimal number)
- **Completeness**: 100% populated (0% null)
- **Cardinality**: 45 unique values
- **Value Range**: 15,262 to 86,839 units
- **Distribution**: Wide range suggesting different scales for each series type
- **Query Use**: Primary metric for aggregation, trending, and calculations (SUM, AVG, MIN, MAX)

### year (INT64)
- **Description**: Extracted year component from time_date
- **Data Type**: INT64 (integer)
- **Completeness**: 100% populated (0% null)
- **Cardinality**: 14 unique years
- **Year Range**: 2001 to 2025
- **Query Use**: Convenient for year-level grouping and filtering without date manipulation; redundant with time_date but useful for simplified queries

## Potential Query Considerations

### Excellent for Filtering:
- **series_name**: Filter by housing type (owner/renter/vacant)
- **year**: Simple year-based filtering
- **time_date**: Date range queries, specific quarters, or time periods

### Excellent for Grouping/Aggregation:
- **series_name**: Compare metrics across housing types
- **year**: Annual trends and year-over-year analysis
- **time_date**: Quarterly or monthly trends (using date functions)

### Aggregation Metrics:
- **series_value**: Primary measure for:
  - Total housing units (SUM)
  - Average units over time (AVG)
  - Min/Max values (MIN/MAX)
  - Growth rates and trends
  - Occupancy calculations (Owner + Renter vs Total)

### Potential Join Keys:
- **time_date** or **year**: Could join with other economic datasets on date/year
- **series_name**: Could potentially join with housing category lookup tables
- Geographic identifier appears to be missing - this may be a region-specific table

### Data Quality Considerations:
1. **Avoid `number_of_households`**: Column is entirely null and should be excluded
2. **Year Redundancy**: `year` duplicates information from `time_date` - choose based on query needs
3. **Complete Series Check**: When querying, verify all three series_name values exist for each time period to ensure data completeness
4. **Quarterly Gaps**: Check for missing quarters when doing time-series analysis
5. **Unit Validation**: Total occupied (Owner + Renter) plus Vacant should logically represent total housing stock - validate this relationship in queries

### Common Query Patterns:
- Time-series trending by housing type
- Year-over-year growth calculations
- Occupancy rate analysis (Occupied vs Vacant)
- Owner vs Renter comparisons
- Quarterly seasonal patterns

## Keywords
housing inventory, occupied units, vacant housing, owner occupied, renter occupied, time series, economic data, housing stock, quarterly data, housing trends, real estate inventory, housing units, residential property, occupancy rates, housing market

## Table and Column Documentation
**Table Comment**: Not provided

**Column Comments**: Not provided