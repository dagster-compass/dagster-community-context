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
# Table Analysis Summary: compass-bigquery-demo.us_real_estate_data.inventory_core_metrics_state

## Overall Dataset Characteristics

- **Total Rows**: 5,661 records
- **Data Quality**: Generally good with most columns having no null values. However, several columns have consistent null patterns (~10.81% missing values)
- **Time Series Nature**: Contains month-over-month (mm) and year-over-year (yy) change metrics, indicating this is time-series real estate data
- **Geographic Coverage**: Covers all 51 US states and territories (including DC)
- **Data Pattern**: Appears to be monthly real estate inventory metrics aggregated at the state level

## Column Details

### Identifier Columns
- **state** (STRING): State names, no nulls, 51 unique values (all US states + DC)
- **state_id** (STRING): State abbreviations, no nulls, 51 unique values (standardized state codes)
- **month_date_yyyymm** (STRING): **100% null values** - appears to be unused/placeholder column

### Core Inventory Metrics
- **total_listing_count** (INT64): Complete data, range 803-231,347 listings
- **active_listing_count** (INT64): Complete data, range 720-182,589 listings  
- **new_listing_count** (INT64): Complete data, range 290-53,332 listings
- **pending_listing_count** (FLOAT64): 0.48% nulls, range 0-82,071 listings

### Price Metrics
- **average_listing_price** (FLOAT64): Complete data, range $206K-$1.73M
- **median_listing_price** (FLOAT64): Complete data, range $130K-$887K
- **median_listing_price_per_square_foot** (FLOAT64): Complete data, range $79-$737/sq ft

### Property Size Metrics
- **median_square_feet** (FLOAT64): Complete data, range 987-2,798 sq ft

### Market Activity Metrics
- **pending_ratio** (FLOAT64): 0.48% nulls, range 0-3.212
- **median_days_on_market** (INT64): Complete data, range 13-157 days
- **price_reduced_count** (FLOAT64): Complete data, range 72-71,888 reductions
- **price_reduced_share** (FLOAT64): Complete data, range 2.54%-40.89%
- **price_increased_count** (INT64): Complete data, range 0-9,466 increases
- **price_increased_share** (FLOAT64): Complete data, range 0%-13.02%

### Change Metrics (Time Comparisons)
**Month-over-Month Changes** (10.81%-11.25% nulls):
- Various *_mm columns showing percentage changes
- Range typically -100% to +100% for most metrics

**Year-over-Year Changes** (10.81%-11.43% nulls):
- Various *_yy columns showing percentage changes  
- Wider ranges indicating more volatility over annual periods

### Data Quality Indicator
- **quality_flag** (FLOAT64): 10.81% nulls, binary values (0.0, 1.0) indicating data quality status

## Query Considerations

### Good for Filtering
- **state/state_id**: Geographic filtering by state
- **quality_flag**: Filter for data quality (when not null)
- **median_days_on_market**: Market speed filtering
- Date-related filtering would require the month_date_yyyymm column to be populated

### Good for Grouping/Aggregation
- **state/state_id**: Geographic grouping
- Price ranges (can create buckets from price columns)
- Market activity levels (using days on market, pending ratios)

### Potential Join Keys
- **state_id**: Standard for joining with other state-level datasets
- **state**: Alternative join key for state-level data
- Missing viable time dimension due to null month_date_yyyymm

### Data Quality Considerations
- Consistent ~10.81% null pattern across change metrics suggests systematic data collection issues for certain time periods/states
- **month_date_yyyymm** being 100% null limits time-based analysis
- **pending_listing_count** and **pending_ratio** have slightly different null patterns (0.48% vs 11.25%/11.43%)
- All core inventory counts are complete (no nulls)

## Keywords
real estate, inventory, listings, housing market, state-level data, property prices, market metrics, days on market, pending sales, price changes, square footage, monthly data, yearly data, market trends

## Table and Column Documentation
No table comments or column comments are present in the provided schema.