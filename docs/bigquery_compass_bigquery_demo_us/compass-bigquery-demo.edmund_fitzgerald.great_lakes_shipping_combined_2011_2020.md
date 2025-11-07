---
columns:
- asphalt_tar_pitch (FLOAT64)
- cement_concrete (FLOAT64)
- coal_lignite (FLOAT64)
- petroleum_coke (FLOAT64)
- salt (FLOAT64)
- sand_gravel (FLOAT64)
- slag (FLOAT64)
- value_iron_ore (FLOAT64)
- value_limestone (FLOAT64)
- wheat (FLOAT64)
- year (INT64)
schema_hash: 4f9db89dc501bb2fb2a50d3498e442da1471a165111c08db72869fd67986ad57

---
# Comprehensive Data Summary: Great Lakes Shipping Combined 2011-2020

## Overall Dataset Characteristics

**Total Rows:** 11 rows (representing years 2011-2021, though the table name suggests 2011-2020)

**General Data Quality:**
- This is a high-quality, small time-series dataset with minimal missing data
- Only 4 columns have null values: `slag`, `coal_lignite`, `salt`, and `value_iron_ore`, and `value_limestone` - all with exactly 9.09% (1 row) missing
- All numeric values are FLOAT64 type except for `year` (INT64)
- Data appears to represent shipping volumes or rates for various commodities on the Great Lakes

**Notable Patterns:**
- The dataset shows annual aggregated data for Great Lakes shipping commodities
- Values appear to be normalized or represent rates per unit (possibly millions of tons or similar)
- Some commodities show negative values (wheat, petroleum_coke), suggesting possible year-over-year changes or adjusted metrics
- Iron ore and limestone show the highest absolute values (44-55 range for iron ore, 18-22 range for limestone)
- Wheat shows the most variation including negative values, suggesting volatility in that commodity

**Table Comment:** Not provided

---

## Column-by-Column Analysis

### **year** (INT64)
- **Purpose:** Time dimension - primary key for annual data
- **Range:** 2011 to 2021 (11 consecutive years)
- **Data Quality:** Complete (0% null), unique values for each row
- **Comment:** Not provided

### **wheat** (FLOAT64)
- **Range:** -0.35 to 2.13
- **Data Quality:** Complete (0% null)
- **Pattern:** Shows both negative and positive values, suggesting this may represent year-over-year changes or normalized deviations from a baseline
- **Distribution:** Most values are negative or near zero, with one significant positive outlier (2.13)
- **Comment:** Not provided

### **sand_gravel** (FLOAT64)
- **Range:** 1.11 to 3.73
- **Data Quality:** Complete (0% null)
- **Pattern:** All positive values, relatively stable with most values between 1-3
- **Distribution:** Fairly consistent across years with one high value (3.73)
- **Comment:** Not provided

### **cement_concrete** (FLOAT64)
- **Range:** 4.13 to 5.34
- **Data Quality:** Complete (0% null)
- **Pattern:** All positive values, showing the most stability among all commodities
- **Distribution:** Tightly clustered between 4-5, indicating consistent shipping volumes
- **Comment:** Not provided

### **slag** (FLOAT64)
- **Range:** 0.26 to 0.92
- **Data Quality:** 9.09% null (1 missing value)
- **Pattern:** All positive values when present, lower magnitude than most other commodities
- **Distribution:** Relatively low values, ranging from 0.26 to 0.92
- **Comment:** Not provided

### **coal_lignite** (FLOAT64)
- **Range:** 7.35 to 23.08
- **Data Quality:** 9.09% null (1 missing value)
- **Pattern:** All positive values, highly variable
- **Distribution:** Wide range suggesting significant year-to-year fluctuations in coal shipping
- **Comment:** Not provided

### **petroleum_coke** (FLOAT64)
- **Range:** -0.09 to 3.93
- **Data Quality:** Complete (0% null)
- **Pattern:** Mostly positive with two slightly negative values
- **Distribution:** Variable, with most values under 1.0 but some reaching 3.93
- **Comment:** Not provided

### **salt** (FLOAT64)
- **Range:** 3.71 to 6.33
- **Data Quality:** 9.09% null (1 missing value)
- **Pattern:** All positive values when present
- **Distribution:** Mid-range values, relatively consistent between 3.7-6.3
- **Comment:** Not provided

### **asphalt_tar_pitch** (FLOAT64)
- **Range:** 0.78 to 5.19
- **Data Quality:** Complete (0% null)
- **Pattern:** All positive values
- **Distribution:** Variable, ranging from 0.78 to 5.19, suggesting fluctuating demand
- **Comment:** Not provided

### **value_limestone** (FLOAT64)
- **Range:** 18.00 to 22.44
- **Data Quality:** 9.09% null (1 missing value)
- **Pattern:** All positive values, highest absolute values along with iron ore
- **Distribution:** Consistently high values, suggesting limestone is a major shipping commodity
- **Comment:** Not provided

### **value_iron_ore** (FLOAT64)
- **Range:** 44.99 to 55.75
- **Data Quality:** 9.09% null (1 missing value)
- **Pattern:** All positive values, the highest absolute values in the dataset
- **Distribution:** Consistently very high values (45-56 range), indicating iron ore is the dominant commodity
- **Comment:** Not provided

---

## Potential Query Considerations

### **Filtering Columns:**
- **year:** Primary filter for time-based queries (e.g., specific years, year ranges)
- **All commodity columns:** Good for threshold-based filtering (e.g., years when iron ore exceeded 50)

### **Grouping/Aggregation Columns:**
- **year:** Natural grouping dimension for temporal analysis
- Limited grouping potential due to small dataset and lack of categorical dimensions
- Aggregations would primarily involve calculating averages, sums, min/max across years

### **Join Keys:**
- **year:** Could join with other time-series tables (economic indicators, weather data, etc.)
- No other obvious foreign keys present

### **Data Quality Considerations:**

1. **Missing Values:** Queries involving `slag`, `coal_lignite`, `salt`, `value_limestone`, or `value_iron_ore` should handle nulls appropriately:
   - Use `IS NOT NULL` filters when nulls would affect calculations
   - Consider `COALESCE()` or `IFNULL()` for default values
   - One year (likely 2011 or 2021) is missing data for these five columns

2. **Negative Values:** Wheat and petroleum_coke can have negative values:
   - These likely represent declines or adjusted metrics
   - Avoid absolute value assumptions in aggregations
   - Consider whether negative values should be excluded for certain analyses

3. **Small Dataset:** With only 11 rows:
   - Statistical analyses will have limited power
   - Outlier detection should be used cautiously
   - Trend analysis is possible but limited by sample size

4. **Value Interpretation:** All values appear to be normalized or rate-based:
   - Column names with "value_" prefix (limestone, iron ore) may represent monetary value vs. volume
   - Consider the measurement unit when interpreting results

---

## Keywords

Great Lakes, shipping, commodities, maritime transport, bulk cargo, iron ore, limestone, coal, cement, wheat, sand, gravel, salt, petroleum coke, asphalt, slag, time series, annual data, 2011-2020, waterborne commerce, inland waterways, freight transport, commodity volumes, shipping rates, Great Lakes economy, bulk materials, industrial shipping

---

## Table and Column Documentation

**Table Comment:** Not provided in the analysis report

**Column Comments:** No column-level comments were provided in the analysis report