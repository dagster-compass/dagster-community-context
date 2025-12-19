---
columns:
- commodity_name (STRING)
- commodity_unit (STRING)
- date (DATE)
- price (NUMERIC)
schema_hash: 51846afc4d41dfb8408cb568b2cf3088b86c7567e285c5e562f29bbc77f05076

---
# Data Summary: stg_energy_commodities Table

## Overall Dataset Characteristics

**Total Records:** 21,819 rows

**Data Quality:** Excellent - all columns have 0% null values, indicating complete data coverage across all fields.

**Dataset Scope:** This table contains historical pricing data for six energy commodities tracked over time. With 3,847 unique dates, the data appears to span multiple years with regular time series observations.

**Distribution Patterns:**
- Multiple commodities tracked simultaneously (6 distinct types)
- Price data shows high variability (9,464 unique values across 21,819 rows)
- Time series data with approximately 5-6 observations per date on average (21,819 rows / 3,847 dates)
- Sample dates range from 2014 to 2019, suggesting at least 5+ years of historical data

## Column Details

### commodity_name (STRING)
- **Purpose:** Primary commodity identifier
- **Data Type:** Categorical string
- **Completeness:** 100% populated
- **Values:** 6 distinct energy commodities:
  - brent (Brent crude oil)
  - coal
  - crude oil
  - gasoline
  - heating oil
  - natural gas
- **Patterns:** Standardized lowercase naming convention; appears to distinguish between different types of petroleum products (brent vs crude oil)

### price (NUMERIC)
- **Purpose:** Commodity price value
- **Data Type:** Numeric (decimal precision)
- **Completeness:** 100% populated
- **Cardinality:** 9,464 unique values
- **Patterns:** High variability appropriate for market pricing data; likely includes decimal precision for accurate financial reporting
- **Considerations:** Prices must be interpreted in conjunction with commodity_unit for context

### date (DATE)
- **Purpose:** Observation/pricing date
- **Data Type:** Date
- **Completeness:** 100% populated
- **Range:** 3,847 unique dates spanning 2014-2019 (based on samples)
- **Patterns:** Time series data with regular observations; multiple commodities typically recorded per date
- **Format:** Standard DATE format (YYYY-MM-DD)

### commodity_unit (STRING)
- **Purpose:** Unit of measurement for price
- **Data Type:** Categorical string
- **Completeness:** 100% populated
- **Values:** 4 distinct units:
  - USD/Bbl (Barrel - for crude oil, brent)
  - USD/Gal (Gallon - for gasoline, heating oil)
  - USD/MMBtu (Million British Thermal Units - for natural gas)
  - USD/T (Ton - for coal)
- **Patterns:** All units are USD-denominated; units correspond logically to commodity types (energy industry standards)

## Potential Query Considerations

### Optimal Filtering Columns:
- **commodity_name:** Primary filter for analyzing specific energy commodities
- **date:** Essential for time-based filtering (date ranges, specific periods)
- **commodity_unit:** Useful for grouping commodities by measurement type

### Aggregation Opportunities:
- **price:** Primary metric for calculations (AVG, MIN, MAX, SUM for weighted analyses)
- **date:** Time-based grouping (by day, month, quarter, year using DATE_TRUNC functions)
- **commodity_name:** Group by commodity type for comparative analysis
- **commodity_unit:** Secondary grouping dimension

### Time Series Analysis:
- Excellent candidate for trend analysis, moving averages, and period-over-period comparisons
- Date column enables year-over-year, month-over-month price change calculations
- Can calculate price volatility metrics per commodity

### Join Considerations:
- **Potential Join Keys:** date (for joining with other economic/market data), commodity_name (for reference tables)
- Could join with currency exchange rates, economic indicators, or supply/demand data on date
- May relate to broader economic datasets in the `economic_data` schema

### Data Quality Considerations:
- No null handling required - data is complete
- Price values should be validated as positive numbers in queries
- Date ranges should be considered when performing aggregations (check MIN/MAX dates)
- Commodity-unit relationships are fixed (each commodity has one consistent unit)
- Weekend/holiday date gaps may exist in time series

### Query Performance Tips:
- Index on date column recommended for time-based queries
- Partition by date for large-scale time series queries
- commodity_name has low cardinality (6 values) - excellent for filtering and grouping

## Keywords

energy commodities, oil prices, natural gas prices, coal prices, gasoline prices, heating oil prices, brent crude, commodity prices, time series data, economic data, energy market data, historical prices, USD pricing, barrel pricing, BTU pricing, gallon pricing, ton pricing, petroleum products, fossil fuels, energy economics

## Table and Column Documentation

**Table Comment:** Not provided

**Column Comments:** Not provided