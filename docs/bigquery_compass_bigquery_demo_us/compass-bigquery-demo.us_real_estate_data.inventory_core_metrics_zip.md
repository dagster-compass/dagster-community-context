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
# Comprehensive Data Summary: US Real Estate Inventory Core Metrics by ZIP Code

## Overall Dataset Characteristics

**Total Rows:** 3,142,815

This table contains comprehensive real estate inventory metrics aggregated at the ZIP code level. The dataset tracks various listing statistics, pricing information, and market dynamics with temporal comparisons (month-over-month and year-over-year changes).

**Data Quality Observations:**
- Generally high data quality with most core metrics having low null percentages
- The `month_date_yyyymm` column is 100% null, suggesting it may be deprecated or unused
- Price increase metrics have very high null percentages (89-90%), indicating these may be newer or less consistently tracked metrics
- New listing and pending listing metrics show moderate null percentages (20-45%), suggesting seasonal or market condition dependencies
- Quality_flag column (11% null) appears to be a data quality indicator with binary values (0.0 or 1.0)

**Notable Patterns:**
- Year-over-year (yy) and month-over-month (mm) comparison columns typically show percentage changes, often ranging from -1.0 (representing -100% or complete decline) to positive values
- Many "_yy" and "_mm" columns contain values near -1.0, suggesting complete absences of data in comparison periods
- Geographic coverage spans all US ZIP codes (range: 501 to 99929)

## Column Details

### Geographic Identifiers

**postal_code (INT64)**
- **Format:** 5-digit ZIP codes
- **Null Percentage:** 0.00% (complete)
- **Range:** 501 to 99929
- **Purpose:** Primary geographic identifier
- **Use Case:** Essential for geographic filtering, joining with other ZIP-level data

**zip_name (STRING)**
- **Format:** "city, state" (lowercase)
- **Null Percentage:** 2.30%
- **Examples:** "milton, nh", "ben lomond, ca", "jefferson, oh"
- **Purpose:** Human-readable location identifier
- **Use Case:** User-friendly location display, text searches

### Core Listing Counts

**total_listing_count (FLOAT64)**
- **Null Percentage:** 0.10%
- **Range:** 0.0 to 2,860.0
- **Common Values:** Small integers (0-10), concentrated at lower values
- **Comment:** Total active listings in the ZIP code
- **Use Case:** Primary volume metric, good for market size analysis

**active_listing_count (FLOAT64)**
- **Null Percentage:** 0.15%
- **Range:** 0.0 to 2,646.0
- **Pattern:** Similar to total_listing_count
- **Use Case:** Current inventory levels, supply metrics

**new_listing_count (FLOAT64)**
- **Null Percentage:** 0.10%
- **Range:** 0.0 to 802.0
- **Pattern:** Generally lower than total counts, even values common (0, 2, 4, 6...)
- **Use Case:** Market activity indicator, new supply tracking

**pending_listing_count (FLOAT64)**
- **Null Percentage:** 20.69%
- **Range:** 0.0 to 976.0
- **Pattern:** Higher null percentage suggests not all markets track pending status
- **Use Case:** Demand indicator, market velocity analysis

### Pricing Metrics

**median_listing_price (FLOAT64)**
- **Null Percentage:** 0.25%
- **Range:** $1 to $279,000,000
- **Unique Values:** 238,139 (highly granular)
- **Pattern:** Wide range suggests diverse markets from rural to ultra-luxury
- **Use Case:** Primary price metric for affordability analysis

**average_listing_price (FLOAT64)**
- **Null Percentage:** 0.25%
- **Range:** $1 to $279,000,000
- **Unique Values:** 894,375 (very granular)
- **Pattern:** Typically higher than median due to outlier impact
- **Use Case:** Market valuation, comparison with median for skew analysis

**median_listing_price_per_square_foot (FLOAT64)**
- **Null Percentage:** 0.96%
- **Range:** $0 to $795,000 per sq ft
- **Pattern:** Most values in reasonable range ($0-$500/sq ft)
- **Use Case:** Normalized price comparison across property sizes

### Property Characteristics

**median_square_feet (FLOAT64)**
- **Null Percentage:** 0.95%
- **Range:** 1 to 12,503,400 sq ft
- **Pattern:** Extreme upper range suggests data quality issues or commercial properties
- **Use Case:** Property size analysis, correlation with pricing

### Time-on-Market Metrics

**median_days_on_market (FLOAT64)**
- **Null Percentage:** 0.93%
- **Range:** 1 to 365 days
- **Pattern:** Full year range suggests some listings remain active for extended periods
- **Use Case:** Market velocity indicator, seller competition metric

### Price Change Indicators

**price_reduced_count (FLOAT64)**
- **Null Percentage:** 0.10%
- **Range:** 0 to 628
- **Pattern:** Even values common, concentrated at lower numbers
- **Use Case:** Market weakness indicator

**price_reduced_share (FLOAT64)**
- **Null Percentage:** 0.46%
- **Range:** 0.0 to 4.0
- **Pattern:** Decimal values representing proportions
- **Use Case:** Percentage of listings with price reductions

**price_increased_count (FLOAT64)**
- **Null Percentage:** 0.10%
- **Range:** 0 to 268
- **Pattern:** Generally lower than reduction counts
- **Use Case:** Market strength indicator

**price_increased_share (FLOAT64)**
- **Null Percentage:** 0.46%
- **Range:** 0.0 to 4.0
- **Pattern:** Generally lower values than reduction shares
- **Use Case:** Percentage of listings with price increases

### Market Activity Ratios

**pending_ratio (FLOAT64)**
- **Null Percentage:** 21.63%
- **Range:** 0.0 to 94.5
- **Pattern:** Percentage-like values, high nulls suggest calculation limitations
- **Use Case:** Demand-to-supply ratio, market heat indicator

### Temporal Comparison Metrics (_mm suffix = Month-over-Month)

All "_mm" columns represent month-over-month percentage changes:

**Pattern:** Values typically range from -1.0 (100% decline) to positive values
**Null Percentages:** Range from 12-90% depending on metric
**Interpretation:** -1.0 = complete absence in prior month, 0.0 = no change, positive = growth

Key _mm metrics:
- `total_listing_count_mm`: 12.72% null
- `active_listing_count_mm`: 13.94% null
- `new_listing_count_mm`: 44.80% null (higher volatility)
- `pending_listing_count_mm`: 32.61% null
- `median_listing_price_mm`: 13.53% null
- `average_listing_price_mm`: 13.53% null
- `median_square_feet_mm`: 14.16% null
- `median_days_on_market_mm`: 14.22% null
- `pending_ratio_mm`: 33.49% null
- Price change metrics: 13-90% null

### Temporal Comparison Metrics (_yy suffix = Year-over-Year)

All "_yy" columns represent year-over-year percentage changes:

**Pattern:** Similar to _mm metrics but comparing to same period prior year
**Null Percentages:** Generally 15-90%
**Use Case:** Longer-term trend analysis, seasonal adjustment

Key _yy metrics:
- `total_listing_count_yy`: 15.86% null
- `active_listing_count_yy`: 17.31% null
- `new_listing_count_yy`: 45.00% null
- `pending_listing_count_yy`: 37.49% null
- `median_listing_price_yy`: 16.67% null
- `average_listing_price_yy`: 16.67% null
- `median_square_feet_yy`: 17.36% null
- `median_days_on_market_yy`: 17.58% null
- `pending_ratio_yy`: 37.99% null
- Price change metrics: 16-90% null

### Data Quality Indicator

**quality_flag (FLOAT64)**
- **Null Percentage:** 11.09%
- **Unique Values:** 2 (0.0 and 1.0)
- **Purpose:** Binary quality indicator
- **Use Case:** Filter for high-quality data records (where quality_flag = 1.0)

### Deprecated/Unused Column

**month_date_yyyymm (STRING)**
- **Null Percentage:** 100.00%
- **Status:** Completely empty, likely deprecated
- **Recommendation:** Do not use in queries

## Query Considerations

### Best Columns for Filtering

1. **Geographic filters:**
   - `postal_code` (complete data, precise)
   - `zip_name` (for text searches, 2.3% null)

2. **Data quality filter:**
   - `quality_flag = 1.0` (recommended for accurate analysis)

3. **Market activity filters:**
   - `total_listing_count > 0` (exclude empty markets)
   - `median_listing_price IS NOT NULL` (price data available)

4. **Price range filters:**
   - `median_listing_price` (for affordability analysis)
   - `median_listing_price_per_square_foot` (for normalized comparisons)

### Best Columns for Grouping/Aggregation

1. **Geographic aggregations:**
   - `postal_code` (for ZIP-level analysis)
   - Can extract state from `zip_name` for state-level rollups

2. **Market size buckets:**
   - Create buckets from `total_listing_count` (small/medium/large markets)

3. **Price tier analysis:**
   - Create buckets from `median_listing_price` (affordable/mid/luxury)

4. **Time analysis:**
   - Note: No explicit date column available; data appears to be point-in-time snapshots

### Aggregation Recommendations

- **SUM:** `total_listing_count`, `active_listing_count`, `new_listing_count`, `pending_listing_count`, price change counts
- **AVG/MEDIAN:** All price metrics, `median_square_feet`, `median_days_on_market`, ratio metrics
- **WEIGHTED AVG:** Consider weighting by `total_listing_count` for price aggregations

### Join Key

- **Primary Key:** `postal_code` (can join with other ZIP-level demographic, economic, or geographic data)

### Data Quality Considerations for Queries

1. **Always consider filtering on `quality_flag = 1.0`** for production queries

2. **Handle high null percentages in:**
   - New listing metrics (44-45% null)
   - Pending metrics (20-38% null)
   - Price increase metrics (89-90% null) - may want to exclude or use COALESCE

3. **Temporal comparisons (_mm, _yy):**
   - Values of -1.0 indicate no data in comparison period (100% decline)
   - Consider whether to exclude these or treat as genuine declines
   - Use `IS NOT NULL` filters when analyzing trends

4. **Extreme values:**
   - `median_square_feet` has suspicious max (12.5M sq ft) - consider capping
   - `median_listing_price` reaches $279M - verify if outliers should be excluded

5. **Month-over-month vs Year-over-year:**
   - MM metrics have lower null rates (more recent data)
   - YY metrics better for seasonal adjustment
   - Both can be used together for trend validation

## Keywords

real estate, housing market, inventory metrics, ZIP code, postal code, listing prices, median price, average price, price per square foot, days on market, market velocity, new listings, active listings, pending listings, price reductions, price increases, month over month, year over year, market trends, housing supply, housing demand, property metrics, square footage, market activity, real estate analytics, geographic data, time series, market indicators, pending ratio, quality flag, US real estate, housing statistics

## Table and Column Documentation

**Table Comment:** Not provided

**Column Comments:** None of the columns have explicit comments in the schema. The column naming convention is self-documenting with suffixes:
- `_mm`: Month-over-month percentage change
- `_yy`: Year-over-year percentage change  
- `_count`: Absolute counts
- `_share`: Proportions/percentages
- `_ratio`: Calculated ratios

No formal column comments are present in the schema provided.