---
columns:
- county (STRING)
- median_property_taxes_paid_by_county_2021_5_year_estimate (INT64)
- state (STRING)
schema_hash: ff4c4d9126f8ac82b4a56d344f64cdefa61b08063949cfbe8f312bd99b8c0a9c

---
# Property Taxes State County Dataset Summary

## Overall Dataset Characteristics

- **Total Rows**: 3,221 records
- **Data Quality**: High quality dataset with minimal missing data (only 0.56% null values in the tax amount column)
- **Geographic Coverage**: Comprehensive coverage of US counties across all 50 states plus District of Columbia (52 total state/territory entities)
- **Data Source**: 2021 5-year estimate data, indicating this is likely American Community Survey (ACS) data
- **Notable Patterns**: 
  - Wide range of property tax values ($200 to $10,000) reflecting significant geographic variation
  - Nearly complete geographic coverage with 1,955 unique counties represented
  - Clean, standardized naming conventions for states and counties

## Column Details

### state (STRING)
- **Data Type**: String with full state names
- **Completeness**: 100% complete (0% null values)
- **Distribution**: 52 unique values covering all US states plus DC
- **Format**: Full state names (e.g., "Michigan", "South Carolina", "Alabama")
- **Query Considerations**: Excellent for geographic filtering and grouping by state

### county (STRING)
- **Data Type**: String with county names including "County" suffix
- **Completeness**: 100% complete (0% null values)
- **Distribution**: 1,955 unique counties (high cardinality)
- **Format**: Standardized format with "County" suffix (e.g., "Hand County", "Carroll County")
- **Query Considerations**: Good for specific county lookups; note that county names may repeat across states

### median_property_taxes_paid_by_county_2021_5_year_estimate (INT64)
- **Data Type**: Integer representing dollar amounts
- **Completeness**: 99.44% complete (0.56% null values - 18 missing records)
- **Distribution**: 1,946 unique values ranging from $200 to $10,000
- **Sample Values**: $541, $2,831, $856, $1,094, $1,518
- **Query Considerations**: Primary metric for analysis, aggregation, and comparison

## Potential Query Considerations

### Filtering Opportunities
- **Geographic filtering**: Filter by specific states or regions
- **Tax range filtering**: Filter counties by property tax brackets (low, medium, high)
- **Data completeness**: May want to exclude records with null tax values

### Grouping/Aggregation Opportunities
- **State-level analysis**: GROUP BY state for state comparisons
- **Regional analysis**: Can group states into regions for broader geographic analysis
- **Tax bracket analysis**: Create buckets/ranges of tax amounts for distribution analysis
- **Statistical aggregations**: Calculate state averages, medians, min/max values

### Join Considerations
- **Primary Keys**: Combination of (state, county) forms a natural composite key
- **Potential Joins**: Can join with other county-level demographic or economic datasets
- **Geographic Relationships**: Can join with state-level data using the state column

### Data Quality Considerations
- **Missing Values**: 18 records (0.56%) have null property tax values - consider how to handle in aggregations
- **County Name Standardization**: County names include "County" suffix consistently
- **State Name Format**: Uses full state names rather than abbreviations - may need conversion for joins with other datasets
- **Currency Format**: Tax values are in whole dollars (no cents), suitable for most financial analyses

## Keywords

Property taxes, county data, state data, real estate, tax assessment, geographic analysis, ACS data, American Community Survey, median taxes, county-level statistics, US counties, state comparison, tax burden, real estate taxation

## Table and Column Documentation

**Table Comment**: Not provided in the analysis

**Column Comments**: No column comments were provided in the analysis