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

**Dataset Size:** 2,176 rows

**Data Quality:** High quality dataset with no null values across any columns. All fields are fully populated, indicating clean, well-maintained data.

**Time Period Coverage:** Quarterly data spanning from 1999-Q1 through approximately 2016 (105 unique quarters)

**Geographic Scope:** United States national-level data only (us="1" for all records)

**Data Structure:** This is a time-series dataset tracking various housing inventory metrics and rates across different categories. The data appears to be sourced from official housing statistics (likely Census Bureau's Housing Vacancy Survey).

## Column Details

### **category_code** (STRING)
- **Type:** Categorical identifier
- **Values:** ESTIMATE (actual measurements) or RATE (calculated percentages)
- **Nulls:** None (0%)
- **Usage:** Distinguishes between absolute counts and percentage-based metrics

### **time_slot_id** (STRING)
- **Type:** Fixed identifier
- **Values:** Always "0"
- **Nulls:** None (0%)
- **Usage:** Appears to be a technical field with no variation; may be unused or placeholder

### **seasonally_adj** (STRING)
- **Type:** Boolean indicator
- **Values:** "yes" or "no"
- **Nulls:** None (0%)
- **Usage:** Indicates whether data has been seasonally adjusted to remove cyclical patterns

### **data_type_code** (STRING)
- **Type:** Metric identifier code
- **Unique Values:** 21 distinct codes
- **Sample Codes:** OCC (Occupied), HOR (Homeownership Rate), HVR (Homeowner Vacancy Rate), RVR (Rental Vacancy Rate), OFFMAR (Off Market), URE, YRVAC, RNTSLD
- **Nulls:** None (0%)
- **Usage:** Primary classification for different housing metrics; essential for filtering specific data types

### **cell_value** (STRING)
- **Type:** Numeric data stored as string
- **Unique Values:** 317 distinct values
- **Range:** Values vary from small rates (likely single digits for percentages) to large counts (up to 119,129 for total occupied units)
- **Nulls:** None (0%)
- **Usage:** The actual measurement value; requires casting to numeric type for calculations

### **error_data** (STRING)
- **Type:** Boolean indicator
- **Values:** "yes" or "no"
- **Nulls:** None (0%)
- **Usage:** Flags whether the row represents error margin data (important for statistical accuracy)

### **time** (STRING)
- **Type:** Temporal identifier
- **Format:** YYYY-Q# (e.g., "2005-Q2", "2013-Q3")
- **Unique Values:** 105 quarters
- **Range:** 1999-Q1 through ~2016
- **Nulls:** None (0%)
- **Usage:** Primary time dimension for time-series analysis; requires parsing for date operations

### **us** (STRING)
- **Type:** Geographic identifier
- **Values:** Always "1"
- **Nulls:** None (0%)
- **Usage:** Indicates national-level data; no variation (may support future state-level data)

### **series_name** (STRING)
- **Type:** Descriptive label
- **Unique Values:** 21 distinct series
- **Sample Names:** 
  - "Homeownership Rate"
  - "Homeowner Vacancy Rate"
  - "Rental Vacancy Rate"
  - "Total Occupied housing Units"
  - "Owner Occupied Units"
  - "Held Off the Market Vacant Housing Units"
  - "Year-Round Vacant Housing Units"
- **Nulls:** None (0%)
- **Usage:** Human-readable description of the metric; useful for reporting and display

### **plot_grouping** (STRING)
- **Type:** Categorical grouping
- **Unique Values:** 5 categories
- **Values:**
  - "Error" (error margins)
  - "Occupied Inventory" (occupied housing metrics)
  - "Rates" (percentage-based metrics)
  - "Total Housing Units" (aggregate counts)
  - "Vacant Inventory" (vacant housing metrics)
- **Nulls:** None (0%)
- **Usage:** High-level categorization for organizing visualizations and reports

## Potential Query Considerations

### **Excellent Filtering Columns:**
- **time**: Filter by specific quarters or date ranges for time-series analysis
- **data_type_code**: Select specific metrics (e.g., only homeownership rates)
- **plot_grouping**: Filter by broad category (e.g., all vacancy metrics)
- **seasonally_adj**: Separate seasonally adjusted from non-adjusted data
- **error_data**: Exclude error margin rows when analyzing point estimates
- **category_code**: Filter for rates vs. estimates

### **Good for Grouping/Aggregation:**
- **time**: Group by quarter for time-series trends
- **plot_grouping**: Aggregate related metrics together
- **seasonally_adj**: Compare adjusted vs. non-adjusted trends
- **data_type_code**: Group by metric type for comprehensive analysis

### **Key Metrics (data_type_code values):**
- **OCC**: Total occupied housing units (absolute count)
- **HOR**: Homeownership rate (percentage)
- **HVR**: Homeowner vacancy rate (percentage)
- **RVR**: Rental vacancy rate (percentage)

### **Data Quality Considerations:**
1. **cell_value is STRING**: Must cast to FLOAT64 or INT64 for mathematical operations
2. **time is STRING**: Parse to DATE or TIMESTAMP for temporal operations
3. **Mixed units**: Some values are counts (thousands of units), others are percentages—check category_code and series_name
4. **Error rows**: Filter out error_data='yes' unless specifically analyzing margins of error
5. **No nulls**: No need for null handling, but always validate numeric conversions
6. **Seasonality**: Consider filtering by seasonally_adj based on analysis needs

### **Common Query Patterns:**
- Time-series trend analysis (GROUP BY time)
- Comparing rates vs. estimates (filter by category_code)
- Vacancy analysis (filter plot_grouping = 'Vacant Inventory')
- Homeownership trends (filter data_type_code = 'HOR')
- Quarter-over-quarter changes (self-join on time with LAG functions)

### **Potential Relationships:**
- No obvious foreign keys to other tables
- Self-joinable on time for period-over-period comparisons
- Could potentially join to geographic tables if expanded beyond national data

## Keywords

housing inventory, vacancy rates, homeownership rate, occupied units, vacant units, quarterly data, time series, Census data, real estate statistics, housing stock, rental vacancy, homeowner vacancy, seasonal adjustment, US housing market, housing units, off-market inventory, year-round vacant, occasional use, economic indicators, housing survey, 1999-2016

## Table and Column Docs

**Table Comment:** Not provided

**Column Comments:** None provided for any columns