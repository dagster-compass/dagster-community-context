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
# Comprehensive Data Summary: US Real Estate County Inventory Metrics

## Overview

This dataset contains **344,538 rows** of real estate inventory metrics aggregated at the county level across the United States. The data appears to be a time-series dataset tracking various housing market indicators, though the date column (`month_date_yyyymm`) is entirely null, suggesting dates may need to be derived from context or this represents a snapshot view.

### Data Quality Observations
- **Generally high quality** with most core metrics having <1% null values
- **Significant missing data** in month-over-month (MM) comparisons (~10-19% nulls) and year-over-year (YY) comparisons (~11-20% nulls)
- **Sparse data** for price change metrics: `price_increased_count` fields have 73-74% nulls
- **Quality flag** present with 10.72% nulls, containing binary values (0.0, 1.0) likely indicating data reliability

## Column Details

### Geographic Identifiers

**county_fips** (INT64)
- Primary geographic identifier
- 3,141 unique counties represented
- Range: 1001 to 56045 (FIPS codes for US counties)
- No null values (0.00%)
- *Use for:* Primary key, joining with other geographic datasets

**county_name** (STRING)
- Human-readable county and state names (format: "county, state")
- 3,135 unique values (slightly fewer than FIPS codes, indicating some name duplication)
- No null values
- Examples: "gloucester, nj", "suffolk, ny", "keweenaw, mi"

### Temporal Field

**month_date_yyyymm** (STRING)
- **100% null** - completely empty field
- Intended format likely YYYYMM (e.g., "202301")
- *Note:* Date information may be stored elsewhere or this represents a single time period snapshot

### Price Metrics

**median_listing_price** (FLOAT64)
- Core price metric
- Range: $1,311 to $13,000,000
- 52,273 unique values
- Only 0.02% nulls
- *Use for:* Primary price analysis, filtering by price ranges

**median_listing_price_mm** (FLOAT64)
- Month-over-month price change ratio
- Range: -0.9971 to 570.3196 (percentage changes)
- 10.89% nulls (typical for comparative metrics)
- Negative values indicate price decreases

**median_listing_price_yy** (FLOAT64)
- Year-over-year price change ratio
- Range: -0.9968 to 222.8749
- 11.27% nulls
- *Use for:* Trend analysis, identifying hot/cold markets

**average_listing_price** (FLOAT64)
- Mean price (vs median)
- Range: $5,000 to $142,882,807
- 252,993 unique values (highly granular)
- Extreme high values suggest luxury properties or data anomalies

**median_listing_price_per_square_foot** (FLOAT64)
- Price efficiency metric
- Range: $0 to $56,250/sqft
- 1,378 unique values
- 0.10% nulls
- *Use for:* Comparing markets of different size properties

### Inventory Counts

**active_listing_count** (FLOAT64)
- Current homes for sale
- Range: 0 to 23,258
- 6,008 unique values
- 0.01% nulls
- *Use for:* Supply analysis, market activity levels

**new_listing_count** (FLOAT64)
- Fresh listings in period
- Range: 0 to 9,888
- 2,274 unique values
- 0.01% nulls
- *Note:* High null percentage (19.15%) in MM comparison

**pending_listing_count** (FLOAT64)
- Under contract properties
- Range: 0 to 14,211
- 4,075 unique values
- 7.28% nulls (higher than other counts)
- *Use for:* Demand indicator, market velocity

**total_listing_count** (FLOAT64)
- Aggregate of all listings
- Range: 0 to 33,580
- 7,738 unique values
- 0.01% nulls

### Market Velocity Metrics

**median_days_on_market** (FLOAT64)
- Time to sale indicator
- Range: 1 to 365 days
- 365 unique values (likely capped at 365)
- 0.11% nulls
- *Use for:* Market hotness, pricing appropriateness

**pending_ratio** (FLOAT64)
- Ratio of pending to active listings
- Range: 0.0 to 11.5
- 22,233 unique values
- 7.32% nulls
- Values >1 indicate more pendings than actives (hot market)
- *Use for:* Market momentum, buyer demand strength

### Price Change Behavior

**price_increased_count** (FLOAT64)
- Properties with price increases
- Range: 0 to 1,666
- 492 unique values
- **74.31% nulls in MM**, **73.67% nulls in YY**
- Sparse data suggests this is less common or tracked

**price_reduced_count** (FLOAT64)
- Properties with price reductions
- Range: 0 to 12,596
- 1,930 unique values
- **25.05% nulls in MM**, **25.53% nulls in YY**
- More complete than price increases (indicates more reductions occur)

**price_increased_share** (FLOAT64)
- Proportion of listings with increases
- Range: 0.0 to 4.0
- 0.04% nulls
- *Use for:* Seller confidence, market strength

**price_reduced_share** (FLOAT64)
- Proportion of listings with reductions
- Range: 0.0 to 4.0
- 3,919 unique values
- 0.04% nulls
- *Use for:* Market distress, overpricing indicators

### Property Characteristics

**median_square_feet** (FLOAT64)
- Typical property size
- Range: 4 to 30,902 sqft
- 3,322 unique values
- 0.10% nulls
- Extreme values may indicate data quality issues or unique properties

### Data Quality Indicator

**quality_flag** (FLOAT64)
- Binary quality indicator
- Values: 0.0, 1.0
- 10.72% nulls
- Likely: 1.0 = reliable data, 0.0 = questionable quality
- *Critical for:* Filtering analysis to high-quality data only

## Query Considerations

### Best Columns for Filtering
- **county_fips** or **county_name**: Geographic filtering
- **quality_flag = 1.0**: Ensure data reliability
- **median_listing_price**: Price range filtering (avoid extreme outliers >$10M)
- **active_listing_count > 0**: Exclude counties with no inventory
- **median_days_on_market**: Identify fast/slow markets (<30 days = hot, >90 = slow)

### Best Columns for Grouping/Aggregation
- **county_name**: Human-readable geographic grouping
- State (extractable from county_name via string parsing)
- Price ranges (bin median_listing_price)
- Market velocity tiers (bin median_days_on_market)

### Potential Join Keys
- **county_fips**: Standard US county identifier for joining demographic, economic, or geographic data
- State codes (extractable from county_name)

### Data Quality Considerations

1. **Temporal Analysis Limitations**: Without valid dates in `month_date_yyyymm`, time-series analysis within this table is impossible. May need external date information.

2. **Null Handling Strategy**:
   - Core metrics (<1% nulls): Safe to use with minimal impact
   - Comparative metrics (10-20% nulls): Consider WHERE clauses to exclude nulls
   - Price change counts (73-74% nulls): Use only when specifically analyzing price changes; expect small sample sizes

3. **Outlier Detection**:
   - Prices >$10M warrant investigation
   - Square footage extremes (<100 or >10,000) may be errors
   - Year-over-year changes >10x (1000%) are suspect

4. **Quality Flag Usage**: Always include `WHERE quality_flag = 1.0` for production analysis to ensure data reliability

5. **Small County Issues**: Counties with very low listing counts (<10) may have unstable metrics; consider minimum thresholds

### Recommended Query Patterns

```sql
-- Reliable county analysis
WHERE quality_flag = 1.0 
  AND active_listing_count >= 10
  AND median_listing_price IS NOT NULL

-- Hot market identification
WHERE median_days_on_market < 30
  AND pending_ratio > 1.0
  AND quality_flag = 1.0

-- Market health scoring
WHERE price_reduced_share < 0.10  -- <10% with reductions
  AND median_days_on_market < 60
  AND active_listing_count_yy < 0  -- Declining inventory
```

## Keywords

real estate, housing market, county data, inventory metrics, listing prices, days on market, pending ratio, active listings, market velocity, price changes, FIPS codes, US counties, housing supply, median prices, square footage, property metrics, market trends, year-over-year, month-over-month, housing demand, real estate analytics

## Table and Column Documentation

**Table Comment**: Not provided in source data

**Column Comments**: Not provided in source data