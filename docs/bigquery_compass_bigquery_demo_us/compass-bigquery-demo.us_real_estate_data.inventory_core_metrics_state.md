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
# Table Analysis Summary: US Real Estate Data - State-Level Inventory Core Metrics

## Overall Dataset Characteristics

- **Total Rows**: 5,661 records
- **Geographic Coverage**: 51 US states including District of Columbia
- **Data Quality**: Generally good with most core metrics having complete data
- **Missing Data Pattern**: Approximately 10.81% of rows have missing values for year-over-year and month-over-month comparison metrics, suggesting these may be newer records or periods without historical comparisons
- **One Column Completely Empty**: `month_date_yyyymm` has 100% null values

## Column Details

### Geographic Identifiers
- **state** (STRING): Complete data for all 51 US states and DC
- **state_id** (STRING): Two-letter state abbreviations, complete data

### Core Listing Metrics (Complete Data)
- **total_listing_count** (INT64): Range 803-231,347, represents total active listings
- **active_listing_count** (INT64): Range 720-182,589, subset of total listings
- **new_listing_count** (INT64): Range 290-53,332, new listings added
- **pending_listing_count** (FLOAT64): Range 0-82,071, listings under contract

### Price Metrics (Complete Data)
- **average_listing_price** (FLOAT64): Range $206,417-$1,730,505
- **median_listing_price** (FLOAT64): Range $129,913-$886,500
- **median_listing_price_per_square_foot** (FLOAT64): Range $79-$737 per sq ft

### Property Characteristics (Complete Data)
- **median_square_feet** (FLOAT64): Range 987-2,798 sq ft
- **median_days_on_market** (INT64): Range 13-157 days

### Market Activity Metrics (Complete Data)
- **pending_ratio** (FLOAT64): Range 0-3.212, ratio of pending to active listings
- **price_reduced_count** (FLOAT64): Range 72-71,888 listings with price reductions
- **price_reduced_share** (FLOAT64): Range 0.0254-0.4089, percentage of listings with price reductions
- **price_increased_count** (INT64): Range 0-9,466 listings with price increases
- **price_increased_share** (FLOAT64): Range 0-0.1302, percentage of listings with price increases

### Change Metrics (10.81% Missing)
All metrics ending in `_yy` (year-over-year) and `_mm` (month-over-month) have consistent missing data:
- **Values represent percentage changes** from previous periods
- **YoY changes** generally show larger ranges than MoM changes
- **Missing pattern** suggests these are calculated fields unavailable for certain time periods

### Data Quality Indicator
- **quality_flag** (FLOAT64): Binary indicator (0.0 or 1.0) with 10.81% missing values

### Completely Missing Column
- **month_date_yyyymm** (STRING): 100% null values, likely unused date field

## Query Considerations

### Good for Filtering
- **state/state_id**: Geographic filtering by state
- **median_days_on_market**: Market speed filtering (hot/cold markets)
- **quality_flag**: Data quality filtering when not null
- **Price ranges**: Filter by price tiers using median_listing_price

### Good for Grouping/Aggregation
- **state/state_id**: Geographic grouping
- **Price ranges**: Create price tier buckets
- **Market activity levels**: Group by pending_ratio or days_on_market ranges

### Potential Relationships
- **State identifiers**: Could join with other geographic datasets
- **No obvious temporal keys**: month_date_yyyymm is empty
- **Price metrics**: Strong relationships between different price measures

### Data Quality Considerations
- **~10.81% missing data** for comparison metrics should be handled in queries
- **month_date_yyyymm should be excluded** from queries (100% null)
- **quality_flag** could be used to filter for higher quality records
- **Wide value ranges** in some metrics may require outlier handling

## Keywords

Real estate, housing market, inventory metrics, state data, listing prices, market activity, pending sales, price changes, days on market, square footage, geographic analysis, housing statistics, property metrics, market trends

## Table and Column Documentation

**Table Comment**: Not provided

**Column Comments**: No individual column comments were provided in the source data.