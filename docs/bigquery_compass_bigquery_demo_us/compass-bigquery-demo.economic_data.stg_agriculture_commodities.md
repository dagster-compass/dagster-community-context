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

**Total Rows:** 32,285

**General Description:** This staging table contains historical and forecasted pricing data for agricultural commodities, spanning multiple years with daily or near-daily granularity. The dataset appears to be clean and well-structured, with no null values detected across any columns.

**Data Quality Observations:**
- Excellent data completeness: 0% null values across all columns
- Consistent formatting and standardized values
- Appropriate data types for each field
- Mix of historical and future-dated records (includes dates into 2025)

**Notable Patterns:**
- 3,749 unique dates suggest approximately 9-10 years of daily data coverage
- 9 distinct commodities tracked with standardized naming conventions
- Multiple unit types indicate different commodities measured in different ways
- 13,773 unique price points across 32,285 rows suggest some price repetition, likely due to same prices across different commodities or dates

## Column Details

### commodity_name (STRING)
- **Purpose:** Identifies the agricultural commodity being priced
- **Values:** 9 distinct commodities
  - corn
  - cotton
  - eggs us
  - feeder cattle
  - live cattle
  - poultry
  - soybeans
  - sugar
  - wheat
- **Patterns:** All lowercase, standardized naming with "eggs us" being the only multi-word entry
- **Query Considerations:** Excellent dimension for filtering and grouping; use exact matches (case-sensitive)

### commodity_unit (STRING)
- **Purpose:** Specifies the pricing unit for each commodity
- **Values:** 5 distinct units
  - BRL/Kgs (Brazilian Real per Kilogram)
  - USD/Dozen (US Dollars per Dozen)
  - USd/BU (US cents per Bushel)
  - USd/Bu (US cents per Bushel - alternate formatting)
  - USd/Lbs (US cents per Pound)
- **Patterns:** Mix of currency and measurement units; note inconsistent capitalization (BU vs Bu)
- **Query Considerations:** Important for price interpretation; USd/BU and USd/Bu appear to be the same unit with formatting variation

### price (NUMERIC)
- **Purpose:** The commodity price in the specified unit
- **Range:** Wide range from single digits to four digits (sample: 1024.5, 12.87, 105.525)
- **Format:** Decimal values with varying precision
- **Patterns:** 13,773 unique values across 32,285 rows (~42.7% uniqueness)
- **Query Considerations:** Suitable for aggregations (AVG, MIN, MAX, SUM); consider rounding for grouping operations

### date (DATE)
- **Purpose:** The date of the price observation or forecast
- **Range:** 3,749 unique dates spanning from historical data through 2025
- **Sample Range:** 2014-04-01 through 2025-05-21 (based on samples)
- **Patterns:** Daily granularity with some gaps possible
- **Query Considerations:** Excellent for time-series analysis, trending, and date range filtering; can extract year, month, quarter for aggregations

## Query Considerations

### Ideal for Filtering:
- **commodity_name:** Primary dimension for specific commodity analysis
- **date:** Time-based filtering (date ranges, specific periods)
- **commodity_unit:** When analyzing specific measurement systems or currencies

### Ideal for Grouping/Aggregation:
- **commodity_name:** Commodity-level summaries
- **date components:** Year, month, quarter trends (EXTRACT functions)
- **commodity_unit:** Unit-based analysis
- **Combinations:** commodity_name + time period for time-series by commodity

### Potential Join Keys:
- **commodity_name:** Could join to commodity reference/master tables
- **date:** Could join to calendar/date dimensions, economic indicators, weather data
- **commodity_name + date:** Composite key for joining to other commodity-related datasets

### Data Quality Considerations:
1. **Unit Standardization:** Be aware of USd/BU vs USd/Bu inconsistency when filtering
2. **Price Comparability:** Different units mean prices aren't directly comparable across commodities without conversion
3. **Currency Considerations:** BRL/Kgs uses Brazilian Real, requiring currency conversion for USD comparisons
4. **Future Dates:** Dataset includes forecasted prices (2025 dates); queries may need to distinguish between historical and projected data
5. **Missing Dates:** With 3,749 dates across ~11 years, there may be gaps (weekends, holidays); consider date range queries carefully

## Keywords

agriculture, commodities, pricing, agricultural markets, corn, wheat, soybeans, cotton, cattle, poultry, eggs, sugar, commodity prices, time series, economic data, staging table, daily prices, agricultural economics, livestock, grains, USd, BRL, bushel, pound, dozen, kilogram, price history, commodity trading, agribusiness, feeder cattle, live cattle

## Table and Column Documentation

**Table Comment:** Not provided

**Column Comments:** Not provided