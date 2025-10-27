---
columns:
- county (STRING)
- median_property_taxes_paid_by_county_2021_5_year_estimate (INT64)
- state (STRING)
schema_hash: ff4c4d9126f8ac82b4a56d344f64cdefa61b08063949cfbe8f312bd99b8c0a9c

---
# Comprehensive Data Summary: Property Taxes State County Dataset

## Keywords
property taxes, median property tax, county data, state data, real estate taxes, US counties, property tax analysis, geographic analysis, tax burden, 2021 estimates

## Overall Dataset Characteristics

- **Total Rows**: 3,221 records
- **Geographic Coverage**: Complete US coverage with 52 unique states/territories (including District of Columbia)
- **Granularity**: County-level data across all US states
- **Data Quality**: Excellent overall quality with minimal missing values (only 0.56% nulls in tax data)
- **Time Period**: 2021 5-year estimates (American Community Survey data)
- **Data Distribution**: Wide range of property tax values from $200 to $10,000, indicating significant geographic variation in tax burden

## Column Details

### state (STRING)
- **Data Type**: String/Text
- **Completeness**: 100% complete (0% null values)
- **Unique Values**: 52 distinct states/territories
- **Geographic Scope**: All US states plus District of Columbia
- **Sample Values**: Illinois, Ohio, South Dakota, Georgia, Florida
- **Format**: Full state names (not abbreviations)
- **Query Considerations**: Primary grouping column for state-level analysis

### county (STRING)
- **Data Type**: String/Text
- **Completeness**: 100% complete (0% null values)
- **Unique Values**: 1,955 distinct counties
- **Format**: County names with "County" suffix (e.g., "Hughes County", "Barrow County")
- **Geographic Coverage**: Represents most US counties
- **Query Considerations**: Useful for county-level filtering and analysis

### median_property_taxes_paid_by_county_2021_5_year_estimate (INT64)
- **Data Type**: Integer (whole dollar amounts)
- **Completeness**: 99.44% complete (0.56% null values)
- **Unique Values**: 1,946 distinct tax amounts
- **Value Range**: $200 to $10,000
- **Statistical Distribution**: Wide variation suggesting significant geographic disparities
- **Sample Values**: $2,356, $1,669, $651, $1,243, $1,569
- **Data Source**: Based on American Community Survey 5-year estimates
- **Query Considerations**: Primary metric for analysis, aggregation, and ranking

## Potential Query Considerations

### Filtering Opportunities
- **State-based filtering**: Filter by specific states or regions
- **Tax range filtering**: Find counties with tax burdens within specific ranges
- **Non-null filtering**: Exclude the 0.56% of records with missing tax data

### Grouping and Aggregation Possibilities
- **State-level aggregation**: Calculate average, median, min, max property taxes by state
- **Regional analysis**: Group states into regions for broader geographic analysis
- **Tax bracket analysis**: Group counties into tax burden categories (low, medium, high)
- **Statistical analysis**: Percentile calculations, standard deviation analysis

### Join Key Potential
- **state + county**: Could serve as composite key for joining with other county-level datasets
- **state**: Can be joined with state-level demographic, economic, or political data
- **Geographic matching**: Potential joins with census data, economic indicators, or housing market data

### Data Quality Considerations
- **Missing values**: 18 records (0.56%) have null property tax values - consider excluding from calculations
- **Outlier detection**: Tax values at extreme ends ($200, $10,000) may warrant investigation
- **Standardization**: All county names include "County" suffix for consistency
- **Time sensitivity**: Data represents 5-year estimates centered on 2021

### Analytical Use Cases
- **Comparative analysis**: Ranking states/counties by property tax burden
- **Geographic visualization**: Mapping property tax variations across the US
- **Economic analysis**: Correlating property taxes with other economic indicators
- **Policy research**: Analyzing tax policy impacts across different jurisdictions

## Table and Column Documentation
*No table comment or column comments were provided in the source data.*