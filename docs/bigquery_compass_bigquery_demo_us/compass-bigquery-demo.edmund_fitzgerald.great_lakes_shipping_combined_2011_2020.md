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
# Table Documentation Summary: great_lakes_shipping_combined_2011_2020

## Overall Dataset Characteristics

**Total Rows:** 11

**Dataset Description:** This table contains aggregated shipping data for various commodities transported across the Great Lakes from 2011-2020 (despite the table name, data appears to extend through 2021 based on year range). The dataset represents annual measurements of shipping volumes for different cargo types including bulk materials, minerals, and agricultural products.

**Data Quality:** 
- Generally high quality with most columns having complete data
- Four columns (slag, coal_lignite, salt, value_iron_ore, value_limestone) have approximately 9.09% null values (1 row missing)
- Small dataset size (11 rows) suggests annual aggregation
- All numeric columns appear to contain ratio or normalized values rather than raw tonnage

**Notable Patterns:**
- Data spans consecutive years from 2011-2021
- Most values appear to be normalized or calculated metrics (many floating-point ratios/percentages)
- Iron ore and limestone show the highest absolute values (44-56 and 18-22 ranges respectively)
- Several commodities show negative values (wheat, petroleum_coke), suggesting possible year-over-year change calculations or standardized scores

## Column Details

### year (INT64)
- **Type:** Integer, primary temporal dimension
- **Range:** 2011 to 2021
- **Nulls:** None (0%)
- **Pattern:** Consecutive annual data
- **Comment:** None provided
- **Usage:** Primary key candidate, essential for time-series analysis

### slag (FLOAT64)
- **Type:** Decimal/Float
- **Range:** 0.256 to 0.919
- **Nulls:** 9.09% (1 missing value)
- **Distribution:** Moderate variation, all positive values between 0-1
- **Comment:** None provided
- **Usage:** Likely represents shipping volume proportion or efficiency metric for slag (steel industry byproduct)

### wheat (FLOAT64)
- **Type:** Decimal/Float
- **Range:** -0.354 to 2.133
- **Nulls:** None (0%)
- **Distribution:** Includes negative values, suggesting normalized/standardized measurements
- **Comment:** None provided
- **Usage:** Agricultural commodity metric, possibly year-over-year change or z-score

### cement_concrete (FLOAT64)
- **Type:** Decimal/Float
- **Range:** 4.132 to 5.343
- **Nulls:** None (0%)
- **Distribution:** Relatively stable, clustered around 4-5 range
- **Comment:** None provided
- **Usage:** Construction materials shipping metric

### sand_gravel (FLOAT64)
- **Type:** Decimal/Float
- **Range:** 1.113 to 3.731
- **Nulls:** None (0%)
- **Distribution:** Moderate spread, all positive values
- **Comment:** None provided
- **Usage:** Aggregate materials shipping volume indicator

### petroleum_coke (FLOAT64)
- **Type:** Decimal/Float
- **Range:** -0.090 to 3.930
- **Nulls:** None (0%)
- **Distribution:** Wide range including small negative values
- **Comment:** None provided
- **Usage:** Petroleum industry byproduct shipping metric

### asphalt_tar_pitch (FLOAT64)
- **Type:** Decimal/Float
- **Range:** 0.783 to 5.187
- **Nulls:** None (0%)
- **Distribution:** Wide range, all positive values
- **Comment:** None provided
- **Usage:** Petroleum-based construction materials metric

### salt (FLOAT64)
- **Type:** Decimal/Float
- **Range:** 3.708 to 6.335
- **Nulls:** 9.09% (1 missing value)
- **Distribution:** Moderate range, higher absolute values
- **Comment:** None provided
- **Usage:** Bulk mineral commodity shipping indicator

### coal_lignite (FLOAT64)
- **Type:** Decimal/Float
- **Range:** 7.346 to 23.084
- **Nulls:** 9.09% (1 missing value)
- **Distribution:** Highest variability, largest absolute values
- **Comment:** None provided
- **Usage:** Energy commodity metric, shows significant year-to-year variation

### value_iron_ore (FLOAT64)
- **Type:** Decimal/Float
- **Range:** 44.988 to 55.749
- **Nulls:** 9.09% (1 missing value)
- **Distribution:** Highest absolute values in dataset, relatively stable
- **Comment:** None provided
- **Usage:** Primary iron ore shipping value/volume - likely most economically significant commodity

### value_limestone (FLOAT64)
- **Type:** Decimal/Float
- **Range:** 18.003 to 22.438
- **Nulls:** 9.09% (1 missing value)
- **Distribution:** Moderate range, second-highest absolute values
- **Comment:** None provided
- **Usage:** Industrial mineral shipping metric

## Table and Column Documentation

**Table Comment:** None provided

**Column Comments:** No column-level comments are present in the schema.

## Query Considerations

### Filtering Recommendations:
- **year:** Ideal for time-range filters (WHERE year BETWEEN 2015 AND 2020)
- **Complete data columns:** wheat, cement_concrete, sand_gravel, petroleum_coke, asphalt_tar_pitch have no nulls and are safe for all operations
- **Nullable columns:** Consider NULL handling for slag, coal_lignite, salt, value_iron_ore, value_limestone

### Grouping/Aggregation Opportunities:
- **Temporal analysis:** GROUP BY year for trend analysis
- **Year-over-year comparisons:** Use LAG/LEAD window functions with year ordering
- **Commodity comparisons:** Pivot or aggregate across commodity columns
- **Statistical analysis:** AVG, STDDEV calculations work well given normalized nature of data

### Potential Relationships:
- **Primary key:** year appears to be unique identifier (11 rows, 11 years)
- **No explicit foreign keys:** This appears to be a fact table without obvious dimensional relationships
- **Commodity correlations:** Multiple commodity columns may have inter-relationships (e.g., coal_lignite with value_iron_ore for steel production)

### Data Quality Considerations:
- **Missing data pattern:** The same row appears to be missing across multiple columns (9.09% = 1/11 rows)
- **Scale differences:** Queries comparing commodities must account for different value ranges (wheat: -0.35 to 2.13 vs coal_lignite: 7.35 to 23.08)
- **Negative values:** Some commodities have negative values - verify interpretation before aggregation
- **Small sample size:** 11 rows limits statistical analysis and requires careful interpretation of trends
- **NULL handling:** Use COALESCE or WHERE IS NOT NULL for columns with missing data

### Keywords:
Great Lakes, shipping, maritime, cargo, bulk commodities, freight, iron ore, limestone, coal, lignite, slag, wheat, cement, concrete, sand, gravel, petroleum coke, salt, asphalt, tar, pitch, transportation, logistics, 2011-2020, annual data, time series, commodity volumes, trade statistics, waterborne commerce, inland waterways, steel industry, construction materials, energy commodities, agricultural shipping, mineral resources, Edmund Fitzgerald