---
columns:
- commodity_name (STRING)
- commodity_unit (STRING)
- date (DATE)
- price (NUMERIC)
schema_hash: 51846afc4d41dfb8408cb568b2cf3088b86c7567e285c5e562f29bbc77f05076

---
# Table Summary: stg_agriculture_commodities

## Overall Dataset Characteristics

**Total Rows:** 31,989

**General Description:**
This table contains historical pricing data for agricultural commodities traded on markets. The dataset tracks 9 different commodity types across approximately 3,714 unique trading dates, resulting in a comprehensive time-series dataset of agricultural commodity prices.

**Data Quality Observations:**
- **Excellent completeness**: 0% null values across all columns
- High data integrity with no missing values in any column
- Contains 13,637 unique price points across the dataset
- Multiple commodities tracked with varying price units

**Notable Patterns:**
- Multi-commodity tracking system covering livestock (cattle, poultry), grains (corn, wheat, soybeans), and other agricultural products (cotton, eggs, sugar)
- Time-series nature with dates spanning multiple years (at least 2023-2024 based on sample values)
- Different pricing units used depending on commodity type (bushels for grains, pounds for livestock, dozen for eggs, etc.)

---

## Column Details

### 1. commodity_name (STRING)
- **Data Type:** String/Categorical
- **Null Values:** None (0%)
- **Cardinality:** 9 unique commodities
- **Values:**
  - **Livestock:** live cattle, feeder cattle, poultry
  - **Grains:** corn, wheat, soybeans
  - **Other:** cotton, eggs us, sugar
- **Pattern:** Lowercase naming convention, some with multi-word names (e.g., "eggs us", "live cattle")

### 2. commodity_unit (STRING)
- **Data Type:** String/Categorical
- **Null Values:** None (0%)
- **Cardinality:** 5 unique units
- **Values:**
  - `BRL/Kgs` - Brazilian Real per Kilogram
  - `USD/Dozen` - US Dollars per Dozen (likely for eggs)
  - `USd/BU` - US cents per Bushel
  - `USd/Bu` - US cents per Bushel (variant spelling)
  - `USd/Lbs` - US cents per Pound
- **Pattern:** Mixed capitalization; note the inconsistency between "BU" and "Bu" for bushels

### 3. price (NUMERIC)
- **Data Type:** Numeric
- **Null Values:** None (0%)
- **Cardinality:** 13,637 unique values (42.6% of total rows)
- **Characteristics:**
  - High variability across commodities due to different units
  - Continuous pricing data
  - Likely includes decimal precision for accurate market pricing

### 4. date (DATE)
- **Data Type:** Date
- **Null Values:** None (0%)
- **Cardinality:** 3,714 unique dates
- **Sample Range:** 2023-03-01 to 2024-10-18 (based on samples)
- **Pattern:** 
  - Approximately 8.6 records per date on average (31,989 / 3,714)
  - Suggests regular daily or near-daily tracking of multiple commodities

---

## Query Considerations

### Filtering Columns
- **commodity_name**: Primary filter for commodity-specific analysis
- **date**: Essential for time-based queries, trend analysis, and date range filtering
- **commodity_unit**: Useful for grouping commodities by pricing methodology

### Grouping/Aggregation Columns
- **commodity_name**: Primary grouping dimension for comparative analysis
- **date**: For temporal aggregations (daily, monthly, yearly trends)
- **commodity_unit**: For understanding pricing structures across different measurement systems
- **Aggregation opportunities**: AVG(price), MIN(price), MAX(price), price volatility calculations

### Potential Join Keys
- **date**: Can join with other economic datasets (e.g., currency rates, market indices, weather data)
- **commodity_name**: Could join with commodity metadata, production data, or inventory tables
- **Composite key (date, commodity_name)**: Unique identifier for specific commodity prices on specific dates

### Data Quality Considerations

1. **Unit Consistency Issue:**
   - Note the inconsistency: `USd/BU` vs `USd/Bu` (both represent bushels)
   - Queries filtering or grouping by unit should account for both variants
   - May need normalization for accurate aggregations

2. **Price Comparability:**
   - Direct price comparisons across commodities are NOT meaningful due to different units
   - Convert to normalized units or use percentage changes for cross-commodity analysis

3. **Time Series Completeness:**
   - With 3,714 dates and 9 commodities, average coverage is ~8.6 records per date
   - Some commodities may not trade on all dates (weekends, holidays, market closures)
   - Queries should handle potential gaps in time series

4. **Currency Considerations:**
   - Mix of USD and BRL currencies (Brazilian Real for at least one commodity)
   - Cross-currency comparisons require exchange rate adjustments

5. **Query Performance:**
   - Date-based partitioning would benefit time-range queries
   - Indexing on commodity_name and date recommended for common query patterns

---

## Keywords

agriculture, commodities, pricing, livestock, cattle, poultry, grains, corn, wheat, soybeans, cotton, eggs, sugar, feeder cattle, live cattle, time series, market data, trading, agricultural economics, commodity prices, USD, BRL, bushels, pounds, dozen, kilogram, economic data, price trends, historical prices, commodity trading, agricultural markets

---

## Table and Column Documentation

**Note:** No table comment or column comments were provided in the source analysis report. This table appears to be a staging table (prefix "stg_") in a data warehouse, likely part of an ETL pipeline for agricultural commodity market data.