---
columns:
- county (STRING)
- median_property_taxes_paid_by_county_2021_5_year_estimate (INT64)
- state (STRING)
schema_hash: ff4c4d9126f8ac82b4a56d344f64cdefa61b08063949cfbe8f312bd99b8c0a9c

---
# Table Summary: Property Taxes by State and County

## Overall Dataset Characteristics

- **Total Rows**: 3,221 records
- **Data Quality**: Excellent overall data quality with minimal missing values (only 0.56% nulls in the tax amount column)
- **Geographic Coverage**: Comprehensive coverage of US counties across 52 states/territories (including District of Columbia and Puerto Rico)
- **Data Source**: 2021 5-year estimate data, suggesting this is American Community Survey (ACS) data
- **Notable Patterns**: 
  - Wide range in property tax amounts ($200 to $10,000)
  - More counties than states indicates multiple counties per state
  - Some counties appear multiple times across different states (e.g., "Platte County" exists in multiple states)

## Column Details

### county (STRING)
- **Data Type**: String/text field
- **Completeness**: 100% complete (no null values)
- **Uniqueness**: 1,955 unique county names out of 3,221 records
- **Format**: Standard county naming format with "County" suffix (e.g., "New York County", "Platte County")
- **Special Cases**: Puerto Rico uses "Municipio" instead of "County" (e.g., "Hatillo Municipio")

### state (STRING)
- **Data Type**: String/text field
- **Completeness**: 100% complete (no null values)
- **Coverage**: 52 unique states/territories including all 50 US states plus District of Columbia and Puerto Rico
- **Format**: Full state names (not abbreviations)
- **Distribution**: Varies by state size - larger states likely have more county records

### median_property_taxes_paid_by_county_2021_5_year_estimate (INT64)
- **Data Type**: Integer (whole dollar amounts)
- **Completeness**: 99.44% complete (18 null values out of 3,221 records)
- **Range**: $200 to $10,000 annually
- **Uniqueness**: 1,946 unique values, indicating some counties have identical median property tax amounts
- **Distribution**: Likely right-skewed with most counties having moderate tax amounts and fewer counties with very high taxes

## Potential Query Considerations

### Filtering Columns
- **state**: Excellent for filtering by geographic region or specific states
- **median_property_taxes_paid_by_county_2021_5_year_estimate**: Good for filtering by tax amount ranges (e.g., high-tax vs low-tax areas)
- **county**: Useful for finding specific counties, though county names may repeat across states

### Grouping/Aggregation Columns
- **state**: Primary grouping column for state-level analysis
- **Tax amount ranges**: Can be binned for distribution analysis
- **Geographic regions**: States could be grouped into regions for broader analysis

### Join Considerations
- **Primary Key**: Combination of state + county would create a unique identifier
- **Join Keys**: State and county columns can join with other geographic datasets
- **Relationship**: Many counties to one state relationship

### Data Quality Considerations
- **Handle Nulls**: 18 records have null tax amounts - decide whether to exclude or impute
- **County Name Consistency**: Be aware that county names alone are not unique (need state context)
- **Puerto Rico Handling**: Special consideration for "Municipio" vs "County" naming convention
- **Data Currency**: This is 2021 5-year estimate data, so consider temporal relevance for current analysis

## Keywords
property taxes, county taxes, state taxes, median property tax, real estate taxes, ACS data, American Community Survey, geographic analysis, tax burden, county-level data, state-level data

## Table and Column Documentation
*No table comment or column comments were provided in the source data.*