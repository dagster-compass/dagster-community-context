---
columns:
- active_listing_count (INT64)
- active_listing_count_mm (FLOAT64)
- active_listing_count_yy (FLOAT64)
- average_listing_price (FLOAT64)
- average_listing_price_mm (FLOAT64)
- average_listing_price_yy (FLOAT64)
- country (STRING)
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
- pending_listing_count (INT64)
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
schema_hash: e657215716a559308360810f9c2b29a688e8a830a64b7fd25300c324e416e4f2

---
# Comprehensive Table Summary: US Real Estate Inventory Core Metrics (Country Level)

## Overall Dataset Characteristics

- **Total Rows:** 111 records
- **Geographic Scope:** United States only (country-level aggregation)
- **Data Quality:** Generally high quality with ~11% null values in year-over-year (yy) and month-over-month (mm) comparison metrics
- **Table Purpose:** Time-series analysis of US real estate inventory metrics tracking listing prices, counts, market activity, and trends
- **Notable Pattern:** The `month_date_yyyymm` column is 100% null, suggesting this may be a dimensional attribute stored elsewhere or an unused field
- **Table Comment:** Not provided

## Column Details

### Geographic Identifier
- **country** (STRING): Single value "United States" across all records, serving as the geographic anchor for country-level aggregation

### Primary Date Field
- **month_date_yyyymm** (STRING): 100% null - appears to be a non-functional field; actual date tracking likely managed externally

### Core Listing Metrics

#### Listing Counts
- **total_listing_count** (INT64): Total active listings ranging from 815K to 1.87M, no nulls
- **active_listing_count** (INT64): Currently active listings (346K - 1.46M), no nulls
- **pending_listing_count** (INT64): Listings under contract (257K - 659K), no nulls
- **new_listing_count** (INT64): New market entries (215K - 584K), no nulls

#### Price Metrics
- **median_listing_price** (FLOAT64): $249,900 - $449,000 range, 94 unique values, no nulls
- **average_listing_price** (FLOAT64): $439,191 - $791,655 range, higher than median indicating right-skewed distribution, no nulls
- **median_listing_price_per_square_foot** (FLOAT64): $125 - $234, only 55 unique values suggesting some standardization

#### Property Characteristics
- **median_square_feet** (FLOAT64): 1,776 - 1,997 sq ft, relatively narrow range (86 unique values)
- **median_days_on_market** (INT64): 30 - 88 days, only 45 unique values indicating common durations

#### Price Action Metrics
- **price_reduced_count** (FLOAT64): 64,958 - 458,240 reductions per period
- **price_reduced_share** (FLOAT64): 5.37% - 21.68% of listings experience price cuts
- **price_increased_count** (INT64): 12,220 - 61,028 increases per period (109 unique values)
- **price_increased_share** (FLOAT64): 0.86% - 3.47% of listings see price increases

#### Market Activity Ratios
- **pending_ratio** (FLOAT64): 0.2322 - 1.4765, representing pending/active listing ratio; values >1 indicate high market velocity

### Trend Indicators (Change Metrics)

All trend columns show ~10.81% null values, likely representing the first period(s) where no prior comparison exists.

#### Month-over-Month Changes (_mm suffix)
- Range approximately -40% to +75% across various metrics
- Examples:
  - **total_listing_count_mm**: -14.06% to +11.61%
  - **median_listing_price_mm**: -3.39% to +5.02%
  - **new_listing_count_mm**: -27.61% to +42.03%
  - **median_days_on_market_mm**: -31.36% to +20.59%

#### Year-over-Year Changes (_yy suffix)
- Generally show wider ranges than monthly changes, reflecting longer-term trends
- Examples:
  - **total_listing_count_yy**: -27.12% to +22.68%
  - **median_listing_price_yy**: -2.2% to +18.19%
  - **active_listing_count_yy**: -53.74% to +67.17%
  - **pending_listing_count_yy**: -36.9% to +58.77%
  - **price_reduced_count_yy**: -61.74% to +174.13% (extreme volatility)

### Data Quality Indicator
- **quality_flag** (FLOAT64): Only value is 0.0 where not null; appears to be a binary flag where 0 = good quality

## Table and Column Documentation

**Table Comment:** Not provided in the analysis report.

**Column Comments:** No individual column comments were provided in the source data.

## Potential Query Considerations

### Ideal Filtering Columns
- **country**: Always "United States" (limited utility for filtering but required for clarity)
- **median_days_on_market**: Good for market temperature analysis (45 discrete values)
- **quality_flag**: Filter for quality = 0.0 when not null
- Date-based filtering would require external date dimension (month_date_yyyymm is null)

### Good Aggregation/Grouping Candidates
- Time-series grouping (requires external date field)
- Price bands (using median_listing_price ranges)
- Market velocity tiers (using pending_ratio or median_days_on_market)
- Property size categories (median_square_feet ranges)

### Potential Join Keys
- **country**: Could join to country-level demographic or economic data
- Implicit time dimension: Would need external date table to enable temporal joins
- Could relate to regional (state/metro) versions of this table for drill-down analysis

### Data Quality Considerations

1. **Missing Comparison Data**: ~11% nulls in all _mm and _yy fields suggests these are earliest periods; queries comparing trends should handle nulls appropriately

2. **Month Date Field**: 100% null month_date_yyyymm requires alternative approach to time-based queries (likely row number or external date mapping)

3. **Price Volatility**: Some metrics show extreme ranges (e.g., price_reduced_count_yy from -61.74% to +174.13%), requiring outlier handling in statistical analyses

4. **Value Distributions**: 
   - Median < Average prices indicate luxury property skew
   - Limited unique values in some fields (45 for days_on_market, 55 for price/sqft) suggest bucketing or rounding

5. **Ratio Calculations**: pending_ratio can exceed 1.0, indicating more pending than active listings in high-velocity markets

6. **Share Metrics**: All "share" columns are decimals (e.g., 0.1592 = 15.92%), not percentages

## Keywords

real estate, housing market, inventory metrics, listing prices, median price, average price, days on market, pending ratio, active listings, new listings, price reductions, price increases, square footage, market trends, month-over-month, year-over-year, United States, national housing data, property metrics, market velocity, housing inventory, real estate analytics, time series, market indicators, price per square foot, listing counts, market activity