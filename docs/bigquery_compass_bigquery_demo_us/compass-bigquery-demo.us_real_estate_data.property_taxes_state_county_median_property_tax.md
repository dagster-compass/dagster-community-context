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

**General Description:** This table contains median property tax data at the county level across the United States, including Puerto Rico and the District of Columbia. The data represents 5-year estimates from 2021, providing a comprehensive view of property tax burdens across different geographic areas.

**Data Quality:** 
- Excellent overall data quality with minimal null values (only 0.56% in the tax amount column)
- Complete coverage for geographic identifiers (state and county)
- 1,955 unique counties across 52 states/territories

**Notable Patterns:**
- Wide variation in property taxes, ranging from $200 (Puerto Rico) to $10,000
- Geographic diversity with representation from all US states plus Puerto Rico and DC
- Some states/counties may have multiple entries or variations in naming conventions

---

## Column Details

### 1. **county** (STRING)
- **Data Type:** String/Text
- **Null Values:** 0% (complete data)
- **Unique Values:** 1,955 distinct counties
- **Format:** Full county names (e.g., "Hardin County", "Madison County", "Lares Municipio")
- **Patterns:** 
  - Most entries include "County" suffix
  - Puerto Rico uses "Municipio" designation
  - Some entries may be parishes (Louisiana) or boroughs (Alaska)
  - Examples: "DeKalb County", "Red River", "Meigs County"

### 2. **state** (STRING)
- **Data Type:** String/Text
- **Null Values:** 0% (complete data)
- **Unique Values:** 52 states/territories
- **Format:** Full state names (not abbreviations)
- **Coverage:** All 50 US states plus District of Columbia and Puerto Rico
- **Common Values:** Includes Alabama, Alaska, Arizona, Arkansas, California, Colorado, Connecticut, Delaware, District of Columbia, Florida, Georgia, Minnesota, Montana, New York, Ohio, Iowa, Puerto Rico

### 3. **median_property_taxes_paid_by_county_2021_5_year_estimate** (INT64)
- **Data Type:** Integer (whole numbers)
- **Null Values:** 0.56% (18 rows missing)
- **Unique Values:** 1,946 distinct tax amounts
- **Range:** $200 to $10,000
- **Format:** Dollar amounts represented as integers (no decimal places)
- **Statistical Characteristics:**
  - Minimum: $200 (Puerto Rico - Lares Municipio)
  - Maximum: $10,000
  - High variability indicating significant regional differences
- **Examples:** $913, $1,025, $1,612, $2,266, $2,479, $3,656

---

## Potential Query Considerations

### **Filtering Opportunities:**
- **By State:** Excellent for state-level comparisons and regional analysis
- **By Tax Range:** Filter properties by tax burden (low: <$1000, medium: $1000-$3000, high: >$3000)
- **By County:** Direct lookup of specific counties
- **NULL handling:** Consider excluding the 18 rows with null tax values for accurate calculations

### **Grouping/Aggregation Use Cases:**
- **State-level aggregations:** Calculate average, median, min, max property taxes by state
- **Regional analysis:** Group states by region (requires external mapping)
- **Tax burden categories:** Create buckets for low, medium, high tax areas
- **Top/Bottom rankings:** Identify highest and lowest tax counties/states

### **Potential Join Keys:**
- **state + county:** Composite key for joining with other demographic or real estate datasets
- **state:** Can join with state-level datasets (economic indicators, population, etc.)
- **county name:** May require standardization for joins (watch for "Parish" vs "County" variations)

### **Data Quality Considerations:**
- **NULL values:** 18 records (0.56%) have missing tax data - decide whether to exclude or handle separately
- **County name variations:** Be aware of naming inconsistencies (County, Parish, Municipio, Borough)
- **Integer precision:** Tax amounts are rounded to whole dollars; no cents available
- **5-year estimate:** Data represents an average over 5 years ending in 2021, not a single year snapshot
- **Puerto Rico data:** May have different tax structures; consider separate analysis if needed

### **Common Query Patterns:**
1. State rankings by median property tax
2. Finding counties with taxes above/below certain thresholds
3. Comparing urban vs rural counties (requires additional demographic data)
4. Regional variations in property tax burden
5. Identifying outliers (unusually high or low tax jurisdictions)

---

## Keywords

property tax, median property tax, county property tax, state property tax, real estate tax, property taxes by county, property taxes by state, tax burden, 2021 property tax, ACS 5-year estimate, American Community Survey, county-level data, geographic tax data, tax comparison, real estate, housing costs, county data, state data, US property data, municipal finance

---

## Table and Column Documentation

**Table Comment:** Not provided

**Column Comments:**
- `county`: No comment provided
- `state`: No comment provided  
- `median_property_taxes_paid_by_county_2021_5_year_estimate`: No comment provided

*Note: While no explicit documentation comments exist in the schema, the column name is self-documenting and indicates this represents median property taxes paid at the county level, using 2021 American Community Survey 5-year estimates.*