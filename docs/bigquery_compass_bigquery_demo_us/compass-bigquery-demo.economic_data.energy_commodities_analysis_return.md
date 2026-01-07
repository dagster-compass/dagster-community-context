---
columns:
- commodity_name (STRING)
- commodity_unit (STRING)
- current_price (NUMERIC)
- date (DATE)
- high_1mo (NUMERIC)
- high_1yr (NUMERIC)
- high_3mo (NUMERIC)
- high_6mo (NUMERIC)
- high_9mo (NUMERIC)
- low_1mo (NUMERIC)
- low_1yr (NUMERIC)
- low_3mo (NUMERIC)
- low_6mo (NUMERIC)
- low_9mo (NUMERIC)
- pct_change_1mo (FLOAT64)
- pct_change_1yr (FLOAT64)
- pct_change_3mo (FLOAT64)
- pct_change_6mo (FLOAT64)
- pct_change_9mo (FLOAT64)
- std_diff_1mo (FLOAT64)
- std_diff_1yr (FLOAT64)
- std_diff_3mo (FLOAT64)
- std_diff_6mo (FLOAT64)
- std_diff_9mo (FLOAT64)
schema_hash: fa5f61622dc3fbbc589bdddb5a4882bc3b7515101f1ed67fa7fd1fb2118449f9

---
# Comprehensive Summary: Energy Commodities Analysis Return Table

## Overall Dataset Characteristics

**Total Rows:** 21,903

**General Description:** This table contains time-series analysis data for energy commodity prices with rolling return metrics across multiple time periods (1 month, 3 months, 6 months, 9 months, and 1 year). The data tracks six different energy commodities with their current prices, historical high/low values, percentage changes, and standard deviation differences.

**Data Quality Observations:**
- Very high data quality overall with minimal null values in most columns
- Percentage change columns have significant null percentages (21-42%), likely representing initial periods where historical data isn't available for comparison
- Only 0.05% null values in standard deviation columns
- All core columns (commodity_name, current_price, date, commodity_unit) have 0% null values
- Date range spans from at least 2016 to 2025 (approximately 9 years)

**Notable Patterns:**
- Data appears to be daily or near-daily observations (3,862 unique dates for 21,903 rows suggests multiple commodities tracked per date)
- High variability in price ranges across different commodities (e.g., coal ranging from $169-457.8 vs natural gas from $0.866-4.463)
- Extreme percentage changes observed (ranging from -167% to +512%), indicating high volatility in energy markets

## Column Details

### Categorical/Identifier Columns

**commodity_name (STRING)**
- Data Type: Categorical identifier
- Null Values: 0%
- Unique Values: 6 commodities
- Values: brent, coal, crude oil, gasoline, heating oil, natural gas
- Purpose: Primary grouping dimension for commodity type

**commodity_unit (STRING)**
- Data Type: Categorical measurement unit
- Null Values: 0%
- Unique Values: 4 units
- Values: USD/Bbl (barrels), USD/Gal (gallons), USD/MMBtu (million British thermal units), USD/T (tons)
- Purpose: Indicates pricing measurement standard for each commodity
- Pattern: Direct relationship with commodity_name (e.g., coal always in USD/T, natural gas in USD/MMBtu)

**date (DATE)**
- Data Type: Temporal dimension
- Null Values: 0%
- Unique Values: 3,862 dates
- Range: 2016-01-04 to 2025-04-24
- Purpose: Time-series tracking key
- Pattern: Approximately 5.7 records per date on average (21,903/3,862), consistent with 6 commodities

### Price Columns

**current_price (NUMERIC)**
- Data Type: Decimal number
- Null Values: 0%
- Unique Values: 9,485 distinct prices
- Sample Range: $2.334 to $457.8 (varies by commodity)
- Purpose: Current/spot price for the commodity on the given date
- Pattern: High precision decimal values reflecting market prices

### Rolling High/Low Price Columns

**high_1yr / low_1yr (NUMERIC)**
- Null Values: 0%
- Unique Values: 1,441 (high), 1,384 (low)
- Purpose: 1-year rolling maximum and minimum prices

**high_9mo / low_9mo (NUMERIC)**
- Null Values: 0%
- Unique Values: 1,584 (high), 1,491 (low)
- Purpose: 9-month rolling maximum and minimum prices

**high_6mo / low_6mo (NUMERIC)**
- Null Values: 0%
- Unique Values: 1,918 (high), 1,864 (low)
- Purpose: 6-month rolling maximum and minimum prices

**high_3mo / low_3mo (NUMERIC)**
- Null Values: 0%
- Unique Values: 2,783 (high), 2,621 (low)
- Purpose: 3-month rolling maximum and minimum prices

**high_1mo / low_1mo (NUMERIC)**
- Null Values: 0%
- Unique Values: 3,732 (high), 3,661 (low)
- Purpose: 1-month rolling maximum and minimum prices

Pattern: More unique values for shorter time periods (indicating more granular price variations)

### Statistical Measures - Standard Deviation Differences

**std_diff_1yr (FLOAT64)**
- Null Values: 0.05%
- Unique Values: 9,139
- Range: 0.0226 to 13.597
- Purpose: Standard deviation of price differences over 1 year

**std_diff_9mo (FLOAT64)**
- Null Values: 0.05%
- Unique Values: 9,327
- Range: 0.0221 to 14.0946
- Purpose: Standard deviation of price differences over 9 months

**std_diff_6mo (FLOAT64)**
- Null Values: 0.05%
- Unique Values: 9,381
- Range: 0.0211 to 15.8354
- Purpose: Standard deviation of price differences over 6 months

**std_diff_3mo (FLOAT64)**
- Null Values: 0.05%
- Unique Values: 9,780
- Range: 0.0182 to 20.3103
- Purpose: Standard deviation of price differences over 3 months

**std_diff_1mo (FLOAT64)**
- Null Values: 0.05%
- Unique Values: 10,256
- Range: 0.0118 to 33.4104
- Purpose: Standard deviation of price differences over 1 month

Pattern: Higher maximum std_diff values for shorter periods, suggesting short-term volatility can be more extreme

### Percentage Change Columns

**pct_change_1yr (FLOAT64)**
- Null Values: 26.08% (5,711 rows)
- Unique Values: 9,193
- Range: -158.33% to +512.89%
- Purpose: Year-over-year percentage change in price

**pct_change_9mo (FLOAT64)**
- Null Values: 42.10% (9,221 rows)
- Unique Values: 7,599
- Range: -167.17% to +309.0%
- Purpose: 9-month percentage change in price

**pct_change_6mo (FLOAT64)**
- Null Values: 40.61% (8,895 rows)
- Unique Values: 7,013
- Range: -167.23% to +196.3%
- Purpose: 6-month percentage change in price

**pct_change_3mo (FLOAT64)**
- Null Values: 21.86% (4,787 rows)
- Unique Values: 6,670
- Range: -164.47% to +307.69%
- Purpose: 3-month percentage change in price

**pct_change_1mo (FLOAT64)**
- Null Values: 38.93% (8,527 rows)
- Unique Values: 4,202
- Range: -153.73% to +238.86%
- Purpose: 1-month percentage change in price

Pattern: High null percentages indicate insufficient historical data for early observations in the time series

## Query Considerations

### Excellent Columns for Filtering:
- **commodity_name**: Only 6 values, perfect for WHERE clauses to analyze specific commodities
- **date**: Ideal for time-based filtering (date ranges, specific years, quarters)
- **commodity_unit**: Can filter by pricing unit if analyzing specific measurement types
- **pct_change_*** columns: Can filter for significant price movements (e.g., WHERE pct_change_1yr > 50)

### Excellent Columns for Grouping/Aggregation:
- **commodity_name**: Primary grouping dimension for commodity comparisons
- **date** (with DATE_TRUNC): Can group by year, quarter, month for trend analysis
- **commodity_unit**: Secondary grouping if analyzing by pricing methodology
- Time-based aggregations of price metrics (AVG, MIN, MAX of current_price by commodity)

### Potential Join Keys:
- **commodity_name + date**: Composite key for joining with other commodity-related tables
- **date**: Can join with general economic indicators, market indices, or event data
- No obvious foreign keys present, but commodity_name could link to a commodity master table

### Data Quality Considerations for Queries:

1. **Null Handling Required:**
   - Always check for nulls in pct_change_* columns (21-42% null)
   - Use COALESCE or WHERE IS NOT NULL when aggregating percentage changes
   - Consider whether nulls represent missing data or insufficient history

2. **Time Series Gaps:**
   - Verify date continuity if performing time-based calculations
   - Use window functions carefully with potential date gaps
   - Consider the ~26% null rate in pct_change_1yr means early records lack full year history

3. **Price Comparability:**
   - Always filter or group by commodity_unit when comparing prices
   - Coal ($169-$457) vs Natural Gas ($0.866-$4.463) have vastly different scales
   - Consider normalizing prices or using percentage changes for cross-commodity comparisons

4. **Volatility Analysis:**
   - std_diff columns provide volatility metrics but vary by time period
   - Extreme values in pct_change suggest outliers or market shocks worth investigating
   - Consider filtering out extreme percentages for typical analysis

5. **Current vs Historical:**
   - current_price is point-in-time; high/low columns are rolling windows
   - Ensure queries account for the rolling nature of high/low metrics
   - Be careful with edge cases where current_price might equal high or low values

## Keywords

energy commodities, oil prices, natural gas, coal, gasoline, heating oil, Brent crude, price analysis, volatility, percentage change, rolling returns, time series, commodity trading, energy markets, price movements, standard deviation, historical prices, price highs, price lows, market analysis, commodity units, USD per barrel, USD per gallon, USD per MMBtu, USD per ton, 1-year returns, 9-month returns, 6-month returns, 3-month returns, 1-month returns, price volatility, energy sector, commodity pricing, financial analysis, market metrics, trading analysis

## Table and Column Documentation

**Table Comment:** Not provided in the analysis report.

**Column Comments:** No column-level comments were provided in the analysis report. The column names are self-descriptive, following a consistent naming pattern:
- Base metric + time period (e.g., high_1yr, low_3mo)
- Calculated metrics prefixed with metric type (pct_change_*, std_diff_*)
- Core columns use standard naming (commodity_name, date, current_price, commodity_unit)