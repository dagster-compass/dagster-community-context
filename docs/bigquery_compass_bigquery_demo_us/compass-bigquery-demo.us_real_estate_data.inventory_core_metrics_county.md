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
# Table Documentation: us_real_estate_data.inventory_core_metrics_county

## Overview

This table contains comprehensive real estate inventory metrics at the county level across the United States. With **344,538 total rows**, it provides detailed information about listing prices, inventory counts, market dynamics, and property characteristics for 3,135+ unique counties.

### Critical Data Quality Note
- **The `month_date_yyyymm` column is 100% NULL across all records**, indicating missing temporal data that would typically identify the reporting period for each row
- Despite this, year-over-year (yy) and month-over-month (mm) comparisons are present in the data, suggesting temporal relationships exist but the date field itself is unpopulated

## Table Structure

### Geographic Identifiers
- **county_name** (STRING): County name with state abbreviation (e.g., "guilford, nc", "upson, ga")
  - No nulls, 3,135 unique values
  - Format: lowercase county name, state abbreviation
  
- **county_fips** (INT64): Federal Information Processing Standards code for counties
  - No nulls, 3,141 unique values
  - Range: 1001 to 56045
  - Primary geographic key for joining to other datasets

## Core Metrics Categories

### 1. Listing Prices

**median_listing_price** (FLOAT64)
- Nearly complete (0.02% null)
- Range: $1,311 to $13,000,000
- 52,273 unique values indicating high granularity
- Sample values show typical ranges: $124,900, $129,950, $299,900

**average_listing_price** (FLOAT64)
- Nearly complete (0.02% null)
- Significantly wider range: $5,000 to $142,882,807
- 252,993 unique values (highest uniqueness in table)
- More susceptible to outliers than median

**median_listing_price_per_square_foot** (FLOAT64)
- 0.10% null
- Range: $0 to $56,250
- 1,378 unique values
- Key metric for price normalization

### 2. Inventory Counts

**active_listing_count** (FLOAT64)
- 0.01% null, highly complete
- Range: 0 to 23,258 listings
- 6,008 unique values
- Critical for market supply analysis

**new_listing_count** (FLOAT64)
- 0.01% null
- Range: 0 to 9,888
- Measures fresh inventory entering market

**total_listing_count** (FLOAT64)
- 0.01% null
- Range: 0 to 33,580
- Comprehensive inventory measure

**pending_listing_count** (FLOAT64)
- 7.28% null (higher than other counts)
- Range: 0 to 14,211
- Indicates properties under contract

### 3. Market Velocity Metrics

**median_days_on_market** (FLOAT64)
- 0.11% null
- Range: 1 to 365 days
- 365 unique values (suggests day-level precision)
- Key indicator of market liquidity

**pending_ratio** (FLOAT64)
- 7.32% null
- Range: 0.0 to 11.5
- Ratio of pending to active listings
- Market demand indicator

### 4. Price Change Activity

**price_increased_count** (FLOAT64)
- 0.01% null, but **74.31% null for month-over-month** changes
- Range: 0 to 1,666 listings

**price_reduced_count** (FLOAT64)
- 0.01% null, but **25.05% null for month-over-month** changes
- Range: 0 to 12,596 listings
- More complete data than price increases

**price_increased_share** and **price_reduced_share** (FLOAT64)
- Proportions ranging 0.0 to 4.0
- Normalized metrics less affected by market size

### 5. Property Characteristics

**median_square_feet** (FLOAT64)
- 0.10% null
- Range: 4 to 30,902 square feet
- 3,322 unique values
- Sample values (1,596, 1,652, 2,021) show typical home sizes

### 6. Temporal Comparison Metrics

All core metrics have companion fields for:
- **_mm** (month-over-month): Showing percentage/ratio changes
  - Generally 10-19% null rates
  - Ranges often include -1.0 (complete decrease) to high positive values
  
- **_yy** (year-over-year): Showing annual comparisons
  - Generally 11-20% null rates
  - Wider ranges than month-over-month

**Notable null patterns:**
- Price increase comparisons: 73-74% null (sparse data)
- Price reduction comparisons: 25% null (more complete)
- Pending count comparisons: 17-20% null
- Other metrics: 10-11% null (fairly complete)

### 7. Data Quality Indicator

**quality_flag** (FLOAT64)
- 10.72% null
- Binary values: 0.0 or 1.0
- Likely indicates data reliability or completeness threshold
- Consider filtering on this field for high-quality analysis

## Key Patterns and Distributions

1. **Geographic Coverage**: Data spans all US states based on FIPS codes (01xxx = Alabama through 56xxx = Wyoming)

2. **Market Size Variation**: Enormous range in listing counts (0 to 33,580) reflects diversity from rural to major metropolitan counties

3. **Price Dispersion**: 
   - Median prices range nearly 10,000x (min to max)
   - Average prices show even greater dispersion
   - Suggests mix of rural, suburban, and high-cost urban markets

4. **Temporal Comparison Completeness**:
   - Year-over-year data more complete than month-over-month
   - Price reduction data more complete than price increase data
   - Suggests data collection methodology differences

## Query Considerations

### Excellent for Filtering:
- **county_fips**: Precise geographic filtering
- **county_name**: Human-readable geographic filtering (ensure lowercase, with state)
- **quality_flag**: Data quality filtering (use = 1.0 for high quality)
- **active_listing_count**: Market size filtering (e.g., > 100 for active markets)

### Excellent for Aggregation/Grouping:
- **county_name**: Geographic rollups
- Geographic regions (derived from FIPS code ranges)
- Price ranges (bucketing median_listing_price)
- Market velocity tiers (based on median_days_on_market)

### Potential Join Keys:
- **county_fips**: Standard for joining to census, demographic, or other geographic data
- **county_name**: Human-readable joins (but requires consistent formatting)

### Important Caveats:

1. **Missing Date Dimension**: Without month_date_yyyymm populated, temporal analysis requires careful consideration of how data is organized. The presence of _mm and _yy fields suggests data has temporal structure but lacks explicit date stamps.

2. **Null Handling**: 
   - Price increase metrics have 70%+ nulls - use COALESCE or filter appropriately
   - Most core metrics are <1% null - safe for calculations
   - Temporal comparison fields 10-25% null - consider in trend analysis

3. **Outlier Awareness**: 
   - Maximum values for prices and counts suggest outliers or data quality issues
   - Consider percentile-based filtering for robust analysis
   - The $142M average listing price maximum is likely an anomaly

4. **Rate Calculation Context**: The _mm and _yy fields contain rates (e.g., 0.1278 = 12.78% change), not absolute differences

5. **Data Completeness Patterns**: Counties with low listing counts may have higher null rates in derived metrics

## Keywords

real estate, housing market, inventory, listings, median price, county data, market metrics, days on market, pending sales, price per square foot, active listings, new listings, price reductions, market trends, housing supply, real estate analytics, county-level data, FIPS codes, property metrics, market velocity, housing inventory, listing counts, price changes, real estate statistics, geographic analysis, market dynamics

## Table and Column Documentation

**Table Comment**: Not provided

**Column Comments**: Not provided for any columns