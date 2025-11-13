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
# Comprehensive Data Summary: US Real Estate Inventory Core Metrics (Country Level)

## Overall Dataset Characteristics

**Total Rows:** 111

**General Data Quality:**
- The dataset contains approximately 10.81% null values across most analytical columns (month-over-month and year-over-year metrics)
- Core metrics (counts, prices, ratios) have 0% null values, indicating complete data for primary measurements
- One column (`month_date_yyyymm`) is 100% null, suggesting it may be unused or deprecated
- The `country` column contains only "United States", indicating this is a country-level aggregated dataset
- `quality_flag` has minimal variation (only value 0.0 where present), suggesting data quality issues are rare

**Notable Patterns:**
- The dataset appears to be a time-series of monthly real estate metrics for the United States
- 111 rows likely represent approximately 9+ years of monthly data
- Data includes both absolute counts and percentage change metrics (month-over-month "_mm" and year-over-year "_yy" suffixes)
- Price metrics are tracked in multiple ways: average, median, per square foot
- Listing lifecycle stages are captured: total, active, pending, new
- Price change behavior is tracked: reductions and increases

## Column Details

### Geographic Identifier
**`country` (STRING)**
- Always "United States" (single unique value)
- No null values
- This is a country-level aggregation table

### Primary Time Identifier
**`month_date_yyyymm` (STRING)**
- 100% null values - appears to be unused/deprecated
- Not suitable for time-based queries in current state

### Inventory Counts (Core Metrics)

**`total_listing_count` (INT64)**
- No nulls, 111 unique values
- Range: 815,253 to 1,873,209 listings
- Total inventory across all stages

**`active_listing_count` (INT64)**
- No nulls, 111 unique values
- Range: 346,514 to 1,463,025 listings
- Currently available listings on market

**`pending_listing_count` (INT64)**
- No nulls, 111 unique values
- Range: 257,571 to 659,596 listings
- Listings under contract but not closed

**`new_listing_count` (INT64)**
- No nulls, 111 unique values
- Range: 215,940 to 584,354 listings
- Fresh listings added in the period

### Price Metrics (Core)

**`average_listing_price` (FLOAT64)**
- No nulls, 111 unique values
- Range: $439,191 to $791,655
- Mean listing price across all properties

**`median_listing_price` (FLOAT64)**
- No nulls, 94 unique values
- Range: $249,900 to $449,000
- Median listing price (less sensitive to outliers)

**`median_listing_price_per_square_foot` (FLOAT64)**
- No nulls, 55 unique values
- Range: $125 to $234 per sq ft
- Normalized price metric

### Property Characteristics

**`median_square_feet` (FLOAT64)**
- No nulls, 86 unique values
- Range: 1,776 to 1,997 square feet
- Median property size

**`median_days_on_market` (INT64)**
- No nulls, 45 unique values
- Range: 30 to 88 days
- Time to sell/pending status

### Price Change Tracking

**`price_reduced_count` (FLOAT64)**
- No nulls, 111 unique values
- Range: 64,958 to 458,240 properties
- Absolute count of price reductions

**`price_reduced_share` (FLOAT64)**
- No nulls, 109 unique values
- Range: 0.0537 to 0.2168 (5.37% to 21.68%)
- Proportion of listings with price reductions

**`price_increased_count` (INT64)**
- No nulls, 109 unique values
- Range: 12,220 to 61,028 properties
- Absolute count of price increases

**`price_increased_share` (FLOAT64)**
- No nulls, 88 unique values
- Range: 0.0086 to 0.0347 (0.86% to 3.47%)
- Proportion of listings with price increases

### Derived Ratios

**`pending_ratio` (FLOAT64)**
- No nulls, 111 unique values
- Range: 0.2322 to 1.4765
- Ratio of pending to active listings (market temperature indicator)

### Change Metrics (Month-over-Month "_mm" suffix)

All "_mm" columns have **10.81% null values**, likely representing the first month where YoY comparison isn't possible:

- `total_listing_count_mm`: Range -14.06% to +11.61%
- `active_listing_count_mm`: Range -15.35% to +26.18%
- `pending_listing_count_mm`: Range -14.61% to +27.17%
- `new_listing_count_mm`: Range -27.61% to +42.03%
- `average_listing_price_mm`: Range -3.74% to +5.66%
- `median_listing_price_mm`: Range -3.39% to +5.02%
- `median_listing_price_per_square_foot_mm`: Range -1.61% to +3.88%
- `median_square_feet_mm`: Range -1.78% to +2.18%
- `median_days_on_market_mm`: Range -31.36% to +20.59%
- `price_reduced_count_mm`: Range -40.76% to +74.56%
- `price_reduced_share_mm`: Range -6.11% to +4.59%
- `price_increased_count_mm`: Range -27.81% to +42.26%
- `price_increased_share_mm`: Range -0.76% to +1.19%
- `pending_ratio_mm`: Range -29.23% to +27.10%

### Change Metrics (Year-over-Year "_yy" suffix)

All "_yy" columns have **10.81% null values**:

- `total_listing_count_yy`: Range -27.12% to +22.68%
- `active_listing_count_yy`: Range -53.74% to +67.17%
- `pending_listing_count_yy`: Range -36.90% to +58.77%
- `new_listing_count_yy`: Range -36.84% to +40.99%
- `average_listing_price_yy`: Range -4.08% to +33.37%
- `median_listing_price_yy`: Range -2.20% to +18.19%
- `median_listing_price_per_square_foot_yy`: Range -0.94% to +23.63%
- `median_square_feet_yy`: Range -7.28% to +4.14%
- `median_days_on_market_yy`: Range -48.53% to +59.26%
- `price_reduced_count_yy`: Range -61.74% to +174.13%
- `price_reduced_share_yy`: Range -6.84% to +10.84%
- `price_increased_count_yy`: Range -59.15% to +120.92%
- `price_increased_share_yy`: Range -1.75% to +1.77%
- `pending_ratio_yy`: Range -77.88% to +99.31%

### Data Quality Indicator

**`quality_flag` (FLOAT64)**
- 10.81% null values
- Only one unique value: 0.0
- Appears to flag data quality issues (0.0 = good quality)

## Potential Query Considerations

### Ideal Filtering Columns
- **Time-based filtering**: Would require external date column or row indexing since `month_date_yyyymm` is null
- **Threshold filtering**: All price metrics, counts, and ratios work well for range queries
- **Market condition filtering**: `pending_ratio`, `median_days_on_market`, price change shares

### Good for Aggregation/Grouping
- Since this is country-level data, aggregation would be limited to:
  - Time-based aggregations (if date information available)
  - Calculating averages/trends across all 111 periods
  - Categorizing market conditions (hot/cold markets based on metrics)

### Join Considerations
- **No obvious join keys** in this table alone
- Would likely join to:
  - A separate date dimension table using a row identifier
  - Regional/state-level tables with similar metrics
  - External economic indicators by time period

### Data Quality Considerations for Queries

1. **Null Handling**: ~11% of rows lack "_mm" and "_yy" metrics
   - Queries using change metrics should use `WHERE [metric] IS NOT NULL`
   - First ~12 rows likely represent early data collection period

2. **Percentage vs. Absolute Values**: 
   - Change metrics are proportions (0.05 = 5% change)
   - Share metrics are also proportions
   - Multiply by 100 for percentage displays

3. **Data Completeness**:
   - Core metrics (counts, prices, ratios) are 100% complete
   - Trend analysis requires non-null comparison metrics

4. **Outlier Detection**:
   - Some YoY metrics show extreme changes (e.g., +174% in price_reduced_count_yy)
   - May indicate market volatility or data quality issues during certain periods

5. **Time Series Analysis**:
   - 111 rows suggests complete monthly series
   - Gap analysis would require external date validation
   - Seasonality patterns likely present in listing counts and days on market

## Keywords

Real estate, housing market, inventory metrics, listing prices, market trends, pending ratio, days on market, price changes, month-over-month, year-over-year, United States housing, property metrics, real estate analytics, housing supply, active listings, new listings, median price, average price, price per square foot, market velocity, housing statistics, time series data, market indicators

## Table and Column Documentation

**Table Comment:** Not provided in the analysis report.

**Column Comments:** No column-level comments were provided in the analysis report. The column names follow a clear naming convention where:
- Base metrics have no suffix (e.g., `total_listing_count`)
- Month-over-month changes use `_mm` suffix
- Year-over-year changes use `_yy` suffix
- Geographic identifier is `country`
- Quality indicators use `quality_flag` naming