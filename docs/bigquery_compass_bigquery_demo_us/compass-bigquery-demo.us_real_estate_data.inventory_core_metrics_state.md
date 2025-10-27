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
# Dataset Summary: US Real Estate Inventory Core Metrics by State

## Overall Dataset Characteristics

- **Total Rows**: 5,661 records
- **Geographic Scope**: State-level real estate data across all 51 US states (including DC)
- **Data Quality**: Mixed quality with systematic null patterns - approximately 10.81% of records missing values for year-over-year and month-over-month change metrics
- **Time Series Nature**: Contains both absolute values and percentage changes (month-over-month "_mm" and year-over-year "_yy" suffixes)
- **Notable Pattern**: One column (`month_date_yyyymm`) is completely null, suggesting temporal information may be stored externally

## Column Details

### Geographic Identifiers
- **state** (STRING): Full state names, no nulls, 51 unique values
- **state_id** (STRING): Two-letter state abbreviations, no nulls, 51 unique values

### Core Inventory Metrics (Absolute Values)
- **total_listing_count** (INT64): Total property listings per state, ranging 803-231,347, no nulls
- **active_listing_count** (INT64): Active listings, ranging 720-182,589, no nulls  
- **new_listing_count** (INT64): New listings, ranging 290-53,332, no nulls
- **pending_listing_count** (FLOAT64): Pending listings, ranging 0-82,071, minimal nulls (0.48%)

### Price Metrics (Absolute Values)
- **average_listing_price** (FLOAT64): Average prices $206K-$1.73M, no nulls
- **median_listing_price** (FLOAT64): Median prices $130K-$887K, no nulls
- **median_listing_price_per_square_foot** (FLOAT64): Price per sq ft $79-$737, no nulls

### Property Characteristics
- **median_square_feet** (FLOAT64): Property sizes 987-2,798 sq ft, no nulls
- **median_days_on_market** (INT64): Market time 13-157 days, no nulls

### Market Activity Ratios
- **pending_ratio** (FLOAT64): Pending/total ratio 0.0-3.212, minimal nulls (0.48%)
- **price_reduced_share** (FLOAT64): Share of price reductions 0.025-0.409, no nulls
- **price_increased_share** (FLOAT64): Share of price increases 0.0-0.130, no nulls

### Count Metrics for Price Changes
- **price_reduced_count** (FLOAT64): Count of price reductions 72-71,888, no nulls
- **price_increased_count** (INT64): Count of price increases 0-9,466, no nulls

### Change Metrics (Month-over-Month "_mm" suffix)
All have ~10.81-11.25% nulls, representing percentage changes:
- **total_listing_count_mm**: -0.36 to +0.77
- **active_listing_count_mm**: -0.31 to +0.61
- **new_listing_count_mm**: -0.69 to +2.25
- **pending_listing_count_mm**: -0.97 to +15.94
- **average_listing_price_mm**: -0.45 to +0.92
- **median_listing_price_mm**: -0.10 to +0.11
- **median_listing_price_per_square_foot_mm**: -0.12 to +0.12
- **median_square_feet_mm**: -0.10 to +0.18
- **median_days_on_market_mm**: -0.60 to +0.59
- **pending_ratio_mm**: -0.87 to +1.20
- **price_reduced_share_mm**: -0.13 to +0.11
- **price_increased_share_mm**: -0.07 to +0.10
- **price_reduced_count_mm**: -0.76 to +2.95
- **price_increased_count_mm**: -1.0 to +63.0

### Change Metrics (Year-over-Year "_yy" suffix)
All have ~10.81-11.45% nulls, representing percentage changes:
- **total_listing_count_yy**: -0.50 to +1.17
- **active_listing_count_yy**: -0.72 to +2.35
- **new_listing_count_yy**: -0.74 to +2.06
- **pending_listing_count_yy**: -0.98 to +16.10
- **average_listing_price_yy**: -0.39 to +1.05
- **median_listing_price_yy**: -0.21 to +0.41
- **median_listing_price_per_square_foot_yy**: -0.10 to +0.49
- **median_square_feet_yy**: -0.31 to +0.27
- **median_days_on_market_yy**: -0.72 to +1.63
- **pending_ratio_yy**: -2.59 to +2.59
- **price_reduced_share_yy**: -0.25 to +0.30
- **price_increased_share_yy**: -0.12 to +0.10
- **price_reduced_count_yy**: -0.85 to +5.77
- **price_increased_count_yy**: -1.0 to +57.0

### Data Quality Indicator
- **quality_flag** (FLOAT64): Binary flag (0.0/1.0) with 10.81% nulls, likely indicating data reliability

### Temporal Column (Unused)
- **month_date_yyyymm** (STRING): 100% null values, appears to be unused

## Query Considerations

### Excellent for Filtering
- **state** and **state_id**: Perfect for geographic filtering
- **quality_flag**: For filtering reliable data (when not null)
- All absolute value metrics for range-based filtering

### Good for Grouping/Aggregation
- **state** and **state_id**: State-level analysis
- Ranges of absolute metrics can be binned for distribution analysis

### Potential Relationships
- **state** and **state_id**: Natural join keys for other geographic datasets
- Price metrics likely correlate with each other and property characteristics
- Change metrics ("_mm", "_yy") relate to their corresponding absolute values

### Data Quality Considerations
- **Systematic Nulls**: ~10.81% of records missing all change metrics - likely represents earliest time periods in dataset
- **Complete Null Column**: `month_date_yyyymm` should be avoided in queries
- **Mixed Nulls**: `pending_listing_count` and `pending_ratio` have different null patterns (0.48% vs 10.81%)
- **Quality Flag**: Consider filtering on `quality_flag = 0.0` for higher confidence data

### Recommended Query Patterns
- Filter by state for geographic analysis
- Use absolute values for current state analysis
- Use "_yy" suffixes for annual trend analysis  
- Use "_mm" suffixes for short-term trend analysis
- Join on state identifiers with other geographic datasets
- Consider null handling for change metrics in temporal analysis

## Keywords
real estate, inventory, listings, housing market, property prices, market metrics, state data, price trends, days on market, pending sales, active listings, price changes, square footage, geographic analysis, time series, percentage changes, market activity

## Table and Column Documentation
No explicit table or column comments are provided in the source data.