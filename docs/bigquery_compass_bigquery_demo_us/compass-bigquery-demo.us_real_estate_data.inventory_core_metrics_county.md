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
# Table Summary: US Real Estate Inventory Core Metrics (County Level)

## Overall Dataset Characteristics

**Total Rows:** 344,538

This table contains comprehensive real estate market metrics at the county level across the United States. The dataset tracks various listing statistics, pricing information, and market dynamics over time. Notably, the `month_date_yyyymm` column is entirely null (100%), suggesting temporal information may be stored elsewhere or this represents a snapshot dataset. The data quality varies significantly by metric, with some columns having high null percentages (70%+) while core metrics like county identifiers and basic listing counts have near-complete data (<1% null).

**Geographic Coverage:** 3,135+ unique counties across all US states (identifiable by state abbreviations in county names and FIPS codes ranging from 1001 to 56045).

**Data Quality Observations:**
- Core metrics (median listing price, active listings, county identifiers) have excellent coverage (<0.1% nulls)
- Price change metrics show high null rates (70-75%), likely indicating insufficient data for these calculations in many counties
- Month-over-month (mm) and year-over-year (yy) comparison metrics have moderate null rates (10-20%)
- Quality flag present but 10.72% null, suggesting data quality assessment may be incomplete

## Column Details

### Geographic Identifiers

**county_name** (STRING)
- Format: "county name, state abbreviation" (e.g., "abbeville, sc")
- 3,135 unique counties with complete coverage (0% null)
- Serves as human-readable geographic identifier
- Examples: "morris, nj", "sumner, tn", "claiborne, tn"

**county_fips** (INT64)
- Standard 5-digit FIPS codes (1001-56045)
- 3,141 unique values (slightly more than county names, suggesting potential data granularity differences)
- 0% null - reliable join key
- Comment: Primary geographic key for joining with other datasets

### Temporal Field

**month_date_yyyymm** (STRING)
- **100% NULL** - Non-functional column
- Intended format likely YYYYMM based on name
- Temporal context must be derived from context or external metadata

### Price Metrics

**median_listing_price** (FLOAT64)
- Range: $1,311 to $13,000,000
- 52,273 unique values indicating granular pricing
- 0.02% null - highly reliable
- Sample values show typical ranges: $84,375 (rural), $255,000 (suburban), $695,000 (affluent areas)

**median_listing_price_mm** (FLOAT64)
- Month-over-month price change rate
- Range: -99.71% to +57,032% (extreme values suggest data quality issues or calculation anomalies)
- 10.89% null
- Negative values indicate price decreases, positive indicate increases

**median_listing_price_yy** (FLOAT64)
- Year-over-year price change rate
- Range: -99.68% to +22,287%
- 11.27% null
- Shows longer-term market trends

**average_listing_price** (FLOAT64)
- Range: $5,000 to $142,882,807 (extreme high suggests luxury/outlier properties)
- 252,993 unique values (most granular price metric)
- 0.02% null
- Higher variability than median due to outlier sensitivity

**average_listing_price_mm/yy** (FLOAT64)
- Similar patterns to median price changes
- 10.89% and 11.27% null respectively

**median_listing_price_per_square_foot** (FLOAT64)
- Range: $0 to $56,250/sqft
- 1,378 unique values
- 0.10% null
- Key metric for normalized price comparisons
- Sample: $89-$310/sqft showing geographic price variation

**median_listing_price_per_square_foot_mm/yy** (FLOAT64)
- 10.96% and 11.37% null respectively
- Wide ranges indicate volatile price-per-sqft changes in some markets

### Inventory Metrics

**active_listing_count** (FLOAT64)
- Current available properties for sale
- Range: 0 to 23,258 listings
- 0.01% null - highly reliable
- 6,008 unique values
- Critical for market supply analysis

**active_listing_count_mm/yy** (FLOAT64)
- Inventory change rates
- Range -100% to +3,250% (mm), -100% to +9,150% (yy)
- ~11% null for both

**new_listing_count** (FLOAT64)
- Fresh market entries
- Range: 0 to 9,888 listings
- 0.01% null
- 2,274 unique values
- Even numbers suggest possible aggregation

**new_listing_count_mm/yy** (FLOAT64)
- 19.15% and 19.51% null - higher than other mm/yy metrics
- Indicates new listing data may be less available historically

**total_listing_count** (FLOAT64)
- Combined inventory metric
- Range: 0 to 33,580
- 0.01% null
- 7,738 unique values

**pending_listing_count** (FLOAT64)
- Properties under contract
- Range: 0 to 14,211
- 7.28% null - moderate missing data
- Important demand indicator

**pending_ratio** (FLOAT64)
- Pending/Active ratio showing market heat
- Range: 0 to 11.5
- 7.32% null
- Values >1 indicate very hot markets

### Market Velocity

**median_days_on_market** (FLOAT64)
- Time to sell/contract
- Range: 1 to 365 days
- 0.11% null
- 365 unique values (appears capped at 1 year)
- Key liquidity indicator

**median_days_on_market_mm/yy** (FLOAT64)
- ~11% null
- Shows market acceleration/deceleration

### Price Change Activity

**price_increased_count** (FLOAT64)
- Listings with price hikes
- Range: 0 to 1,666
- 0.01% null
- 492 unique values (lower than other counts)

**price_increased_count_mm/yy** (FLOAT64)
- **74.31% and 73.67% NULL** - Very high missing data
- Suggests this metric is only calculated for subset of markets

**price_increased_share** (FLOAT64)
- Proportion of listings with price increases
- Range: 0 to 4.0 (values >1.0 likely data errors)
- 0.04% null
- 1,717 unique values

**price_reduced_count** (FLOAT64)
- Listings with price cuts
- Range: 0 to 12,596
- 0.01% null
- 1,930 unique values
- Generally higher counts than price increases

**price_reduced_count_mm/yy** (FLOAT64)
- 25.53% and 25.05% null - moderate missing data
- More available than price_increased metrics

**price_reduced_share** (FLOAT64)
- Range: 0 to 4.0
- 0.04% null
- 3,919 unique values (more granular than price_increased_share)

### Property Characteristics

**median_square_feet** (FLOAT64)
- Property size metric
- Range: 4 to 30,902 sqft
- 0.10% null
- 3,322 unique values
- Samples: 1,497-2,662 sqft typical

**median_square_feet_mm/yy** (FLOAT64)
- 10.96% and 11.37% null
- Shows shifting property size preferences

### Data Quality

**quality_flag** (FLOAT64)
- Binary indicator: 0.0 or 1.0
- 10.72% null
- Likely indicates data reliability (1.0 = good quality)
- Sample data shows mix of 0.0 and 1.0 values

## Query Considerations

### Excellent for Filtering:
- **county_fips**: Precise geographic filtering with complete data
- **county_name**: Human-readable geographic filtering
- **quality_flag**: Filter for data quality when not null
- **active_listing_count**: Non-zero to exclude inactive markets
- Price ranges for market segmentation

### Good for Aggregation/Grouping:
- Geographic groupings (by state via county_name parsing)
- Market segments (by price ranges, inventory levels)
- Market health categories (by pending_ratio, days_on_market)

### Strong Metrics for Analysis:
- **median_listing_price**: Most reliable price metric
- **active_listing_count**: Supply indicator
- **median_days_on_market**: Velocity metric
- **pending_ratio**: Demand indicator
- **median_listing_price_per_square_foot**: Normalized pricing

### Caution Areas:
- **month_date_yyyymm**: Unusable (100% null)
- **price_increased_count metrics**: 70%+ null, use cautiously
- Extreme values in mm/yy metrics may need filtering
- Share metrics with values >1.0 may indicate calculation errors

### Potential Join Keys:
- **county_fips**: Standard government identifier for census, economic data
- **county_name**: Can join to geographic databases (may need state parsing)

### Missing Temporal Context:
- No reliable date field means temporal analysis requires external date information
- All mm/yy metrics suggest time-series data, but specific dates are missing
- Query design must accommodate this limitation or join to date dimension

## Keywords

real estate, housing market, property listings, county data, inventory metrics, median price, days on market, pending sales, active listings, new listings, price per square foot, market velocity, supply and demand, FIPS codes, geographic analysis, housing statistics, property metrics, market trends, listing counts, price changes, price increases, price reductions, square footage, real estate analytics, US counties, housing inventory, market indicators, pending ratio, time series, month over month, year over year, comparative metrics, quality flag

## Table and Column Documentation

**Table Comment:** Not provided

**Column Comments:**
- county_fips: Standard 5-digit FIPS codes for US counties
- No other column comments provided in the analysis