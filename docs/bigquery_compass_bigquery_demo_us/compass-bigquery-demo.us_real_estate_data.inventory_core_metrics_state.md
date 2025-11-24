---
columns:
- active_listing_count (INT64)
- active_listing_count_mm (FLOAT64)
- active_listing_count_yy (FLOAT64)
- average_listing_price (FLOAT64)
- average_listing_price_mm (FLOAT64)
- average_listing_price_yy (FLOAT64)
- median_days_on_market (INT64)
- median_days_on_market_mm (FLOAT64)
- median_days_on_market_yy (FLOAT64)
- median_listing_price (FLOAT64)
- median_listing_price_mm (FLOAT64)
- median_listing_price_per_square_foot (FLOAT64)
- median_listing_price_per_square_foot_mm (FLOAT64)
- median_listing_price_per_square_foot_yy (FLOAT64)
- median_listing_price_yy (FLOAT64)
- median_square_feet (FLOAT64)
- median_square_feet_mm (FLOAT64)
- median_square_feet_yy (FLOAT64)
- month_date_yyyymm (STRING)
- new_listing_count (INT64)
- new_listing_count_mm (FLOAT64)
- new_listing_count_yy (FLOAT64)
- pending_listing_count (FLOAT64)
- pending_listing_count_mm (FLOAT64)
- pending_listing_count_yy (FLOAT64)
- pending_ratio (FLOAT64)
- pending_ratio_mm (FLOAT64)
- pending_ratio_yy (FLOAT64)
- price_increased_count (INT64)
- price_increased_count_mm (FLOAT64)
- price_increased_count_yy (FLOAT64)
- price_increased_share (FLOAT64)
- price_increased_share_mm (FLOAT64)
- price_increased_share_yy (FLOAT64)
- price_reduced_count (FLOAT64)
- price_reduced_count_mm (FLOAT64)
- price_reduced_count_yy (FLOAT64)
- price_reduced_share (FLOAT64)
- price_reduced_share_mm (FLOAT64)
- price_reduced_share_yy (FLOAT64)
- quality_flag (FLOAT64)
- state (STRING)
- state_id (STRING)
- total_listing_count (INT64)
- total_listing_count_mm (FLOAT64)
- total_listing_count_yy (FLOAT64)
schema_hash: 36323ae9a667a5738e82100dbb5c34f146458c57608d7261989108d26ec763ee

---
# Comprehensive Summary: US Real Estate Data - State Inventory Core Metrics

## Overall Dataset Characteristics

### Basic Statistics
- **Total Rows**: 5,661 records
- **Geographic Coverage**: 51 unique states (including DC)
- **Time Series Data**: Month-over-month (mm) and year-over-year (yy) metrics present
- **Data Quality**: Generally high quality with ~11% null values in comparative metrics (mm/yy columns)

### Key Observations
- This appears to be a time-series dataset tracking real estate inventory metrics at the state level
- Contains both absolute values and percentage changes (month-over-month and year-over-year)
- The `month_date_yyyymm` column is 100% null, suggesting date information may be stored elsewhere or this is a snapshot
- Price ranges vary significantly by state (median listing prices from $129,913 to $886,500)
- Quality flag present with ~11% null values, predominantly showing 0.0 or 1.0 values

## Column Details

### Geographic Identifiers
- **state** (STRING): Full state names; 51 unique values; no nulls
- **state_id** (STRING): Two-letter state codes (e.g., AL, AZ, CA); 51 unique values; no nulls
- *Use Case*: Primary keys for filtering and grouping by geography

### Listing Counts (Absolute Values)
- **total_listing_count** (INT64): Range 803-231,347; no nulls; 5,310 unique values
- **active_listing_count** (INT64): Range 720-182,589; no nulls; 5,163 unique values
- **new_listing_count** (INT64): Range 290-53,332; no nulls; 3,910 unique values
- **pending_listing_count** (FLOAT64): Range 0-82,071; 0.48% nulls; 4,726 unique values
- **price_reduced_count** (FLOAT64): Range 72-71,888; no nulls; 3,275 unique values
- **price_increased_count** (INT64): Range 0-9,466; no nulls; 1,091 unique values

### Price Metrics (Absolute Values)
- **average_listing_price** (FLOAT64): Range $206,417-$1,730,505; no nulls
- **median_listing_price** (FLOAT64): Range $129,913-$886,500; no nulls; 2,660 unique values
- **median_listing_price_per_square_foot** (FLOAT64): Range $79-$737; no nulls; 484 unique values
- *Pattern*: Significant variation across states reflecting regional market differences

### Property Characteristics
- **median_square_feet** (FLOAT64): Range 987-2,798 sq ft; no nulls; 1,063 unique values
- **median_days_on_market** (INT64): Range 13-157 days; no nulls; 130 unique values
- *Pattern*: Relatively narrow distribution suggesting standardized home sizes

### Market Activity Ratios
- **pending_ratio** (FLOAT64): Range 0-3.212; 0.48% nulls; 4,535 unique values
- **price_reduced_share** (FLOAT64): Range 0.0254-0.4089; no nulls; 1,944 unique values
- **price_increased_share** (FLOAT64): Range 0-0.1302; no nulls; 582 unique values
- *Note*: These ratios indicate market dynamics and pricing pressure

### Month-over-Month Changes (mm suffix)
All mm columns have ~10.81-11.25% null values, representing percentage changes:
- **total_listing_count_mm**: Range -0.3592 to 0.7739
- **active_listing_count_mm**: Range -0.3074 to 0.6116
- **new_listing_count_mm**: Range -0.6912 to 2.2457
- **pending_listing_count_mm**: Range -0.9734 to 15.9403
- **average_listing_price_mm**: Range -0.4512 to 0.9244
- **median_listing_price_mm**: Range -0.1038 to 0.1135
- **median_listing_price_per_square_foot_mm**: Range -0.1165 to 0.1178
- **median_square_feet_mm**: Range -0.101 to 0.1784
- **median_days_on_market_mm**: Range -0.6023 to 0.5873
- **pending_ratio_mm**: Range -0.8669 to 1.1954
- **price_reduced_count_mm**: Range -0.7625 to 2.9498
- **price_reduced_share_mm**: Range -0.1286 to 0.1132
- **price_increased_count_mm**: Range -1.0 to 63.0
- **price_increased_share_mm**: Range -0.0702 to 0.1023

### Year-over-Year Changes (yy suffix)
All yy columns have ~10.81-11.45% null values, representing percentage changes:
- **total_listing_count_yy**: Range -0.4954 to 1.1688
- **active_listing_count_yy**: Range -0.7173 to 2.3532
- **new_listing_count_yy**: Range -0.7398 to 2.0644
- **pending_listing_count_yy**: Range -0.9777 to 16.1045
- **average_listing_price_yy**: Range -0.3896 to 1.0508
- **median_listing_price_yy**: Range -0.2071 to 0.4101
- **median_listing_price_per_square_foot_yy**: Range -0.095 to 0.4914
- **median_square_feet_yy**: Range -0.3058 to 0.2676
- **median_days_on_market_yy**: Range -0.7155 to 1.6271
- **pending_ratio_yy**: Range -2.5872 to 2.5949
- **price_reduced_count_yy**: Range -0.8464 to 5.7706
- **price_reduced_share_yy**: Range -0.2464 to 0.3025
- **price_increased_count_yy**: Range -1.0 to 57.0
- **price_increased_share_yy**: Range -0.1175 to 0.1029

### Data Quality Column
- **quality_flag** (FLOAT64): 10.81% nulls; only values are 0.0 and 1.0
- *Interpretation*: Likely indicates data quality or completeness warnings

### Missing/Unused Column
- **month_date_yyyymm** (STRING): 100% null; no data populated

## Query Considerations

### Recommended Filtering Columns
1. **state/state_id**: Primary geographic filter
2. **quality_flag**: Filter out low-quality records (WHERE quality_flag = 0.0)
3. **median_listing_price**: Price range filters
4. **median_days_on_market**: Market velocity analysis
5. **total_listing_count**: Market size filters

### Recommended Grouping/Aggregation Columns
1. **state/state_id**: Geographic aggregations
2. All absolute value columns can be summed/averaged
3. Price metrics suitable for percentile calculations
4. Time-series analysis using mm/yy columns

### Potential Join Keys
- **state_id**: Can join with other state-level demographic or economic data
- **state**: Alternative join key for state-level tables

### Data Quality Considerations
1. **Null Handling**: ~11% of comparative metrics (mm/yy) are null - may represent first observation in time series or data quality issues
2. **month_date_yyyymm**: Completely empty - temporal context must come from external source
3. **pending_listing_count**: Uses FLOAT64 instead of INT64 (unlike other counts)
4. **Quality Flag**: Should be evaluated before analysis - consider filtering WHERE quality_flag = 0.0
5. **Outliers**: Some extreme values in yy/mm changes (e.g., pending_listing_count_mm up to 15.94) may indicate data anomalies or genuine market shocks

### Key Metrics for Analysis
- **Market Health**: pending_ratio, median_days_on_market
- **Price Trends**: median_listing_price with yy/mm changes
- **Inventory Levels**: active_listing_count, total_listing_count with trends
- **Pricing Pressure**: price_reduced_share, price_increased_share
- **Market Activity**: new_listing_count with trends

## Keywords
real estate, housing market, inventory metrics, state-level data, listing prices, median home prices, days on market, pending sales, active listings, price changes, month-over-month, year-over-year, market trends, housing inventory, price per square foot, new listings, price reductions, market velocity, geographic analysis, time series data

## Table and Column Documentation

### Table Comment
No table comment provided in the analysis.

### Column Comments
No individual column comments were provided in the analysis report.