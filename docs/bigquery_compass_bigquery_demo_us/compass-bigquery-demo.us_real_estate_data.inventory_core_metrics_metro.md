---
columns:
- active_listing_count (INT64)
- active_listing_count_mm (FLOAT64)
- active_listing_count_yy (FLOAT64)
- average_listing_price (FLOAT64)
- average_listing_price_mm (FLOAT64)
- average_listing_price_yy (FLOAT64)
- cbsa_code (INT64)
- cbsa_title (STRING)
- householdrank (INT64)
- median_days_on_market (FLOAT64)
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
- total_listing_count (INT64)
- total_listing_count_mm (FLOAT64)
- total_listing_count_yy (FLOAT64)
schema_hash: 6270d365685bef4b40bf9d4f9061148c6ee6c0642b9d6a5bf4f5860252556ccf

---
# Table Summary: compass-bigquery-demo.us_real_estate_data.inventory_core_metrics_metro

## Overall Dataset Characteristics

- **Total Rows**: 102,675
- **Data Type**: US real estate inventory metrics aggregated by metropolitan statistical areas (CBSA)
- **Time Period Coverage**: The dataset appears to represent a single time period snapshot, as the `month_date_yyyymm` column is completely null (100% null values)
- **Geographic Scope**: 925 unique metropolitan areas across the United States
- **Data Quality**: Generally good with most core metrics having complete data, though some calculated fields have higher null percentages

## Column Details

### Geographic Identifiers
- **cbsa_title** (STRING): Metropolitan area names with no null values (925 unique areas)
- **cbsa_code** (INT64): Numeric CBSA codes ranging from 10,100 to 49,820 with no null values
- **householdrank** (INT64): Ranking system from 1 to 925, likely based on household count or market size

### Temporal Data
- **month_date_yyyymm** (STRING): Completely null (100%), indicating this is likely a single time period snapshot

### Core Price Metrics
- **median_listing_price** (FLOAT64): Complete data, ranging from $19,900 to $5.5M
- **average_listing_price** (FLOAT64): Complete data, ranging from $44K to $23.5M
- **median_listing_price_per_square_foot** (FLOAT64): Complete data, ranging from $22 to $1,778 per sq ft
- **median_square_feet** (FLOAT64): Complete data, ranging from 892 to 6,000 sq ft

### Inventory Metrics
- **active_listing_count** (INT64): Complete data, ranging from 0 to 69,796 listings
- **new_listing_count** (INT64): Complete data, ranging from 0 to 27,262 listings
- **total_listing_count** (INT64): Complete data, ranging from 1 to 83,125 listings
- **pending_listing_count** (FLOAT64): 2.7% null values, ranging from 0 to 28,578

### Market Activity Metrics
- **median_days_on_market** (FLOAT64): Nearly complete (0.01% null), ranging from 3 to 322 days
- **price_increased_count** (INT64): Complete data, ranging from 0 to 4,978
- **price_reduced_count** (FLOAT64): Complete data, ranging from 0 to 22,456
- **pending_ratio** (FLOAT64): 2.7% null values, ranging from 0 to 8.0

### Share Metrics
- **price_increased_share** (FLOAT64): Complete data, ranging from 0% to 38.15%
- **price_reduced_share** (FLOAT64): Complete data, ranging from 0% to 66.67%

### Month-over-Month (mm) Change Metrics
All mm metrics have 10.81% null values, indicating these calculations may not be available for all markets:
- Price changes: -55% to +299% for median listing price
- Inventory changes: -100% to +2,438% for active listings
- Market timing changes: -94% to +378% for days on market

### Year-over-Year (yy) Change Metrics
Similar null patterns to mm metrics (10.81-14.41% null), with wider ranges:
- Price changes: -78% to +498% for median listing price
- Inventory changes: -100% to +9,150% for active listings
- Market timing changes: -88% to +757% for days on market

### Data Quality Indicator
- **quality_flag** (FLOAT64): 10.81% null values, binary indicator (0.0 or 1.0) for data quality

## Query Considerations

### Good for Filtering
- **cbsa_title**: Metropolitan area names for geographic filtering
- **cbsa_code**: Numeric codes for efficient geographic joins
- **householdrank**: Market size ranking for segmentation
- **quality_flag**: Data quality filtering

### Good for Grouping/Aggregation
- **householdrank**: Market size tiers
- **cbsa_title**: Geographic groupings
- Price and inventory ranges for market segmentation

### Potential Join Keys
- **cbsa_code**: Primary key for joining with other CBSA-level datasets
- **cbsa_title**: Alternative join key (though less efficient)

### Data Quality Considerations
- **Missing temporal data**: All queries should account for the absence of time period information
- **Change metrics availability**: ~11% of records missing mm/yy calculations
- **Price increase metrics**: 54-55% null values suggest limited price increase activity
- **Pending data gaps**: 2.7% missing pending listing data
- **Quality flag usage**: Consider filtering by quality_flag = 0.0 for highest quality data

## Keywords

Real estate, housing market, inventory metrics, CBSA, metropolitan areas, listing prices, market activity, days on market, price changes, pending sales, active listings, new listings, price per square foot, median square feet, housing statistics, market analysis, geographic data, US housing market

## Table and Column Documentation

**Table Comment**: Not provided in the analysis

**Column Comments**: No column-specific comments were provided in the source analysis