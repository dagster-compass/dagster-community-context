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
# Table Documentation Summary: US Real Estate Inventory Metrics (Country Level)

## Overall Dataset Characteristics

**Total Rows:** 111

**General Data Quality:**
- This is a country-level aggregated dataset focused on United States real estate inventory metrics
- Approximately 10.81% of values are null across most metric columns, suggesting these rows represent base periods or initial data points without year-over-year (yy) or month-over-month (mm) comparisons
- One column (`month_date_yyyymm`) is completely null (100%), indicating missing temporal identifiers
- Core count metrics have no null values, providing reliable baseline measurements
- `country` field contains only "United States" as a value

**Notable Patterns:**
- Data includes both absolute values (counts, prices) and relative changes (yy, mm comparisons)
- Consistent null patterns across comparative metrics (_yy, _mm suffixes) suggest time-series data where early periods lack comparison baselines
- Metrics span multiple dimensions: pricing, inventory counts, days on market, square footage, and price adjustments

**Table Comment:** Not provided

## Column Details

### Temporal Identifier
- **month_date_yyyymm** (STRING): 100% null - intended temporal identifier but completely unpopulated

### Geographic Identifier
- **country** (STRING): Single value "United States" - geographic dimension for aggregation

### Core Count Metrics (No Nulls)
- **total_listing_count** (INT64): Total property listings (815K-1.87M range)
- **active_listing_count** (INT64): Currently active listings (347K-1.46M range)
- **pending_listing_count** (INT64): Listings under contract (258K-660K range)
- **new_listing_count** (INT64): New listings added (216K-584K range)

### Pricing Metrics (No Nulls)
- **average_listing_price** (FLOAT64): Mean listing price ($439K-$792K)
- **median_listing_price** (FLOAT64): Median listing price ($250K-$449K)
- **median_listing_price_per_square_foot** (FLOAT64): Price per sq ft ($125-$234)

### Property Characteristics (No Nulls)
- **median_square_feet** (FLOAT64): Median property size (1,776-1,997 sq ft)
- **median_days_on_market** (INT64): Time until sale/contract (30-88 days)

### Price Adjustment Metrics (No Nulls)
- **price_reduced_count** (FLOAT64): Count of price reductions (65K-458K)
- **price_reduced_share** (FLOAT64): Proportion with price reductions (5.4%-21.7%)
- **price_increased_count** (INT64): Count of price increases (12K-61K)
- **price_increased_share** (FLOAT64): Proportion with price increases (0.9%-3.5%)

### Ratio Metrics (No Nulls)
- **pending_ratio** (FLOAT64): Pending to active listing ratio (0.23-1.48)

### Month-over-Month Change Metrics (10.81% Null)
All _mm suffixed columns represent monthly percentage changes:
- **total_listing_count_mm**: -14.1% to +11.6%
- **active_listing_count_mm**: -15.4% to +26.2%
- **pending_listing_count_mm**: -14.6% to +27.2%
- **new_listing_count_mm**: -27.6% to +42.0%
- **average_listing_price_mm**: -3.7% to +5.7%
- **median_listing_price_mm**: -3.4% to +5.0%
- **median_listing_price_per_square_foot_mm**: -1.6% to +3.9%
- **median_square_feet_mm**: -1.8% to +2.2%
- **median_days_on_market_mm**: -31.4% to +20.6%
- **pending_ratio_mm**: -29.2% to +27.1%
- **price_reduced_count_mm**: -40.8% to +74.6%
- **price_reduced_share_mm**: -6.1% to +4.6%
- **price_increased_count_mm**: -27.8% to +42.3%
- **price_increased_share_mm**: -0.8% to +1.2%

### Year-over-Year Change Metrics (10.81% Null)
All _yy suffixed columns represent annual percentage changes:
- **total_listing_count_yy**: -27.1% to +22.7%
- **active_listing_count_yy**: -53.7% to +67.2%
- **pending_listing_count_yy**: -36.9% to +58.8%
- **new_listing_count_yy**: -36.8% to +41.0%
- **average_listing_price_yy**: -4.1% to +33.4%
- **median_listing_price_yy**: -2.2% to +18.2%
- **median_listing_price_per_square_foot_yy**: -0.9% to +23.6%
- **median_square_feet_yy**: -7.3% to +4.1%
- **median_days_on_market_yy**: -48.5% to +59.3%
- **pending_ratio_yy**: -77.9% to +99.3%
- **price_reduced_count_yy**: -61.7% to +174.1%
- **price_reduced_share_yy**: -6.8% to +10.8%
- **price_increased_count_yy**: -59.2% to +120.9%
- **price_increased_share_yy**: -1.8% to +1.8%

### Quality Flag
- **quality_flag** (FLOAT64): 10.81% null, single value of 0.0 when present - likely indicates data quality issues or special conditions

## Potential Query Considerations

### Good for Filtering:
- **country**: Single value, useful for multi-geography datasets
- **quality_flag**: Filter out problematic records (when = 0.0)
- **median_days_on_market**: Fast vs. slow markets (< 45 days = hot market)
- Date ranges (when month_date_yyyymm is populated)

### Good for Grouping/Aggregation:
- Time-based grouping (monthly, quarterly) once temporal field is populated
- Market condition segments (hot/moderate/slow based on days_on_market)
- Price tier analysis using median_listing_price ranges
- Geographic expansion when combined with other geographic dimensions

### Potential Join Keys:
- **country**: For joining with other country-level demographic/economic data
- **month_date_yyyymm**: Time-series joins (currently unpopulated)
- Could join with regional/state level data using temporal keys

### Data Quality Considerations:
1. **Missing Temporal Key**: month_date_yyyymm is 100% null - queries needing time filtering will be challenging
2. **Consistent Null Pattern**: 10.81% nulls in comparative metrics (_yy, _mm) indicate ~12 rows are baseline periods
3. **Price Reduced Count**: Stored as FLOAT64 but represents counts - may need rounding
4. **Quality Flag**: All non-null values are 0.0 - understand meaning before filtering
5. **Change Metrics**: Some show extreme ranges (e.g., price_reduced_count_yy: -61.7% to +174.1%) - verify outliers before aggregating
6. **Pending Ratio**: Values > 1.0 indicate more pending than active listings - important market signal

### Analytical Use Cases:
- Market trend analysis (using _yy and _mm metrics)
- Pricing strategy insights (price adjustment patterns)
- Inventory health monitoring (active vs. pending ratios)
- Market velocity tracking (days on market trends)
- Supply/demand indicators (listing count trends)

## Keywords

real estate, housing market, inventory metrics, listing prices, market trends, days on market, price reductions, price increases, pending sales, active listings, new listings, square footage, price per square foot, month over month, year over year, market velocity, housing supply, pending ratio, country level data, United States real estate, property metrics, housing inventory, market analysis, time series, comparative metrics

## Table and Column Documentation

**Table Comment:** Not provided

**Column Comments:** None provided for any columns