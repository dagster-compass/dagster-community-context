---
columns:
- active_listing_count (FLOAT64)
- active_listing_count_mm (FLOAT64)
- active_listing_count_yy (FLOAT64)
- average_listing_price (FLOAT64)
- average_listing_price_mm (FLOAT64)
- average_listing_price_yy (FLOAT64)
- county_fips (INT64)
- county_name (STRING)
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
- new_listing_count (FLOAT64)
- new_listing_count_mm (FLOAT64)
- new_listing_count_yy (FLOAT64)
- pending_listing_count (FLOAT64)
- pending_listing_count_mm (FLOAT64)
- pending_listing_count_yy (FLOAT64)
- pending_ratio (FLOAT64)
- pending_ratio_mm (FLOAT64)
- pending_ratio_yy (FLOAT64)
- price_increased_count (FLOAT64)
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
- total_listing_count (FLOAT64)
- total_listing_count_mm (FLOAT64)
- total_listing_count_yy (FLOAT64)
schema_hash: 2ffe0feeb9432a86eef025e95a2af54c425d26745c0615ff163e6f8e4fb86e68

---
# Data Summary: US Real Estate Inventory Core Metrics by County

## Overall Dataset Characteristics

- **Total Rows**: 344,538 records
- **Geographic Coverage**: 3,141 unique counties across the United States (identified by FIPS codes)
- **Data Quality**: Generally good with most core metrics having very low null rates (<1%), though some derived metrics show higher null percentages
- **Key Data Issue**: The `month_date_yyyymm` field is 100% null, indicating missing temporal data that would typically identify the reporting period
- **Data Type**: Time-series real estate market data with month-over-month (mm) and year-over-year (yy) change indicators

## Column Details

### Geographic Identifiers
- **county_fips** (INT64): Complete data (0% null), 3,141 unique values ranging from 1001 to 56045. Primary geographic identifier following standard FIPS county codes.
- **county_name** (STRING): Complete data (0% null), 3,135 unique values. County names formatted as "county_name, state_abbreviation" (e.g., "cloud, ks").

### Temporal Data
- **month_date_yyyymm** (STRING): Critical data quality issue - 100% null values. This field should contain the reporting period but is completely missing.

### Price Metrics
- **median_listing_price** (FLOAT64): Nearly complete (0.02% null), wide range from $1,311 to $13M, indicating diverse market conditions.
- **median_listing_price_mm** (FLOAT64): 10.89% null, month-over-month changes ranging from -99.71% to +570%.
- **median_listing_price_yy** (FLOAT64): 11.27% null, year-over-year changes ranging from -99.68% to +222%.
- **average_listing_price** (FLOAT64): Nearly complete (0.02% null), extreme range up to $142M suggesting some luxury markets.
- **median_listing_price_per_square_foot** (FLOAT64): 0.10% null, ranges from $0 to $56,250 per sq ft.

### Inventory Metrics
- **active_listing_count** (FLOAT64): Nearly complete (0.01% null), ranges from 0 to 23,258 listings.
- **new_listing_count** (FLOAT64): Nearly complete (0.01% null), ranges from 0 to 9,888 listings.
- **total_listing_count** (FLOAT64): Nearly complete (0.01% null), ranges from 0 to 33,580 listings.
- **pending_listing_count** (FLOAT64): 7.28% null, ranges from 0 to 14,211 listings.

### Market Activity Metrics
- **median_days_on_market** (FLOAT64): 0.11% null, ranges from 1 to 365 days.
- **price_increased_count** (FLOAT64): Nearly complete (0.01% null), ranges from 0 to 1,666 listings.
- **price_reduced_count** (FLOAT64): Nearly complete (0.01% null), ranges from 0 to 12,596 listings.

### Share/Ratio Metrics
- **price_increased_share** (FLOAT64): 0.04% null, ranges from 0.0 to 4.0 (likely as decimal percentages).
- **price_reduced_share** (FLOAT64): 0.04% null, ranges from 0.0 to 4.0.
- **pending_ratio** (FLOAT64): 7.32% null, ranges from 0.0 to 11.5.

### Property Characteristics
- **median_square_feet** (FLOAT64): 0.10% null, ranges from 4 to 30,902 sq ft.

### Data Quality Indicator
- **quality_flag** (FLOAT64): 10.72% null, binary values (0.0, 1.0) indicating data quality assessment.

## Potential Query Considerations

### Good for Filtering
- **county_fips**: Excellent for geographic filtering
- **county_name**: Good for state-level or specific county analysis
- **quality_flag**: Important for filtering reliable data
- **Price ranges**: Various price metrics for market segment analysis

### Good for Grouping/Aggregation
- **county_name**: State-level aggregations (extract state from county_name)
- **Price tiers**: Create buckets based on median_listing_price
- **Market size**: Group by active_listing_count ranges
- **Geographic regions**: Group counties by FIPS code patterns

### Potential Join Keys
- **county_fips**: Primary key for joining with other county-level datasets
- **county_name**: Alternative join key (with careful handling of format)

### Data Quality Considerations
1. **Missing temporal data**: `month_date_yyyymm` is completely null - queries cannot filter by time period
2. **Higher null rates**: Price change metrics (mm/yy) have 10-25% null rates
3. **Extreme values**: Some price metrics show very high maximums that may need outlier handling
4. **Quality flag**: Use `quality_flag = 1.0` to ensure reliable data
5. **Derived metrics**: Month-over-month and year-over-year changes have higher null rates, especially for smaller markets

## Keywords
real estate, housing market, county data, inventory metrics, listing prices, market activity, days on market, price changes, pending sales, property characteristics, FIPS codes, geographic analysis, time series, market trends

## Table and Column Documentation
**Table Comment**: Not provided

**Column Comments**: Not provided