---
columns:
- value_domestic (FLOAT64)
- value_foreign (FLOAT64)
- year (INT64)
schema_hash: bf051adb696724a3f6c09cedf6daa16ee61f58a77fc45c85560eb273f21750cc

---
# Table Summary: compass-bigquery-demo.edmund_fitzgerald.annual_us_tonnage_great_lakes

## Overall Dataset Characteristics

**Total Rows:** 69

**Time Period Coverage:** 1952-2020 (69 consecutive years of annual data)

**Data Quality:** 
- Excellent completeness - 0% null values across all columns
- Continuous annual time series with no gaps
- All columns contain unique values for each year, suggesting year-level aggregated metrics

**General Observations:**
- This appears to be a historical dataset tracking annual cargo tonnage shipped through the Great Lakes
- The table name references the Edmund Fitzgerald, the famous Great Lakes freighter that sank in 1975
- Data distinguishes between domestic and foreign shipping tonnage
- Foreign tonnage shows negative values in the minimum range (-8.92), which may indicate data quality issues, directional flow adjustments, or specific accounting methodologies

**Notable Patterns:**
- Domestic tonnage values are significantly higher than foreign tonnage (roughly 4-10x larger)
- Domestic tonnage ranges from ~40 to ~162 million tons (estimated units)
- Foreign tonnage ranges from approximately -9 to ~42 million tons

## Column Details

### year (INT64)
**Type:** Integer, 4-digit year format
**Range:** 1952 to 2020
**Null Values:** None (0%)
**Unique Values:** 69 (one per row)
**Pattern:** Consecutive annual data points

**Characteristics:**
- Primary temporal dimension for the dataset
- Covers nearly 7 decades of shipping activity
- Includes the notable year 1975 (Edmund Fitzgerald sinking)

### value_domestic (FLOAT64)
**Type:** Floating-point decimal
**Range:** 40.47 to 162.29
**Null Values:** None (0%)
**Unique Values:** 69 (distinct value per year)
**Sample Values:** 146.54, 122.65, 56.77, 132.97, 141.20

**Characteristics:**
- Represents domestic cargo tonnage (likely in millions of tons)
- Shows significant variation, suggesting economic cycles or structural changes in Great Lakes shipping
- Higher values appear in earlier decades (1960s-1970s based on samples)
- Recent years (2010s) show lower values around 40-66 million tons
- Likely represents intra-US cargo movement through the Great Lakes

### value_foreign (FLOAT64)
**Type:** Floating-point decimal
**Range:** -8.92 to 41.62
**Null Values:** None (0%)
**Unique Values:** 69 (distinct value per year)
**Sample Values:** 28.50, 13.54, 36.00, 29.00, 26.15

**Characteristics:**
- Represents foreign cargo tonnage (likely in millions of tons)
- Contains at least one negative value (-8.92), requiring investigation for query logic
- Generally lower magnitude than domestic tonnage
- Likely represents international cargo (US-Canada trade through Great Lakes)
- More volatile than domestic values

## Potential Query Considerations

### Optimal Filtering Columns:
- **year**: Primary filter for time-based queries
  - Range queries (e.g., `WHERE year BETWEEN 1970 AND 1980`)
  - Specific year lookups (e.g., `WHERE year = 1975`)
  - Decade-based filtering (e.g., `WHERE year >= 2000`)

### Optimal Grouping/Aggregation:
- **year**: Natural grouping dimension, though already at annual granularity
- **Calculated decades**: `FLOOR(year/10)*10` for decade-level analysis
- **Era-based grouping**: Pre/post-1975 (Edmund Fitzgerald era), pre/post-2000, etc.

### Aggregation Opportunities:
- Sum, average, min, max operations on value columns
- Total tonnage: `value_domestic + value_foreign`
- Ratio analysis: `value_domestic / value_foreign`
- Year-over-year growth calculations using LAG/LEAD functions
- Moving averages for trend analysis

### Join Key Considerations:
- **year**: Natural join key for other time-series datasets
- Could join with economic indicators, weather data, infrastructure events, or other Great Lakes shipping tables

### Data Quality Considerations:

1. **Negative Values in value_foreign:**
   - Queries should handle or filter negative values appropriately
   - May need conditional logic: `WHERE value_foreign >= 0`
   - Investigate meaning before aggregating

2. **Unit Assumptions:**
   - Units are not explicitly stated; likely millions of tons based on value ranges
   - Document unit assumptions in query comments

3. **Trend Analysis:**
   - Clear declining trend in domestic shipping visible in sample data
   - Time series analysis should account for structural changes in shipping industry

4. **Missing Context:**
   - No categorical dimensions (e.g., cargo type, port, vessel type)
   - Additional context may exist in related tables

## Keywords

Great Lakes shipping, cargo tonnage, annual statistics, maritime commerce, domestic freight, foreign trade, US-Canada trade, Edmund Fitzgerald, time series data, 1952-2020, shipping trends, waterborne commerce, inland waterways, bulk cargo, historical shipping data, freight volume, transportation statistics

## Table and Column Documentation

**Table Comment:** Not provided

**Column Comments:**
- `year`: Not provided
- `value_domestic`: Not provided
- `value_foreign`: Not provided

*Note: No explicit documentation comments are available for this table or its columns. The table name suggests a connection to Edmund Fitzgerald and Great Lakes tonnage data.*