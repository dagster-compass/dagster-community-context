---
columns:
- county (STRING)
- median_property_taxes_paid_by_county_2021_5_year_estimate (INT64)
- state (STRING)
schema_hash: ff4c4d9126f8ac82b4a56d344f64cdefa61b08063949cfbe8f312bd99b8c0a9c

---
# Data Summary: Property Taxes by State and County

## Overall Dataset Characteristics

**Total Records:** 3,221 rows

**Dataset Description:** This table contains median property tax information at the county level across the United States, based on 2021 5-year estimates. The dataset provides comprehensive coverage of US counties with property tax data.

**Data Quality:** High quality overall with minimal missing data (only 0.56% nulls in the median property tax column). The dataset appears complete with no nulls in geographic identifiers (state and county).

**Notable Patterns:**
- Coverage spans 52 states/territories (including DC and US territories)
- 1,955 unique counties represented (approximately 60% of US counties)
- Property tax range is substantial: $200 to $10,000, indicating significant geographic variation in property tax burdens
- The 5-year estimate methodology suggests aggregated/smoothed data rather than point-in-time snapshots

## Column Details

### state (STRING)
**Data Type:** String (categorical)
**Completeness:** 100% (no nulls)
**Cardinality:** 52 unique values
**Description:** US state or territory names in full text format (e.g., "Alabama", "California", "District of Columbia")
**Sample Values:** Pennsylvania, Illinois, Kansas, Alabama, Alaska, Arizona, Arkansas, California, Colorado, Connecticut, Delaware, Florida
**Usage Notes:** Standardized state names; includes DC and likely US territories to reach 52 values

### county (STRING)
**Data Type:** String (categorical)
**Completeness:** 100% (no nulls)
**Cardinality:** 1,955 unique values
**Description:** County names including the word "County" suffix (e.g., "Sherman County", "Steuben County")
**Sample Values:** Aurora County, Cherry County, Manassas Park, Sherman County, Steuben County, Preble County, Lorain County, Sedgwick County
**Format Pattern:** Generally follows "[Name] County" format, though exceptions exist (e.g., "Manassas Park")
**Usage Notes:** County names may not be globally unique; must be combined with state for unique identification

### median_property_taxes_paid_by_county_2021_5_year_estimate (INT64)
**Data Type:** Integer (numeric)
**Completeness:** 99.44% (0.56% nulls = ~18 records with missing values)
**Cardinality:** 1,946 unique values
**Range:** $200 to $10,000
**Sample Values:** 1,674, 644, 1,746, 1,784, 1,021, 1,617, 2,687, 2,007
**Distribution Characteristics:** 
- Wide range suggests significant geographic variation
- Values appear to be in whole dollars (no cents)
- The 5-year estimate indicates this is Census Bureau data (likely American Community Survey)
**Usage Notes:** NULL values represent counties where data was unavailable or unreliable; users should handle nulls appropriately in calculations

## Potential Query Considerations

### Recommended for Filtering:
- **state:** Excellent for geographic filtering; use for state-level analysis or multi-state comparisons
- **median_property_taxes_paid_by_county_2021_5_year_estimate:** Good for range queries (e.g., counties with taxes above/below thresholds)

### Recommended for Grouping/Aggregation:
- **state:** Primary grouping dimension for state-level rollups (AVG, MIN, MAX, COUNT of counties per state)
- Combined **state + county:** For ensuring unique geographic identification

### Join Key Considerations:
- **Primary Key:** Combination of (state, county) provides unique record identification
- **Join Potential:** Can join with other geographic datasets using state and/or county fields
- **Caution:** County names alone are NOT unique (e.g., "Washington County" exists in multiple states)

### Data Quality Considerations:
- Account for 18 records (~0.56%) with NULL median property tax values in aggregations
- Use COALESCE or WHERE clauses to handle nulls when computing averages or comparisons
- State names are spelled out (not abbreviated), so joins requiring state codes will need mapping
- Property tax values are estimates, not exact amounts; appropriate for comparative analysis but not precise tax calculations
- Time period is 5-year estimate ending 2021; data may not reflect current conditions for queries run in later years

### Analytical Use Cases:
- **Ranking queries:** Identify highest/lowest property tax counties or states
- **Distribution analysis:** Percentile calculations, histogram groupings
- **Geographic comparisons:** State-to-state or regional comparisons
- **Outlier detection:** Identify counties with unusual property tax patterns
- **Coverage analysis:** Identify states/regions with missing data

## Keywords

property tax, real estate tax, county tax, state tax, median taxes, US counties, American Community Survey, ACS, Census data, 2021 estimates, geographic data, tax burden, local taxes, county-level data, state-level aggregation, real estate economics, housing costs, property assessment, tax analysis, geographic analysis

## Table and Column Documentation

**Table Comment:** Not provided in the analysis report

**Column Comments:** Not provided in the analysis report

The column name `median_property_taxes_paid_by_county_2021_5_year_estimate` is self-documenting, indicating this represents the median (middle value) of property taxes paid within each county, based on a 5-year data collection period ending in 2021, consistent with American Community Survey methodology.