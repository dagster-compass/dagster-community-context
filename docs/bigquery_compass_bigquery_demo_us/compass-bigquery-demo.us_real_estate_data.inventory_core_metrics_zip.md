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
# Table Documentation: inventory_core_metrics_zip

## Overview

This table contains detailed real estate inventory metrics at the ZIP code level, tracking listing prices, inventory counts, market activity, and various period-over-period comparisons. The dataset includes **3,142,815 rows** representing time-series data across approximately 34,141 unique ZIP codes in the United States.

### General Data Quality
- Most core metrics (listing counts, prices) have low null rates (0-1%)
- Year-over-year (yy) and month-over-month (mm) comparison fields have higher null rates (13-90%), likely due to insufficient historical data for newer records
- The `month_date_yyyymm` field is 100% null, indicating a data quality issue or deprecated field
- `quality_flag` field present (11% null) with binary values (0.0, 1.0) suggesting data quality markers

---

## Column Details

### Geographic Identifiers

**postal_code** (INT64)
- Primary geographic key
- 0% null - complete coverage
- Range: 501 to 99929 (US ZIP codes)
- 34,141 unique values
- Used for: Geographic filtering, joins, aggregations

**zip_name** (STRING)
- Human-readable location names in format "city, state"
- 2.30% null
- 26,083 unique values (less than postal codes, indicating many-to-one relationships)
- Examples: "morgantown, in", "new rochelle, ny", "chicago, il"

### Listing Count Metrics

**total_listing_count** (FLOAT64)
- Total active listings
- 0.10% null - highly reliable
- Range: 0 to 2,860 listings
- Common in filtering and aggregation queries

**active_listing_count** (FLOAT64)
- Currently active listings (subset of total)
- 0.15% null
- Range: 0 to 2,646
- Key metric for market supply analysis

**pending_listing_count** (FLOAT64)
- Listings under contract
- 20.69% null - use with caution
- Range: 0 to 976
- Higher null rate suggests not all markets report pending status

**new_listing_count** (FLOAT64)
- New listings in period
- 0.10% null
- Range: 0 to 802
- Important for market velocity analysis

### Price Metrics

**median_listing_price** (FLOAT64)
- Core price metric
- 0.25% null - highly reliable
- Range: $1 to $279,000,000
- Extreme upper values likely luxury/commercial properties
- Use for price trend analysis

**average_listing_price** (FLOAT64)
- Mean listing price
- 0.25% null
- Range: $1 to $279,000,000
- More sensitive to outliers than median

**median_listing_price_per_square_foot** (FLOAT64)
- Price efficiency metric
- 0.96% null
- Range: $0 to $795,000/sqft
- Upper extremes likely data errors or special properties

### Property Size Metrics

**median_square_feet** (FLOAT64)
- Median property size
- 0.95% null
- Range: 1 to 12,503,400 sqft
- Upper extremes suggest data quality issues or commercial properties

### Market Activity Metrics

**pending_ratio** (FLOAT64)
- Ratio of pending to total listings
- 21.63% null
- Range: 0.0 to 94.5
- Values appear to be percentages (0-100 scale)
- Indicates market demand strength

**median_days_on_market** (FLOAT64)
- Time to sale/pending status
- 0.93% null - reliable
- Range: 1 to 365 days
- Key velocity indicator

**price_reduced_count** (FLOAT64)
- Number of listings with price reductions
- 0.10% null
- Range: 0 to 628
- Market distress indicator

**price_reduced_share** (FLOAT64)
- Percentage of listings with price reductions
- 0.46% null
- Range: 0.0 to 4.0
- Values suggest percentage scale

**price_increased_count** (FLOAT64)
- Number of listings with price increases
- 0.10% null
- Range: 0 to 268
- Less common than reductions

**price_increased_share** (FLOAT64)
- Percentage of listings with price increases
- 0.46% null
- Range: 0.0 to 4.0

### Period-over-Period Comparisons

All metrics with **_mm** suffix represent month-over-month changes:
- Generally 13-45% null rates
- Values appear to be fractional changes (-1.0 = -100%, 1.0 = +100%)
- Example: `total_listing_count_mm` shows monthly inventory change

All metrics with **_yy** suffix represent year-over-year changes:
- Generally 15-90% null rates (higher for less common metrics)
- Same fractional change format
- Example: `median_listing_price_yy` shows annual price appreciation

**Notable null patterns in comparison metrics:**
- `price_increased_count_mm`: 90.42% null
- `price_increased_count_yy`: 89.71% null
- `price_reduced_count_mm`: 54.76% null
- `new_listing_count_yy/mm`: ~45% null
- Suggests these metrics require minimum activity thresholds

### Data Quality Indicator

**quality_flag** (FLOAT64)
- 11.09% null
- Binary values: 0.0 or 1.0
- Likely indicates data reliability (1.0 = good quality)
- Consider filtering on this field for critical analyses

### Deprecated Field

**month_date_yyyymm** (STRING)
- 100% null - completely unpopulated
- Avoid using in queries

---

## Query Considerations

### Recommended Filters
- **postal_code**: Primary key for geographic filtering (0% null)
- **zip_name**: User-friendly geographic filter (2.3% null)
- **quality_flag**: Filter to quality_flag = 1.0 for reliable data
- **Date ranges**: Must be inferred from time-series context (month_date_yyyymm unusable)

### Good Aggregation Columns
- **postal_code/zip_name**: Geographic grouping
- Price metrics (median/average_listing_price) for market summaries
- Count metrics (total/active/pending) for inventory analysis
- **median_days_on_market**: Market velocity

### Potential Join Keys
- **postal_code**: Primary join key to other geographic datasets
- **zip_name**: Secondary join (but has more nulls)

### Data Quality Considerations
1. **High null rates** in comparison metrics (_mm, _yy) - require null handling
2. **Quality_flag** should be checked for critical analyses
3. **Extreme values** in price and square footage may need outlier filtering
4. **month_date_yyyymm** is unusable - temporal context must come from external source
5. Period-over-period metrics use **fractional representation** (not percentages)
6. Some metrics like **price_increased_count** have very high null rates (>89%)

### Temporal Analysis
- This appears to be time-series data, but temporal key is missing
- Queries will need to join with external date dimension
- Comparison metrics (_mm, _yy) provide built-in trend analysis
- Higher null rates in historical comparisons for recent data

---

## Keywords

real estate, housing, inventory, listings, prices, zip code, postal code, market metrics, median price, average price, days on market, pending ratio, active listings, price per square foot, month over month, year over year, housing supply, market velocity, price reductions, new listings, geographic analysis, US real estate, property metrics, market trends, time series

---

## Table and Column Documentation

**Table Comment:** Not provided

**Column Comments:**
- No column-level comments were found in the schema. All column descriptions are inferred from data analysis.