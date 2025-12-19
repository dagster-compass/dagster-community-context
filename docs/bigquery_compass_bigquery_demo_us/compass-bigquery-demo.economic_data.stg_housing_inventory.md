---
columns:
- category_code (STRING)
- cell_value (STRING)
- data_type_code (STRING)
- error_data (STRING)
- plot_grouping (STRING)
- seasonally_adj (STRING)
- series_name (STRING)
- time (STRING)
- time_slot_id (STRING)
- us (STRING)
schema_hash: 951d30c6ad8d6b9d116890873c46d330cd18caa34d234c0b324531b9519652f5

---
# Summary: Housing Inventory Data (stg_housing_inventory)

## Overall Dataset Characteristics

- **Total Rows**: 2,156
- **Data Quality**: Excellent - no null values across all columns (0.00% null percentage throughout)
- **Temporal Coverage**: Quarterly data spanning from 1999-Q1 to 2021-Q4 (105 unique quarters)
- **Geographic Scope**: United States national-level data only (all records have `us = "1"`)
- **Data Granularity**: Quarterly housing market statistics with both raw estimates and rates
- **Table Purpose**: Staging table containing housing inventory and occupancy statistics from US economic data

### Notable Patterns
- Contains both seasonally adjusted and non-seasonally adjusted data
- Includes error margins for certain metrics (indicated by `error_data` flag)
- Data is organized by different housing unit types and vacancy/occupancy statuses
- Mix of absolute counts (ESTIMATE) and percentage rates (RATE)

## Column Details

### **time_slot_id** (STRING)
- **Purpose**: Time slot identifier (appears to be a constant placeholder)
- **Value**: Always "0" (single unique value)
- **Query Use**: Not useful for filtering or grouping

### **seasonally_adj** (STRING)
- **Values**: "no" or "yes"
- **Purpose**: Indicates whether data is seasonally adjusted
- **Query Use**: Important filter for consistent time-series comparisons
- **Pattern**: Both seasonal and non-seasonal versions of metrics exist

### **data_type_code** (STRING)
- **Unique Values**: 21 distinct codes
- **Sample Codes**: 
  - OCC (Occupied Units)
  - OWNOCC (Owner Occupied)
  - RENT (For Rent)
  - HOR (Homeownership Rate)
  - HVR (Homeowner Vacancy Rate)
  - RVR (Rental Vacancy Rate)
  - OFFMAR (Off Market)
- **Query Use**: Primary dimension for filtering specific housing metrics
- **Purpose**: Categorizes the type of housing statistic

### **category_code** (STRING)
- **Values**: "ESTIMATE" or "RATE"
- **Purpose**: Distinguishes between absolute counts and percentage rates
- **Query Use**: Critical filter to separate magnitude from proportion metrics
- **Distribution**: Most data appears to be ESTIMATE category

### **us** (STRING)
- **Value**: Always "1"
- **Purpose**: Geographic identifier (US national level)
- **Query Use**: Not useful for filtering (constant value)
- **Note**: May indicate potential for state/regional data in other tables

### **cell_value** (STRING)
- **Data Type**: Numeric stored as STRING
- **Unique Values**: 313 distinct values
- **Range**: From decimals like "0.5" to large numbers like "127704"
- **Units**: Varies by data_type_code (thousands of units for estimates, percentages for rates)
- **Query Considerations**: Requires CAST to numeric for mathematical operations
- **Purpose**: The actual measurement value

### **time** (STRING)
- **Format**: "YYYY-Qn" (e.g., "1999-Q1", "2021-Q4")
- **Unique Values**: 105 quarters
- **Range**: 1999-Q1 to 2021-Q4 (23 years of quarterly data)
- **Query Use**: Primary time dimension for trend analysis and filtering
- **Note**: Stored as STRING, may need parsing for date operations

### **error_data** (STRING)
- **Values**: "no" or "yes"
- **Purpose**: Flags whether the record represents error/margin data
- **Query Use**: Filter to exclude error records when analyzing actual values
- **Pattern**: Separate error records exist for metrics with uncertainty measures

### **series_name** (STRING)
- **Unique Values**: 21 descriptive names
- **Sample Names**:
  - "Total Occupied housing Units"
  - "Owner Occupied Units"
  - "Homeownership Rate"
  - "Rental Vacancy Rate"
  - "Vacant Housing Units For Rent"
- **Purpose**: Human-readable description of the metric
- **Query Use**: User-friendly alternative to data_type_code for filtering
- **Comment**: Contains typos (e.g., "housing" not capitalized in some names)

### **plot_grouping** (STRING)
- **Unique Values**: 5 categories
- **Values**:
  - "Total Housing Units"
  - "Occupied Inventory"
  - "Vacant Inventory"
  - "Rates"
  - "Error"
- **Purpose**: High-level categorization for visualization and reporting
- **Query Use**: Useful for aggregating related metrics

## Potential Query Considerations

### Good Columns for Filtering
1. **time**: Filter by specific quarters or date ranges
2. **data_type_code**: Select specific housing metrics
3. **seasonally_adj**: Choose adjusted vs unadjusted data
4. **error_data**: Exclude error records (WHERE error_data = 'no')
5. **category_code**: Separate estimates from rates
6. **plot_grouping**: Group by broad categories

### Good Columns for Grouping/Aggregation
1. **time**: Time-series analysis, trend identification
2. **series_name**: Group by metric type
3. **plot_grouping**: High-level category summaries
4. **seasonally_adj**: Compare adjusted vs non-adjusted trends
5. **data_type_code**: Aggregate by specific metric types

### Join Considerations
- **time**: Could join to other economic tables by quarter
- **us**: Could join to geographic tables (though currently US-only)
- No obvious primary key; combination of (time, data_type_code, seasonally_adj, error_data) likely forms unique record

### Data Quality Considerations
1. **Type Conversion**: `cell_value` must be cast to numeric for calculations
2. **Error Records**: Always filter error_data appropriately
3. **Mixed Units**: Be aware that cell_value units vary by metric type
4. **Time Parsing**: May need to extract year/quarter from time string
5. **Constant Columns**: `time_slot_id` and `us` provide no variation

## Keywords

housing inventory, housing statistics, vacancy rates, homeownership, occupied units, rental vacancy, quarterly data, economic data, US housing market, seasonally adjusted, housing units, owner occupied, renter occupied, vacant housing, off market, housing census, quarterly housing statistics, time series housing data, housing occupancy rates, housing trends

## Table and Column Documentation

**Table Comment**: Not provided in the analysis report.

**Column Comments**: No column-level comments were provided in the analysis report. The column names and data suggest this is a standardized economic dataset, likely sourced from US Census Bureau Housing Vacancy Survey or similar official statistics.