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
# Great Lakes Shipping Data Analysis Summary

## Overall Dataset Characteristics

### Basic Statistics
- **Total Rows**: 11 rows (appears to be annual data from 2011-2021)
- **Table**: `compass-bigquery-demo.edmund_fitzgerald.great_lakes_shipping_combined_2011_2020`
- **Time Period**: 2011-2021 (11 years of data)
- **Data Type**: Time-series shipping/commodity data for Great Lakes region

### Data Quality Observations
- **Missing Data**: Some columns have 9.09% null values (1 row missing out of 11), specifically:
  - `slag`
  - `salt`
  - `coal_lignite`
  - `value_limestone`
  - `value_iron_ore`
- **Data Completeness**: Most commodity columns are fully populated (0% nulls)
- **Consistency**: All numeric values are FLOAT64 except `year` (INT64)

### Notable Patterns
- Data represents annual aggregations of Great Lakes shipping activity
- Values appear to be rates, percentages, or normalized metrics (many values between 0-25, some up to 55)
- Some commodities show negative values (e.g., wheat ranges from -0.35 to 2.13), suggesting this may be year-over-year change or normalized/standardized data
- Year 2015 appears to be the row with missing values across multiple columns

## Column-by-Column Analysis

### Year Dimension

#### year (INT64)
- **Type**: Integer, Time dimension
- **Range**: 2011 to 2021
- **Nulls**: 0%
- **Characteristics**: Sequential annual data, primary time key
- **Use Case**: Primary dimension for time-based queries and trend analysis

### Commodity Shipping Metrics

#### slag (FLOAT64)
- **Type**: Numeric metric
- **Range**: 0.256 to 0.919
- **Nulls**: 9.09% (1 missing value)
- **Distribution**: Values clustered between 0.3 and 0.8
- **Characteristics**: Industrial byproduct shipping metric, relatively low values

#### cement_concrete (FLOAT64)
- **Type**: Numeric metric
- **Range**: 4.13 to 5.34
- **Nulls**: 0%
- **Distribution**: Tightly clustered between 4.1 and 5.4
- **Characteristics**: Construction materials, most consistent dataset with no missing values

#### wheat (FLOAT64)
- **Type**: Numeric metric
- **Range**: -0.354 to 2.13
- **Nulls**: 0%
- **Distribution**: Includes negative values, suggesting normalized or change metrics
- **Characteristics**: Agricultural commodity, highly variable with both positive and negative values

#### sand_gravel (FLOAT64)
- **Type**: Numeric metric
- **Range**: 1.11 to 3.73
- **Nulls**: 0%
- **Distribution**: Values mostly between 1.1 and 2.6, with one outlier at 3.55
- **Characteristics**: Construction aggregate material

#### salt (FLOAT64)
- **Type**: Numeric metric
- **Range**: 3.71 to 6.33
- **Nulls**: 9.09%
- **Distribution**: Mid-range values between 3.7 and 6.3
- **Characteristics**: Industrial/de-icing commodity

#### coal_lignite (FLOAT64)
- **Type**: Numeric metric
- **Range**: 7.35 to 23.08
- **Nulls**: 9.09%
- **Distribution**: Wide range, highest values among commodities (up to 23)
- **Characteristics**: Energy commodity, showing significant variability

#### asphalt_tar_pitch (FLOAT64)
- **Type**: Numeric metric
- **Range**: 0.78 to 5.19
- **Nulls**: 0%
- **Distribution**: Values spread between 0.78 and 5.19
- **Characteristics**: Petroleum-based construction material

#### petroleum_coke (FLOAT64)
- **Type**: Numeric metric
- **Range**: -0.090 to 3.93
- **Nulls**: 0%
- **Distribution**: Includes small negative values, mostly positive
- **Characteristics**: Petroleum byproduct, relatively low shipping volumes

### Value Metrics

#### value_limestone (FLOAT64)
- **Type**: Numeric metric (likely value/price indicator)
- **Range**: 18.00 to 22.44
- **Nulls**: 9.09%
- **Distribution**: Tightly clustered between 18 and 22.4
- **Characteristics**: Construction/industrial mineral value metric

#### value_iron_ore (FLOAT64)
- **Type**: Numeric metric (likely value/price indicator)
- **Range**: 44.99 to 55.75
- **Nulls**: 9.09%
- **Distribution**: Highest value range, between 45 and 56
- **Characteristics**: Strategic mineral value metric, notably higher than other commodities

## Potential Query Considerations

### Filtering Strategies
- **Time-based filtering**: Use `year` for specific years or ranges (2011-2021)
- **Commodity filtering**: Filter on specific commodity columns to analyze individual materials
- **Value thresholds**: `value_iron_ore` and `value_limestone` can be filtered by value ranges
- **Null handling**: Be aware of 9.09% nulls in slag, salt, coal_lignite, value_limestone, and value_iron_ore

### Grouping/Aggregation Opportunities
- **Temporal analysis**: Group by `year` for trend analysis
- **Commodity comparison**: Aggregate across commodity columns to compare shipping volumes
- **Value analysis**: Calculate averages, trends for value_* columns
- **Complete data analysis**: Filter WHERE slag IS NOT NULL for complete records only

### Join Considerations
- **Primary Key**: `year` serves as the natural primary key
- **External joins**: Could join with economic indicators, weather data, or industry statistics by year
- **No obvious foreign keys**: This appears to be a standalone summary table

### Data Quality Considerations
- **Handle nulls**: Queries should use COALESCE or null-safe operators for columns with missing data
- **Negative values**: Be prepared for negative values in wheat and petroleum_coke (may indicate year-over-year changes)
- **Small dataset**: With only 11 rows, aggregations will have limited statistical power
- **Potential data gaps**: 2015 appears to have multiple missing values - queries may need special handling for this year
- **Scale differences**: Values range from sub-1 to 55+, consider normalization for comparative analysis

### Recommended Query Patterns
1. **Trend analysis**: Year-over-year changes in commodity shipping
2. **Correlation analysis**: Relationships between different commodities
3. **Value comparisons**: Iron ore vs limestone value trends
4. **Complete case analysis**: Filtering to years with no null values
5. **Moving averages**: Calculate trends accounting for the small dataset size

## Keywords
Great Lakes shipping, maritime trade, bulk commodities, iron ore, limestone, coal, cement, wheat, agricultural shipping, industrial materials, construction materials, petroleum products, slag, salt, sand and gravel, shipping volumes, commodity values, annual data, time series, Edmund Fitzgerald, Great Lakes commerce, freight analysis, 2011-2021 data

## Table and Column Documentation

**Note**: No table-level comment or column-level comments were provided in the source data. This table appears to track annual shipping metrics and commodity values for Great Lakes maritime trade from 2011-2021, likely named after the famous Great Lakes freighter SS Edmund Fitzgerald.