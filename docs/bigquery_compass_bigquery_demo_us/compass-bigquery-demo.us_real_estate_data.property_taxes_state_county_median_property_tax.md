---
columns:
- county (STRING)
- median_property_taxes_paid_by_county_2021_5_year_estimate (INT64)
- state (STRING)
schema_hash: ff4c4d9126f8ac82b4a56d344f64cdefa61b08063949cfbe8f312bd99b8c0a9c

---
# Table Summary: Property Taxes by State and County

## Overall Dataset Characteristics

**Total Rows:** 3,221

**General Description:** This table contains median property tax payment data at the county level across the United States, based on 5-year estimates ending in 2021. The dataset provides comprehensive coverage of US counties with their corresponding median property tax payments.

**Data Quality:** 
- Excellent overall quality with minimal null values
- Only 0.56% null values in the property tax column (approximately 18 rows)
- No null values in geographical identifiers (state and county)
- Complete geographic coverage including all 50 states plus District of Columbia and Puerto Rico (52 total)

**Notable Patterns:**
- Property tax values range from $200 to $10,000 annually
- 1,955 unique counties represented out of 3,221 total rows, suggesting some counties may have duplicate entries or the data includes county-equivalents
- Geographic distribution spans entire United States including territories

## Column Details

### state (STRING)
- **Purpose:** Identifies the US state or territory
- **Data Type:** STRING (text)
- **Completeness:** 100% populated (0% null)
- **Unique Values:** 52 states/territories
- **Values Include:** All 50 US states, District of Columbia, and Puerto Rico
- **Sample Values:** Puerto Rico, Mississippi, Indiana, Alabama, Alaska, Arizona, etc.
- **Format:** Full state names (not abbreviations)

### county (STRING)
- **Purpose:** Identifies the specific county within each state
- **Data Type:** STRING (text)
- **Completeness:** 100% populated (0% null)
- **Unique Values:** 1,955 distinct counties
- **Format:** County name followed by " County" suffix (e.g., "Screven County", "Ward County", "Summit County")
- **Note:** Some county names may appear across multiple states (e.g., Summit County exists in multiple states)

### median_property_taxes_paid_by_county_2021_5_year_estimate (INT64)
- **Purpose:** Median annual property tax payment for the county
- **Data Type:** INT64 (integer)
- **Completeness:** 99.44% populated (0.56% null)
- **Value Range:** $200 to $10,000
- **Unique Values:** 1,946 distinct values
- **Sample Values:** $942, $1,209, $1,513, $1,250, $2,823, $1,234
- **Statistical Note:** Based on 5-year American Community Survey estimates ending in 2021
- **Unit:** US Dollars (annual payment)

## Potential Query Considerations

### Filtering Recommendations:
- **state**: Excellent for filtering by geographic region; use exact state names
- **county**: Can filter specific counties, but be aware of duplicate county names across states
- **median_property_taxes_paid_by_county_2021_5_year_estimate**: Good for range-based filters (e.g., high-tax vs low-tax counties)
  - Consider filtering out NULL values when performing calculations
  - Useful thresholds: < $1,000 (low), $1,000-$3,000 (moderate), > $3,000 (high)

### Grouping/Aggregation Opportunities:
- **By State**: Calculate state-level averages, min/max property taxes
- **By Tax Ranges**: Group counties into tax brackets for distribution analysis
- **Regional Analysis**: Combine with external region mappings for multi-state analysis
- **Statistical Functions**: AVG, MIN, MAX, MEDIAN, PERCENTILE functions work well with the tax column

### Join Key Considerations:
- **Primary Key:** Combination of (state, county) forms a composite unique identifier
- **Join Potential:** Can join with other demographic, economic, or real estate datasets using state/county combination
- **Warning:** County names alone are NOT unique (multiple states have counties with same names)
- **Recommendation:** Always use both state AND county for joins

### Data Quality Considerations:
1. **NULL Handling:** 18 rows (~0.56%) have null property tax values - decide whether to exclude or handle separately
2. **Outliers:** Values at extreme ends ($200 or $10,000) may warrant investigation
3. **County Naming:** Ensure consistent formatting when joining (all include "County" suffix)
4. **Time Sensitivity:** Data represents 5-year estimates ending 2021; may not reflect current conditions
5. **Geographic Completeness:** Not all US counties may be represented (1,955 unique vs ~3,000+ actual US counties)

## Keywords

property tax, real estate tax, county tax, state tax, median tax, tax assessment, property assessment, US counties, American Community Survey, ACS 2021, 5-year estimate, tax burden, local tax, geographic tax data, state-level tax, county-level tax, tax analysis, property taxation, real estate data, US real estate, tax statistics, local government revenue, housing costs

## Table and Column Documentation

**Table Comment:** Not provided

**Column Comments:** Not provided

**Note:** The lengthy column name `median_property_taxes_paid_by_county_2021_5_year_estimate` is self-documenting, indicating this is median property tax data at the county level from 2021 5-year ACS estimates.