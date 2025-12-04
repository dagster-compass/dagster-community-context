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
# Table Summary: great_lakes_shipping_combined_2011_2020

## Overall Dataset Characteristics

**Total Rows:** 11 rows (appears to be annual data from 2011-2021)

**General Data Quality:**
- Very small dataset with 11 rows representing 11 consecutive years
- Some columns have 9.09% null values (1 missing row each), suggesting potential data collection issues for year 2021
- All numeric columns are FLOAT64 except year (INT64)
- Data appears to represent shipping volumes or metrics for various commodities on the Great Lakes

**Notable Patterns:**
- Dataset spans 2011-2021 (11 years of annual data)
- Values appear to be normalized or scaled metrics rather than raw tonnage
- Four columns (`slag`, `coal_lignite`, `salt`, `value_limestone`, `value_iron_ore`) each have exactly 1 null value
- Higher-value commodities (iron ore: 45-56 range, limestone: 18-22 range) vs lower-value materials (wheat: -0.35 to 2.13)

**Table Comment:** Not provided

## Column Details

### year (INT64)
- **Type:** Integer, serves as primary temporal identifier
- **Range:** 2011 to 2021 (inclusive, 11 consecutive years)
- **Null Values:** None (0%)
- **Characteristics:** Sequential annual data, likely the primary key
- **Column Comment:** Not provided

### wheat (FLOAT64)
- **Type:** Normalized float values
- **Range:** -0.354 to 2.133
- **Null Values:** None (0%)
- **Distribution:** Mostly small values near zero, with one notable outlier at 2.133
- **Characteristics:** Contains negative values suggesting this may be a standardized/z-score metric
- **Column Comment:** Not provided

### sand_gravel (FLOAT64)
- **Type:** Normalized float values
- **Range:** 1.113 to 3.731
- **Null Values:** None (0%)
- **Distribution:** Consistently positive values, relatively stable range
- **Characteristics:** All values positive, suggesting steady shipping volumes
- **Column Comment:** Not provided

### cement_concrete (FLOAT64)
- **Type:** Normalized float values
- **Range:** 4.132 to 5.343
- **Null Values:** None (0%)
- **Distribution:** Tightly clustered between 4-5.5
- **Characteristics:** Most stable commodity with narrow range
- **Column Comment:** Not provided

### slag (FLOAT64)
- **Type:** Normalized float values
- **Range:** 0.256 to 0.919
- **Null Values:** 1 row (9.09%)
- **Distribution:** Relatively low values compared to other commodities
- **Characteristics:** Missing one year of data; all values less than 1
- **Column Comment:** Not provided

### petroleum_coke (FLOAT64)
- **Type:** Normalized float values
- **Range:** -0.090 to 3.930
- **Null Values:** None (0%)
- **Distribution:** Wide range with one significant outlier at 3.930
- **Characteristics:** Mostly low values with one exceptional year
- **Column Comment:** Not provided

### coal_lignite (FLOAT64)
- **Type:** Normalized float values
- **Range:** 7.346 to 23.084
- **Null Values:** 1 row (9.09%)
- **Distribution:** Higher values, significant variation (range of ~16 units)
- **Characteristics:** Major commodity with substantial fluctuation year-to-year
- **Column Comment:** Not provided

### salt (FLOAT64)
- **Type:** Normalized float values
- **Range:** 3.708 to 6.335
- **Null Values:** 1 row (9.09%)
- **Distribution:** Mid-range values, moderate variation
- **Characteristics:** Consistent presence as a shipping commodity
- **Column Comment:** Not provided

### asphalt_tar_pitch (FLOAT64)
- **Type:** Normalized float values
- **Range:** 0.783 to 5.187
- **Null Values:** None (0%)
- **Distribution:** Wide range, variable shipping volumes
- **Characteristics:** Complete data across all years
- **Column Comment:** Not provided

### value_limestone (FLOAT64)
- **Type:** Normalized float values (possibly value rather than volume)
- **Range:** 18.003 to 22.438
- **Null Values:** 1 row (9.09%)
- **Distribution:** High values, relatively tight clustering
- **Characteristics:** "value_" prefix suggests this may be monetary value rather than volume
- **Column Comment:** Not provided

### value_iron_ore (FLOAT64)
- **Type:** Normalized float values (possibly value rather than volume)
- **Range:** 44.988 to 55.749
- **Null Values:** 1 row (9.09%)
- **Distribution:** Highest values in the dataset, moderate variation
- **Characteristics:** "value_" prefix suggests monetary value; iron ore appears to be most valuable commodity
- **Column Comment:** Not provided

## Potential Query Considerations

### Filtering Opportunities:
- **year:** Primary filter for time-based queries (2011-2021)
- **Thresholds:** Filter by commodity volumes above/below certain thresholds
- **Null handling:** Be aware that 4 columns have one missing value each

### Grouping/Aggregation Potential:
- **Time-based:** Group by year for trends analysis
- **Commodity comparison:** Compare average values across different commodities
- **Decade analysis:** Early 2010s vs late 2010s vs 2020+

### Join Key Candidates:
- **year:** Can be used to join with other Great Lakes shipping tables or economic indicators
- No obvious foreign keys to other tables based on column names

### Data Quality Considerations:
1. **Missing Data:** Four columns have exactly 1 null value (9.09%), likely the same year (possibly 2021)
2. **Negative Values:** `wheat` and `petroleum_coke` have negative values, suggesting normalized/standardized metrics rather than raw volumes
3. **Scale Differences:** Wide variation in value ranges across commodities (0.26-55.75) suggests different measurement scales
4. **Small Sample Size:** Only 11 rows limits statistical analysis capabilities
5. **Metric Interpretation:** Unclear if values represent volume, value, or normalized metrics

### Recommended Query Patterns:
- Time series analysis with year as x-axis
- Year-over-year percent change calculations
- Commodity correlation analysis
- Handle nulls explicitly with `IS NOT NULL` or `COALESCE`
- Consider normalizing across commodities for fair comparison

## Keywords

Great Lakes, shipping, commodities, maritime transport, bulk cargo, wheat, sand, gravel, cement, concrete, slag, petroleum coke, coal, lignite, salt, asphalt, tar, pitch, limestone, iron ore, annual data, time series, 2011-2020, cargo volumes, freight, tonnage, lake carriers

## Table and Column Documentation

**Table Comment:** Not provided

**Column Comments:** None of the columns have associated comments in the schema.