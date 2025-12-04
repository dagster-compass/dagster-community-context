---
columns:
- county (STRING)
- median_property_taxes_paid_by_county_2021_5_year_estimate (INT64)
- state (STRING)
schema_hash: ff4c4d9126f8ac82b4a56d344f64cdefa61b08063949cfbe8f312bd99b8c0a9c

---
# Table Summary: property_taxes_state_county_median_property_tax

## Overall Dataset Characteristics

**Total Rows:** 3,221

**Dataset Description:** This table contains median property tax data at the county level across the United States, based on 2021 5-year estimates. The dataset provides comprehensive coverage with 1,955 unique counties across 52 states/territories (including District of Columbia and likely other territories).

**Data Quality:** 
- High quality dataset with minimal missing data
- Only 0.56% null values in the property tax column (18 records)
- Complete coverage for state and county identifiers (0% null)
- Consistent formatting and structure

**Notable Patterns:**
- Wide range of property tax values from $200 to $10,000 annually
- Represents median values, suggesting typical property tax burden per county
- Geographic distribution spans all 50 states plus DC and territories

## Column Details

### state (STRING)
- **Data Type:** Text string
- **Null Patterns:** No null values (0.00%)
- **Distribution:** 52 unique states/territories
- **Common Values:** All US states including Alabama, Alaska, Arizona, Arkansas, California, Colorado, Connecticut, Delaware, District of Columbia, Florida, Georgia, New Hampshire, Texas, etc.
- **Format:** Full state names (not abbreviations)
- **Column Purpose:** Geographic identifier for state-level grouping

### county (STRING)
- **Data Type:** Text string
- **Null Patterns:** No null values (0.00%)
- **Distribution:** 1,955 unique counties
- **Format:** County names typically include "County" suffix (e.g., "Haywood County", "Johnson County")
- **Common Values:** Examples include Tuscaloosa County, Northumberland County, Richmond County, Hernando County, Billings County, East Feliciana
- **Column Purpose:** Geographic identifier for county-level granularity

### median_property_taxes_paid_by_county_2021_5_year_estimate (INT64)
- **Data Type:** Integer (whole numbers)
- **Null Patterns:** 0.56% null values (approximately 18 records)
- **Value Range:** $200 to $10,000
- **Distribution Examples:** 
  - Lower range: $665 (Tuscaloosa County, Alabama)
  - Mid range: $1,201-$1,601 (various counties)
  - Upper range: $5,429 (Richmond County, New York)
- **Statistical Nature:** Median values representing typical property tax burden
- **Time Period:** 5-year estimate centered on 2021
- **Column Purpose:** Primary metric for analysis of property tax burden by geography

## Potential Query Considerations

### Filtering Opportunities
- **By State:** Excellent for state-level analysis and comparisons
- **By County:** Specific county lookups and comparisons
- **By Tax Range:** Filter low/medium/high tax counties (e.g., WHERE tax > 5000 for high-tax areas)
- **Non-null Values:** Consider filtering out the 18 records with null tax values for accurate statistics

### Grouping/Aggregation Potential
- **State-level aggregation:** Calculate average, min, max property taxes by state
- **Regional analysis:** Group multiple states for regional comparisons
- **Tax bracket analysis:** Create bins/categories of tax levels (low/medium/high)
- **Statistical summaries:** Percentiles, quartiles across counties or states

### Join Considerations
- **Primary Keys:** Combination of (state, county) forms natural composite key
- **Join Candidates:** 
  - Census data tables using state/county identifiers
  - Property value tables for tax-to-value ratio analysis
  - Demographic tables for tax burden vs. income analysis
  - Geographic/mapping tables for spatial analysis
- **Foreign Key Pattern:** State and county names suitable for joining with other geographic datasets

### Data Quality Considerations
- **Null Handling:** Account for 18 records (0.56%) with null tax values in aggregations
- **Outlier Analysis:** The $200-$10,000 range suggests potential outliers at both extremes
- **Name Matching:** County names include "County" suffix - may need string manipulation for joins
- **Estimation Period:** Data represents 5-year estimates, not single-year snapshots
- **Median vs. Mean:** Remember this is median data - half of properties pay more, half pay less

## Keywords

property tax, real estate tax, county taxes, state taxes, median tax, property taxes by county, US counties, geographic tax data, 2021 tax data, tax burden analysis, real estate data, census data, county-level data, state-level aggregation, tax comparison, housing costs, property assessment, local taxation, fiscal data, American Community Survey, ACS estimates

## Table and Column Documentation

**Table Comment:** Not provided in the analysis report.

**Column Comments:** Not provided in the analysis report.

**Column Name Interpretation:**
- `median_property_taxes_paid_by_county_2021_5_year_estimate` - Self-documenting name indicating this represents the median amount of property taxes paid, aggregated at the county level, based on a 5-year estimate period centered on 2021 (likely from American Community Survey data)