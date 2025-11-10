---
columns:
- value_domestic (FLOAT64)
- value_foreign (FLOAT64)
- year (INT64)
schema_hash: bf051adb696724a3f6c09cedf6daa16ee61f58a77fc45c85560eb273f21750cc

---
# Table Summary: annual_us_tonnage_great_lakes

## Overall Dataset Characteristics

- **Total Rows**: 69 rows
- **Time Period**: 1952 to 2020 (69 consecutive years of annual data)
- **Data Quality**: Excellent - no null values in any column
- **Data Type**: Time series data tracking annual tonnage on the Great Lakes
- **Table Context**: Named after the Edmund Fitzgerald, this appears to be historical shipping/cargo tonnage data for US Great Lakes operations, distinguishing between domestic and foreign shipping

## Column Details

### year (INT64)
- **Type**: Integer, temporal dimension
- **Null Values**: 0% (complete)
- **Range**: 1952-2020
- **Unique Values**: 69 (one record per year, no gaps)
- **Characteristics**: Sequential annual data spanning 69 years
- **Usage**: Primary time dimension for analysis, ideal for time-series queries and trend analysis

### value_domestic (FLOAT64)
- **Type**: Floating-point numeric
- **Null Values**: 0% (complete)
- **Range**: 40.47 to 162.29 (units unclear, likely millions of tons)
- **Sample Values**: 131.09, 66.40, 65.95, 98.09, 141.20
- **Characteristics**: 
  - Represents domestic shipping tonnage on Great Lakes
  - Consistently positive values
  - Wide range suggesting significant variation over time period
  - Generally higher values than foreign tonnage
- **Usage**: Primary metric for domestic shipping analysis, aggregation, and trend calculations

### value_foreign (FLOAT64)
- **Type**: Floating-point numeric
- **Null Values**: 0% (complete)
- **Range**: -8.92 to 41.62 (negative values present)
- **Sample Values**: -3.11, 15.55, 26.15, 26.94, 29.00
- **Characteristics**:
  - Represents foreign shipping tonnage on Great Lakes
  - **Notable**: Contains negative values (minimum -8.92), which may indicate:
    - Data adjustments or corrections
    - Net flow calculations
    - Data quality issues requiring investigation
  - Generally lower magnitude than domestic values
  - More volatile than domestic values
- **Usage**: Secondary metric for foreign shipping analysis; **caution needed** when interpreting negative values

## Potential Query Considerations

### Filtering Opportunities
- **By Time Period**: Year-based filters (e.g., `WHERE year BETWEEN 1980 AND 2000`)
- **By Value Range**: Filter for specific tonnage thresholds
- **By Negative Values**: Identify anomalous foreign tonnage records (`WHERE value_foreign < 0`)
- **By Era**: Pre-1975 (before Edmund Fitzgerald sinking) vs. post-1975 analysis

### Grouping/Aggregation Opportunities
- **Decade Analysis**: `GROUP BY FLOOR(year/10)*10` for decadal trends
- **Era Comparisons**: Group by custom time periods (e.g., Cold War, post-NAFTA)
- **Statistical Aggregations**: AVG, SUM, MIN, MAX calculations for both tonnage types
- **Ratio Analysis**: Calculate domestic vs. foreign shipping ratios

### Join Considerations
- **Primary Key**: Year can serve as a join key with other temporal datasets
- **Potential Joins**: Economic indicators, weather data, fuel prices, or other Great Lakes historical data
- **No Foreign Keys**: This appears to be a standalone fact table

### Data Quality Considerations for Queries
1. **Negative Values**: Always consider filtering or special handling of `value_foreign < 0` records
2. **Units Not Documented**: Clarify units (likely millions of tons) before reporting
3. **Complete Time Series**: No missing years, safe for time-series analysis without gap-filling
4. **Floating Point Precision**: Consider rounding for display purposes
5. **Context**: Queries should consider historical events (e.g., Edmund Fitzgerald sinking in 1975, economic recessions, NAFTA implementation)

### Recommended Query Patterns
- Year-over-year growth rates: `LAG()` or `LEAD()` window functions
- Moving averages: `AVG() OVER (ORDER BY year ROWS BETWEEN 4 PRECEDING AND CURRENT ROW)`
- Total tonnage: `value_domestic + value_foreign` (with consideration for negative foreign values)
- Trend analysis: Linear regression or correlation analysis over time
- Comparative periods: Pre/post specific historical events

## Keywords

Great Lakes shipping, tonnage data, maritime commerce, domestic shipping, foreign shipping, time series, annual statistics, Edmund Fitzgerald, US cargo transport, waterway freight, 1952-2020, historical shipping data, lake freighters, bulk cargo, shipping trends, maritime history, transportation statistics

## Table and Column Documentation

**Table Comment**: Not provided

**Column Comments**: Not provided

*Note: The table name references the Edmund Fitzgerald, a famous Great Lakes freighter that sank in Lake Superior in 1975. This may provide historical context for the data collection and significance of Great Lakes shipping operations.*