---
columns:
- commodity_name (STRING)
- commodity_unit (STRING)
- date (DATE)
- price (NUMERIC)
schema_hash: 51846afc4d41dfb8408cb568b2cf3088b86c7567e285c5e562f29bbc77f05076

---
# Table Summary: compass-bigquery-demo.economic_data.stg_input_commodities

## Overall Dataset Characteristics

- **Total Rows**: 62,428 records
- **Data Quality**: Excellent - 0% null values across all columns
- **Time Series Nature**: This is a time-series dataset tracking commodity prices over time
- **Date Range**: Contains data spanning multiple years (2018-2025 based on samples), with 3,723 unique dates
- **Commodity Coverage**: Tracks 20 different commodities with varying price points and measurement units

**Notable Patterns**:
- Multiple unit systems tracked (USD and CNY)
- Different measurement scales (per kg, per ton, per troy ounce, per board feet)
- Mix of metals (precious and industrial), energy products, and construction materials
- Price ranges vary dramatically by commodity type (from single digits to tens of thousands)

## Column Details

### 1. **commodity_name** (STRING)
- **Purpose**: Identifies the specific commodity being tracked
- **Data Quality**: No nulls, 20 distinct commodities
- **Coverage**: Includes metals (aluminum, copper, gold, silver, lead, lithium, nickel, titanium, gallium, germanium), energy (bitumen), and materials (lumber, iron ore, polyethylene)
- **Complete List**: aluminum, bitumen, copper, gallium, germanium, gold, iron ore, lead, lithium, lumber, nickel, polyethylene, silver, titanium (and 6 more not shown in samples)
- **Usage**: Primary dimension for filtering and grouping

### 2. **date** (DATE)
- **Purpose**: Timestamp for price observation
- **Data Quality**: No nulls, 3,723 unique dates
- **Date Range**: Approximately 2018 to 2025 (based on samples: 2018-05-11 to 2025-02-20)
- **Temporal Coverage**: Appears to have regular daily or near-daily observations
- **Usage**: Primary time dimension for trend analysis, filtering by time periods, and time-series operations

### 3. **price** (NUMERIC)
- **Purpose**: The commodity price value at a given date
- **Data Quality**: No nulls, 26,601 unique values
- **Range**: Wide variation (samples show 7.18 to 76,500)
- **Scale Considerations**: Prices vary dramatically based on commodity and unit (e.g., lumber ~370, gold ~7,760, lithium ~76,500)
- **Usage**: Primary measure for aggregation, trending, and analysis

### 4. **commodity_unit** (STRING)
- **Purpose**: Defines the unit of measurement for the price
- **Data Quality**: No nulls, 10 distinct units
- **Currency Systems**: Both USD and CNY (Chinese Yuan)
- **Complete Unit List**:
  - USD/T (US Dollars per Ton)
  - USD/KG (US Dollars per Kilogram)
  - USD/Lbs (US Dollars per Pound)
  - USD/t.oz (US Dollars per troy ounce)
  - USD/1000 board feet (lumber-specific)
  - USD Cents / Kg
  - CNY/T (Chinese Yuan per Ton)
  - CNY/Kg and CNY/KG (case variants)
  - CNY/mtu (metric ton unit)
- **Usage**: Critical for proper interpretation of price values; needed for unit conversion calculations

## Potential Query Considerations

### Best Columns for Filtering:
- **commodity_name**: Filter by specific commodities or groups of commodities
- **date**: Filter by date ranges, specific years, months, or recent periods
- **commodity_unit**: Filter by currency (USD vs CNY) or measurement system

### Best Columns for Grouping/Aggregation:
- **commodity_name**: Group to compare across commodities
- **date** (with DATE_TRUNC): Group by year, quarter, month, or week for trend analysis
- **commodity_unit**: Group by unit type or currency for normalized comparisons

### Join Keys and Relationships:
- **commodity_name + date**: Composite key for potentially joining with other commodity or economic datasets
- **date**: Can join with calendar tables, economic indicators, or other time-series data
- No obvious foreign keys present; this appears to be a fact table

### Data Quality Considerations:

1. **Unit Standardization**: 
   - Case sensitivity issue: "CNY/Kg" vs "CNY/KG"
   - Queries comparing prices must account for different units
   - Price normalization required for meaningful cross-commodity comparisons

2. **Price Scale Variations**:
   - Direct price comparisons are meaningless without unit context
   - Percentage changes or indexed values more appropriate for cross-commodity analysis

3. **Date Continuity**:
   - Check for gaps in daily data (weekends, holidays)
   - Consider whether missing dates represent no trading or no data

4. **Currency Considerations**:
   - Mixed USD and CNY pricing requires currency conversion for unified analysis
   - Exchange rate data would be needed for currency-normalized comparisons

5. **Time-Series Analysis**:
   - Well-suited for trend analysis, moving averages, and volatility calculations
   - Date range allows for year-over-year and seasonal analysis

## Keywords

commodities, commodity prices, economic data, time series, metals, precious metals, industrial metals, raw materials, price tracking, aluminum, copper, gold, silver, lithium, nickel, titanium, lumber, bitumen, iron ore, polyethylene, gallium, germanium, lead, USD prices, CNY prices, market data, trading data, daily prices, economic indicators, staging table, stg_input_commodities

## Table and Column Documentation

**Table Comment**: Not provided

**Column Comments**: Not provided