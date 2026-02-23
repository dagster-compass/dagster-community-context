---
columns:
- commodity_name (STRING)
- commodity_unit (STRING)
- date (DATE)
- price (NUMERIC)
schema_hash: 51846afc4d41dfb8408cb568b2cf3088b86c7567e285c5e562f29bbc77f05076

---
# Table Summary: stg_input_commodities

## Overall Dataset Characteristics

- **Total Rows**: 63,033 records
- **Data Completeness**: Excellent - 0% null values across all columns
- **Time Series Nature**: This is a time-series dataset tracking commodity prices over time
- **Date Range**: Spans from 2014 to 2024 (approximately 10 years of data)
- **Data Quality**: High quality with complete records and consistent formatting
- **Coverage**: 3,758 unique dates with 20 different commodities tracked
- **Granularity**: Daily price observations for various commodities

## Column Details

### 1. **commodity_name** (STRING)
- **Purpose**: Identifies the specific commodity being tracked
- **Values**: 20 unique commodities including:
  - Metals: aluminum, copper, iron ore, lead, zinc, gold, silver, titanium, gallium, germanium
  - Energy/Materials: bitumen, rubber
  - Plastics: polyethylene, polypropylene
  - Building Materials: lumber
  - Battery Materials: lithium
- **Data Quality**: No nulls, consistent naming (lowercase)
- **Query Use**: Primary dimension for filtering and grouping

### 2. **commodity_unit** (STRING)
- **Purpose**: Specifies the unit of measurement for the price
- **Values**: 10 unique units with variations:
  - Weight-based: USD/T, USD/t.oz, USD/KG, USD/Lbs, CNY/T, CNY/Kg, CNY/KG
  - Specialized: USD/1000 board feet (lumber), USD Cents / Kg, CNY/mtu (mineral trading unit)
- **Data Quality**: Some inconsistency in capitalization (CNY/Kg vs CNY/KG)
- **Query Consideration**: Important for price comparisons; unit conversions may be needed

### 3. **date** (DATE)
- **Purpose**: The observation date for the commodity price
- **Range**: 3,758 unique dates spanning ~10 years (2014-2024)
- **Data Quality**: Complete coverage, no nulls
- **Query Use**: 
  - Ideal for time-series analysis and trending
  - Good for filtering by date ranges
  - Suitable for temporal aggregations (daily, monthly, yearly)

### 4. **price** (NUMERIC)
- **Purpose**: The commodity price on the given date in the specified unit
- **Distribution**: 26,893 unique values indicating high price variability
- **Range Examples**: From 6.25 (likely per kg/lb items) to 6950+ (likely per ton items)
- **Data Quality**: Complete dataset, no nulls
- **Query Use**: Primary metric for aggregations (AVG, MIN, MAX, trends)

## Potential Query Considerations

### Good for Filtering:
- **commodity_name**: Filter by specific commodities or groups (e.g., metals, plastics)
- **date**: Date range filtering for specific time periods
- **commodity_unit**: Filter by currency or measurement system (USD vs CNY)

### Good for Grouping/Aggregation:
- **commodity_name**: Group by commodity type for comparative analysis
- **date dimensions**: Extract YEAR, MONTH, QUARTER for temporal aggregations
- **commodity_unit**: Group by unit type for standardization analysis

### Analytical Patterns:
- **Time Series Analysis**: Track price trends over time for each commodity
- **Comparative Analysis**: Compare prices across different commodities
- **Volatility Analysis**: Calculate price variance and standard deviations
- **Period-over-Period**: Calculate YoY, MoM growth rates

### Data Quality Considerations:
- **Unit Standardization**: Queries comparing prices across commodities must account for different units
- **Currency Conversion**: USD vs CNY prices may need conversion for direct comparison
- **Case Sensitivity**: commodity_unit has inconsistent capitalization (KG vs Kg)
- **Missing Dates**: Not all commodities may have data for all dates (check for gaps in time series)

### Potential Join Keys:
- **date**: Can join with other economic indicators or calendar tables
- **commodity_name**: Can join with commodity reference tables for additional attributes (category, industry sector, etc.)
- Composite key **(commodity_name, date)** likely forms a unique identifier for each record

## Keywords

commodities, commodity prices, time series, economic data, metals, aluminum, copper, gold, silver, iron ore, zinc, lead, titanium, gallium, germanium, lithium, plastics, polyethylene, polypropylene, rubber, bitumen, lumber, USD, CNY, price tracking, market data, trading prices, raw materials, daily prices, historical prices, commodity markets, materials pricing

## Table and Column Documentation

**Table Comment**: Not provided

**Column Comments**: Not provided