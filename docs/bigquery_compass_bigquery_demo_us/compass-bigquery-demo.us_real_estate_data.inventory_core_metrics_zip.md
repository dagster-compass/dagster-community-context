---
columns:
- active_listing_count (FLOAT64)
- active_listing_count_mm (FLOAT64)
- active_listing_count_yy (FLOAT64)
- average_listing_price (FLOAT64)
- average_listing_price_mm (FLOAT64)
- average_listing_price_yy (FLOAT64)
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
- postal_code (INT64)
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
- zip_name (STRING)
schema_hash: 298de63c9f54c4d2298f4427674befa32a437912cf25f7841e703aa50148138b

---
# Comprehensive Summary: US Real Estate Inventory Core Metrics (ZIP Code Level)

## Overall Dataset Characteristics

### Scale and Scope
- **Total Rows:** 3,142,815 records
- **Geographic Granularity:** ZIP code level (34,141 unique postal codes, 26,083 unique ZIP names)
- **Data Type:** Time-series real estate market metrics with month-over-month (mm) and year-over-year (yy) comparisons

### Data Quality Observations
- **Critical Issue:** `month_date_yyyymm` column is 100% null, indicating missing temporal reference data
- **Quality Flag:** 11.09% null rate suggests data quality tracking mechanism
- **High Null Columns:** Several derived metrics have 30-90% null rates, particularly price increase/reduction counts
- **Core Metrics:** Listing counts and prices have low null rates (0.10-0.25%), indicating reliable primary data

### Notable Patterns
- Heavy presence of relative change metrics (mm = month-over-month, yy = year-over-year)
- Ratio values often contain negative values close to -1.0 (likely representing -100% or complete decreases)
- Price and square footage metrics span enormous ranges, suggesting inclusion of extreme outliers or data quality issues
- Multiple count metrics appear to be integer-valued floats

### Table Comment
Not provided in source data.

---

## Column Details

### Temporal Identification
**month_date_yyyymm** (STRING)
- **Status:** 100% null - CRITICAL DATA ISSUE
- **Intended Purpose:** Likely YYYYMM format date identifier for time-series queries
- **Impact:** Cannot identify specific time periods without external reference
- **Column Comment:** Not provided

### Geographic Identifiers

**postal_code** (INT64)
- **Range:** 501 to 99,929 (US ZIP codes)
- **Null Rate:** 0.00% (fully populated)
- **Unique Values:** 34,141 ZIP codes
- **Query Use:** Primary geographic filter and grouping key
- **Column Comment:** Not provided

**zip_name** (STRING)
- **Format:** "city, state" (e.g., "molalla, or", "acworth, ga")
- **Null Rate:** 2.30%
- **Unique Values:** 26,083
- **Query Use:** Human-readable geographic reference
- **Column Comment:** Not provided

### Core Inventory Metrics

**total_listing_count** (FLOAT64)
- **Range:** 0.0 to 2,860.0
- **Null Rate:** 0.10% (highly reliable)
- **Distribution:** 1,490 unique values suggesting wide variation by market
- **Query Use:** Primary metric for market size, excellent for filtering and aggregation
- **Column Comment:** Not provided

**active_listing_count** (FLOAT64)
- **Range:** 0.0 to 2,646.0
- **Null Rate:** 0.15%
- **Unique Values:** 1,302
- **Relationship:** Subset of total listings (active = total - pending)
- **Query Use:** Current available inventory metric
- **Column Comment:** Not provided

**pending_listing_count** (FLOAT64)
- **Range:** 0.0 to 976.0
- **Null Rate:** 20.69% (moderate reliability)
- **Unique Values:** 555
- **Query Use:** Under-contract properties indicator
- **Column Comment:** Not provided

**new_listing_count** (FLOAT64)
- **Range:** 0.0 to 802.0
- **Null Rate:** 0.10%
- **Unique Values:** 190
- **Query Use:** Market activity/supply indicator
- **Column Comment:** Not provided

### Price Metrics

**median_listing_price** (FLOAT64)
- **Range:** $1 to $279,000,000
- **Null Rate:** 0.25%
- **Unique Values:** 238,139 (high granularity)
- **Data Quality:** Extreme max suggests outliers or data errors
- **Query Use:** Primary price metric for market analysis
- **Column Comment:** Not provided

**average_listing_price** (FLOAT64)
- **Range:** $1 to $279,000,000
- **Null Rate:** 0.25%
- **Unique Values:** 894,375
- **Comparison:** Higher unique value count than median suggests more variation
- **Query Use:** Alternative central tendency measure
- **Column Comment:** Not provided

**median_listing_price_per_square_foot** (FLOAT64)
- **Range:** $0 to $795,000
- **Null Rate:** 0.96%
- **Unique Values:** 3,167
- **Data Quality:** Max value suggests data error (likely should be per sqft)
- **Query Use:** Normalized price comparison across markets
- **Column Comment:** Not provided

### Property Characteristics

**median_square_feet** (FLOAT64)
- **Range:** 1.0 to 12,503,400.0
- **Null Rate:** 0.95%
- **Unique Values:** 8,467
- **Data Quality:** Max value is clearly an error (12.5M sqft)
- **Query Use:** Property size indicator
- **Column Comment:** Not provided

### Market Velocity Metrics

**median_days_on_market** (FLOAT64)
- **Range:** 1.0 to 365.0
- **Null Rate:** 0.93%
- **Unique Values:** 365
- **Pattern:** Appears capped at 365 days
- **Query Use:** Market speed/liquidity indicator
- **Column Comment:** Not provided

**pending_ratio** (FLOAT64)
- **Range:** 0.0 to 94.5
- **Null Rate:** 21.63%
- **Interpretation:** Likely pending/total ratio as percentage
- **Query Use:** Market heat indicator (higher = more competitive)
- **Column Comment:** Not provided

### Seller Behavior Metrics

**price_reduced_count** (FLOAT64)
- **Range:** 0.0 to 628.0
- **Null Rate:** 0.10%
- **Unique Values:** 244
- **Query Use:** Market weakness indicator
- **Column Comment:** Not provided

**price_reduced_share** (FLOAT64)
- **Range:** 0.0 to 4.0
- **Null Rate:** 0.46%
- **Unique Values:** 5,907
- **Interpretation:** Ratio of price reductions to total listings
- **Query Use:** Market sentiment metric
- **Column Comment:** Not provided

**price_increased_count** (FLOAT64)
- **Range:** 0.0 to 268.0
- **Null Rate:** 0.10%
- **Unique Values:** 100
- **Query Use:** Market strength indicator
- **Column Comment:** Not provided

**price_increased_share** (FLOAT64)
- **Range:** 0.0 to 4.0
- **Null Rate:** 0.46%
- **Unique Values:** 3,721
- **Query Use:** Seller confidence metric
- **Column Comment:** Not provided

### Month-over-Month Change Metrics (mm suffix)

All mm-suffixed columns show relative changes from previous month:

**active_listing_count_mm** (FLOAT64)
- **Range:** -1.0 to 68.0
- **Null Rate:** 13.94%
- **Interpretation:** -1.0 = 100% decrease, positive values = growth rate
- **Column Comment:** Not provided

**total_listing_count_mm** (FLOAT64)
- **Null Rate:** 12.72%
- **Column Comment:** Not provided

**pending_listing_count_mm** (FLOAT64)
- **Null Rate:** 32.61%
- **Column Comment:** Not provided

**new_listing_count_mm** (FLOAT64)
- **Null Rate:** 44.80%
- **Column Comment:** Not provided

**median_listing_price_mm** (FLOAT64)
- **Null Rate:** 13.53%
- **Column Comment:** Not provided

**average_listing_price_mm** (FLOAT64)
- **Null Rate:** 13.53%
- **Column Comment:** Not provided

**median_listing_price_per_square_foot_mm** (FLOAT64)
- **Null Rate:** 14.17%
- **Column Comment:** Not provided

**median_square_feet_mm** (FLOAT64)
- **Null Rate:** 14.16%
- **Column Comment:** Not provided

**median_days_on_market_mm** (FLOAT64)
- **Null Rate:** 14.22%
- **Column Comment:** Not provided

**pending_ratio_mm** (FLOAT64)
- **Null Rate:** 33.49%
- **Column Comment:** Not provided

**price_reduced_count_mm** (FLOAT64)
- **Null Rate:** 54.76% (HIGH)
- **Column Comment:** Not provided

**price_reduced_share_mm** (FLOAT64)
- **Null Rate:** 13.02%
- **Column Comment:** Not provided

**price_increased_count_mm** (FLOAT64)
- **Null Rate:** 90.42% (VERY HIGH)
- **Column Comment:** Not provided

**price_increased_share_mm** (FLOAT64)
- **Null Rate:** 13.02%
- **Column Comment:** Not provided

### Year-over-Year Change Metrics (yy suffix)

All yy-suffixed columns show relative changes from same month previous year:

**active_listing_count_yy** (FLOAT64)
- **Null Rate:** 17.31%
- **Column Comment:** Not provided

**total_listing_count_yy** (FLOAT64)
- **Null Rate:** 15.86%
- **Column Comment:** Not provided

**pending_listing_count_yy** (FLOAT64)
- **Null Rate:** 37.49%
- **Column Comment:** Not provided

**new_listing_count_yy** (FLOAT64)
- **Null Rate:** 45.00%
- **Column Comment:** Not provided

**median_listing_price_yy** (FLOAT64)
- **Null Rate:** 16.67%
- **Column Comment:** Not provided

**average_listing_price_yy** (FLOAT64)
- **Null Rate:** 16.67%
- **Column Comment:** Not provided

**median_listing_price_per_square_foot_yy** (FLOAT64)
- **Null Rate:** 17.37%
- **Column Comment:** Not provided

**median_square_feet_yy** (FLOAT64)
- **Null Rate:** 17.36%
- **Column Comment:** Not provided

**median_days_on_market_yy** (FLOAT64)
- **Null Rate:** 17.58%
- **Column Comment:** Not provided

**pending_ratio_yy** (FLOAT64)
- **Null Rate:** 37.99%
- **Column Comment:** Not provided

**price_reduced_count_yy** (FLOAT64)
- **Null Rate:** 54.67% (HIGH)
- **Column Comment:** Not provided

**price_reduced_share_yy** (FLOAT64)
- **Null Rate:** 16.03%
- **Column Comment:** Not provided

**price_increased_count_yy** (FLOAT64)
- **Null Rate:** 89.71% (VERY HIGH)
- **Column Comment:** Not provided

**price_increased_share_yy** (FLOAT64)
- **Null Rate:** 16.03%
- **Column Comment:** Not provided

### Data Quality Indicator

**quality_flag** (FLOAT64)
- **Values:** 0.0 or 1.0 (binary indicator)
- **Null Rate:** 11.09%
- **Unique Values:** 2
- **Interpretation:** Likely 1.0 = quality data, 0.0 = questionable
- **Query Use:** Filter for reliable records
- **Column Comment:** Not provided

---

## Query Considerations

### Recommended Filters
1. **Geographic:** `postal_code` or `zip_name` for location-based queries
2. **Data Quality:** `quality_flag = 1.0` to exclude questionable records
3. **Non-null checks:** Essential for derived metrics with high null rates
4. **Temporal:** Currently impossible without `month_date_yyyymm` - requires external date mapping

### Good Grouping/Aggregation Columns
- **postal_code:** Primary geographic dimension
- **zip_name:** Human-readable geographic rollup
- State (extractable from zip_name)
- **quality_flag:** Data reliability segments

### Aggregation-Friendly Metrics
- All count columns (total_listing_count, active_listing_count, etc.)
- Price metrics (median_listing_price, average_listing_price)
- median_days_on_market
- All share/ratio metrics for weighted averages

### Potential Join Keys
- **postal_code:** Can join to external ZIP code dimension tables (census data, geographic boundaries, demographics)
- **zip_name:** Human-readable reference but less reliable for joins
- **Missing:** Time dimension requires external mapping

### Data Quality Considerations

**Critical for Queries:**
1. **Missing temporal dimension:** Cannot create time-series queries without external date reference
2. **Extreme outliers:** Price and square footage ranges include impossible values requiring bounds
3. **Negative change values near -1.0:** Represent 100% decreases, need careful handling in calculations
4. **High null rates in price change metrics:** May require COALESCE or null-handling logic
5. **Quality flag:** Should be default filter criterion for analytical queries

**Recommended Query Patterns:**
- Always filter on `quality_flag = 1.0` for production queries
- Use SAFE_DIVIDE for ratio calculations due to potential zeros
- Apply reasonable bounds to price and square footage (e.g., median_listing_price BETWEEN 10000 AND 50000000)
- Consider NULL handling for all _mm and _yy columns
- Group by postal_code for ZIP-level aggregation

**Value Interpretation:**
- Change metrics: -1.0 = 100% decrease, 0.5 = 50% increase
- Share metrics: Values > 1.0 likely represent counts rather than percentages
- Ratios: pending_ratio appears to be percentage (0-100 scale)

---

## Keywords

real estate, housing market, inventory metrics, ZIP code, postal code, listing data, home prices, median price, average price, price per square foot, days on market, active listings, pending listings, new listings, price reductions, price increases, month over month, year over year, market trends, housing supply, property metrics, real estate analytics, market velocity, seller behavior, geographic analysis, time series, quality flag, US housing data, residential real estate

---

## Table and Column Documentation

### Table Comment
Not provided in source data.

### Column Comments
No column comments were provided in the source table schema.