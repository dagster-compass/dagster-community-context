---
columns:
- value_domestic (FLOAT64)
- value_foreign (FLOAT64)
- year (INT64)
schema_hash: bf051adb696724a3f6c09cedf6daa16ee61f58a77fc45c85560eb273f21750cc

---
# Table Summary: compass-bigquery-demo.edmund_fitzgerald.annual_us_tonnage_great_lakes

## Overall Dataset Characteristics

- **Total Rows**: 69 records
- **Time Period**: Complete annual dataset covering 1952 to 2020 (69 consecutive years)
- **Data Quality**: Excellent - no null values in any column (0% null rate across all fields)
- **Dataset Type**: Time series data tracking annual tonnage metrics for Great Lakes shipping
- **Notable Pattern**: The table appears to track two types of tonnage values (domestic and foreign) over nearly 7 decades, likely representing cargo volumes in millions of tons

### Key Observations
- **Domestic Tonnage**: Shows significant variation (40.47 to 162.29), suggesting major changes in domestic shipping activity over the decades
- **Foreign Tonnage**: Includes negative values (-8.92 to 41.62), which may indicate net exports/imports or year-over-year changes rather than absolute volumes
- **Historical Context**: The table name references the Edmund Fitzgerald, the famous Great Lakes freighter that sank in 1975, suggesting this data relates to Great Lakes maritime commerce

## Column Details

### year (INT64)
- **Data Type**: Integer
- **Null Values**: None (0%)
- **Range**: 1952 to 2020
- **Unique Values**: 69 (one record per year)
- **Pattern**: Sequential annual data with complete coverage
- **Use Case**: Primary time dimension for temporal analysis and filtering
- **Query Consideration**: Ideal for WHERE clauses, ORDER BY, and time-based grouping

### value_domestic (FLOAT64)
- **Data Type**: Float (decimal precision)
- **Null Values**: None (0%)
- **Range**: 40.47 to 162.29
- **Unique Values**: 69 (unique value per year)
- **Pattern**: Continuous numeric values, likely representing tonnage in millions
- **Sample Distribution**: Values span from ~40 to ~162, with samples showing variation across decades (50.90 in 2019, 143.07 in 1968)
- **Historical Trend**: Peak values appear in earlier years (1968: 143.07, 1973: 122.65) with lower values in recent years (2019: 50.90)
- **Use Case**: Primary metric for domestic shipping volume analysis
- **Query Consideration**: Suitable for aggregations (SUM, AVG, MIN, MAX), trend analysis, and year-over-year comparisons

### value_foreign (FLOAT64)
- **Data Type**: Float (decimal precision)
- **Null Values**: None (0%)
- **Range**: -8.92 to 41.62
- **Unique Values**: 69 (unique value per year)
- **Pattern**: Contains both negative and positive values
- **Notable**: Negative values present (e.g., -8.92, -6.52, -4.85, -1.43), suggesting this may represent:
  - Net foreign trade balance (exports minus imports)
  - Year-over-year change in foreign tonnage
  - Adjusted or normalized values
- **Sample Distribution**: Shows wider variance with both negative values (recent years like 2019: -1.43) and positive values (1970s-1980s showing higher positive values)
- **Use Case**: Foreign shipping activity metric, potentially net trade balance
- **Query Consideration**: Important to consider negative values in calculations; suitable for sum, average, and comparison analyses

## Potential Query Considerations

### Filtering Opportunities
- **Time-based filtering**: Filter by decade, specific year ranges, or before/after significant events (e.g., Edmund Fitzgerald sinking in 1975)
- **Value thresholds**: Filter years with domestic tonnage above/below certain levels
- **Foreign trade direction**: Separate positive vs. negative foreign values (net import vs. net export years)

### Grouping/Aggregation Opportunities
- **Decade analysis**: GROUP BY with year decade calculations (e.g., `FLOOR(year/10)*10`)
- **Period comparisons**: Pre/post specific years, multi-decade aggregations
- **Statistical summaries**: AVG, MIN, MAX, STDDEV for both domestic and foreign values
- **Running totals**: Cumulative tonnage over time windows

### Join Considerations
- **Year as join key**: Can join with other time-series datasets on the year column
- **Historical events**: Could join with tables containing Great Lakes historical events, economic indicators, or maritime incidents
- **No apparent foreign keys**: This appears to be a standalone fact table

### Data Quality Considerations
- **Negative foreign values**: Queries should account for the interpretation of negative values (likely net trade or changes, not absolute volumes)
- **Unit assumptions**: Values appear to be in consistent units throughout (likely millions of tons), but should be confirmed
- **Completeness**: Perfect data quality with no nulls makes this reliable for time-series analysis
- **Consistency**: Sequential years without gaps ensure reliable trend analysis

## Keywords

`Great Lakes`, `tonnage`, `shipping`, `maritime`, `cargo`, `domestic`, `foreign`, `trade`, `annual`, `time series`, `Edmund Fitzgerald`, `US shipping`, `freight`, `transportation`, `historical data`, `1952-2020`, `waterway commerce`, `bulk cargo`, `lake freighter`, `maritime history`

## Table and Column Documentation

### Table Comment
*No table comment provided in the analysis*

### Column Comments
*No column comments provided in the analysis*

---

**Note**: The table name reference to "Edmund Fitzgerald" provides important historical context. The Edmund Fitzgerald was a Great Lakes freighter that sank in Lake Superior during a storm on November 10, 1975, making it one of the most famous maritime disasters in Great Lakes history. This dataset likely serves to track the broader context of Great Lakes shipping volumes during and around this significant period.