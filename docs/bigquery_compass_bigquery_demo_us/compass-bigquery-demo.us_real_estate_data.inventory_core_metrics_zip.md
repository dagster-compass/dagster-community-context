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
# Comprehensive Summary: US Real Estate Inventory Core Metrics by ZIP Code

## Keywords
real estate, housing market, inventory metrics, ZIP code analysis, listing prices, property sales, market trends, square footage, days on market, pending listings, active listings, price changes, monthly metrics, year-over-year comparisons, month-over-month comparisons, real estate analytics, housing inventory, market performance

## Overall Dataset Characteristics

### Dataset Size and Structure
- **Total Rows**: 3,142,815 records
- **Granularity**: ZIP code level real estate metrics
- **Coverage**: 34,141 unique ZIP codes across the United States
- **Geographic Scope**: ZIP codes ranging from 501 to 99929

### Data Quality Observations
- **High-quality core metrics**: Basic listing counts and prices have excellent data completeness (0.10%-0.25% null rates)
- **Significant missingness in derivative metrics**: Year-over-year and month-over-month comparison metrics show substantial null percentages (13%-90%)
- **Quality flag present**: A binary quality indicator (0.0 or 1.0) exists but is missing for 11.09% of records
- **Temporal dimension**: The `month_date_yyyymm` field is 100% null, suggesting temporal information may be embedded elsewhere or this is a snapshot dataset

### Notable Patterns
- **Negative values in change metrics**: Many comparison fields (YoY, MoM) contain values between -1.0 and positive ranges, indicating percentage changes or rates of change
- **Extreme outliers**: Some fields show extraordinary maximum values (e.g., median_listing_price up to $279M), likely representing luxury properties or data anomalies
- **Price reduction/increase tracking**: Separate metrics track both the count and share of listings with price changes

## Table and Column Documentation

### Table Comment
No table-level comment provided in the analysis.

### Column Comments
No column-level comments provided in the analysis.

## Detailed Column Analysis

### Geographic Identifiers

#### `postal_code` (INT64)
- **Completeness**: 100% (0% null)
- **Unique Values**: 34,141 distinct ZIP codes
- **Range**: 501 to 99,929
- **Purpose**: Primary geographic identifier for aggregating real estate metrics
- **Query Consideration**: Primary key for geographic filtering and joins

#### `zip_name` (STRING)
- **Completeness**: 97.70% (2.30% null)
- **Unique Values**: 26,083 distinct location names
- **Format**: "city, state" (e.g., "rockland, ma", "columbia falls, mt")
- **Query Consideration**: Human-readable location identifier for reporting; may have inconsistencies

### Core Listing Metrics

#### `total_listing_count` (FLOAT64)
- **Completeness**: 99.90% (0.10% null)
- **Unique Values**: 1,490
- **Range**: 0.0 to 2,860.0
- **Distribution**: Discrete values starting from 0
- **Query Consideration**: Primary metric for inventory volume; excellent for aggregation and filtering

#### `active_listing_count` (FLOAT64)
- **Completeness**: 99.85% (0.15% null)
- **Unique Values**: 1,302
- **Range**: 0.0 to 2,646.0
- **Query Consideration**: Key metric for current market supply

#### `pending_listing_count` (FLOAT64)
- **Completeness**: 79.31% (20.69% null)
- **Unique Values**: 555
- **Range**: 0.0 to 976.0
- **Query Consideration**: Indicates properties under contract; moderate null rate requires careful handling

#### `new_listing_count` (FLOAT64)
- **Completeness**: 99.90% (0.10% null)
- **Unique Values**: 190
- **Range**: 0.0 to 802.0
- **Query Consideration**: Tracks fresh inventory; useful for market momentum analysis

### Price Metrics

#### `median_listing_price` (FLOAT64)
- **Completeness**: 99.75% (0.25% null)
- **Unique Values**: 238,139 highly granular values
- **Range**: $1 to $279,000,000
- **Query Consideration**: Primary price indicator; wide range suggests need for outlier handling in analysis

#### `average_listing_price` (FLOAT64)
- **Completeness**: 99.75% (0.25% null)
- **Unique Values**: 894,375 highly granular values
- **Range**: $1 to $279,000,000
- **Query Consideration**: More sensitive to outliers than median; useful for revenue calculations

#### `median_listing_price_per_square_foot` (FLOAT64)
- **Completeness**: 99.04% (0.96% null)
- **Unique Values**: 3,167
- **Range**: $0 to $795,000/sq ft
- **Query Consideration**: Normalized price metric for comparing properties across sizes

### Property Characteristics

#### `median_square_feet` (FLOAT64)
- **Completeness**: 99.05% (0.95% null)
- **Unique Values**: 8,467
- **Range**: 1 to 12,503,400 sq ft
- **Query Consideration**: Property size indicator; extreme maximum suggests commercial properties or data errors

### Market Velocity Metrics

#### `median_days_on_market` (FLOAT64)
- **Completeness**: 99.07% (0.93% null)
- **Unique Values**: 365 (one per day)
- **Range**: 1 to 365 days
- **Query Consideration**: Key indicator of market heat; lower values suggest stronger demand

#### `pending_ratio` (FLOAT64)
- **Completeness**: 78.37% (21.63% null)
- **Unique Values**: 27,259
- **Range**: 0.0 to 94.5
- **Query Consideration**: Ratio metric indicating transaction velocity; high null rate limits usability

### Price Change Metrics

#### `price_reduced_count` (FLOAT64)
- **Completeness**: 99.90% (0.10% null)
- **Range**: 0.0 to 628.0
- **Query Consideration**: Tracks seller concessions

#### `price_increased_count` (FLOAT64)
- **Completeness**: 99.90% (0.10% null)
- **Range**: 0.0 to 268.0
- **Query Consideration**: Less common than reductions; indicates strong markets

#### `price_reduced_share` (FLOAT64)
- **Completeness**: 99.54% (0.46% null)
- **Range**: 0.0 to 4.0
- **Query Consideration**: Percentage of listings with price reductions

#### `price_increased_share` (FLOAT64)
- **Completeness**: 99.54% (0.46% null)
- **Range**: 0.0 to 4.0
- **Query Consideration**: Percentage of listings with price increases

### Year-over-Year Comparison Metrics (YoY)

All YoY metrics show **moderate to high null rates (15.86% - 89.71%)** and contain **negative values close to -1.0**, indicating percentage changes or proportional differences.

#### `total_listing_count_yy` (FLOAT64)
- **Null Rate**: 15.86%
- **Range**: -1.0 to 168.0
- **Interpretation**: Percentage change in total listings YoY

#### `active_listing_count_yy` (FLOAT64)
- **Null Rate**: 17.31%
- **Range**: -1.0 to 103.0

#### `pending_listing_count_yy` (FLOAT64)
- **Null Rate**: 37.49%
- **Range**: -1.0 to 421.0

#### `new_listing_count_yy` (FLOAT64)
- **Null Rate**: 45.00%
- **Range**: -1.0 to 39.0

#### `median_listing_price_yy` (FLOAT64)
- **Null Rate**: 16.67%
- **Range**: -1.0 to $1,789,999

#### `average_listing_price_yy` (FLOAT64)
- **Null Rate**: 16.67%
- **Range**: -1.0 to $1,789,999

#### `median_square_feet_yy` (FLOAT64)
- **Null Rate**: 17.36%
- **Range**: -0.9998 to 8,681.66

#### `median_listing_price_per_square_foot_yy` (FLOAT64)
- **Null Rate**: 17.37%
- **Range**: -1.0 to $1,135,999

#### `median_days_on_market_yy` (FLOAT64)
- **Null Rate**: 17.58%
- **Range**: -0.9973 to 364.0

#### `pending_ratio_yy` (FLOAT64)
- **Null Rate**: 37.99%
- **Range**: -82.33 to 92.63

#### `price_reduced_count_yy` (FLOAT64)
- **Null Rate**: 54.67%
- **Range**: -1.0 to 62.0

#### `price_increased_count_yy` (FLOAT64)
- **Null Rate**: 89.71% (extremely sparse)
- **Range**: -1.0 to 71.0

#### `price_reduced_share_yy` (FLOAT64)
- **Null Rate**: 16.03%
- **Range**: -4.0 to 4.0

#### `price_increased_share_yy` (FLOAT64)
- **Null Rate**: 16.03%
- **Range**: -4.0 to 4.0

### Month-over-Month Comparison Metrics (MoM)

All MoM metrics show **moderate to very high null rates (12.72% - 90.42%)** with similar negative value patterns as YoY metrics.

#### `total_listing_count_mm` (FLOAT64)
- **Null Rate**: 12.72%
- **Range**: -1.0 to 68.0

#### `active_listing_count_mm` (FLOAT64)
- **Null Rate**: 13.94%
- **Range**: -1.0 to 68.0

#### `pending_listing_count_mm` (FLOAT64)
- **Null Rate**: 32.61%
- **Range**: -1.0 to 295.0

#### `new_listing_count_mm` (FLOAT64)
- **Null Rate**: 44.80%
- **Range**: -1.0 to 37.0

#### `median_listing_price_mm` (FLOAT64)
- **Null Rate**: 13.53%
- **Range**: -1.0 to $949,899

#### `average_listing_price_mm` (FLOAT64)
- **Null Rate**: 13.53%
- **Range**: -1.0 to $949,899

#### `median_square_feet_mm` (FLOAT64)
- **Null Rate**: 14.16%
- **Range**: -0.9999 to 2,596.22

#### `median_listing_price_per_square_foot_mm` (FLOAT64)
- **Null Rate**: 14.17%
- **Range**: -1.0 to $859,787.36

#### `median_days_on_market_mm` (FLOAT64)
- **Null Rate**: 14.22%
- **Range**: -0.9973 to 341.0

#### `pending_ratio_mm` (FLOAT64)
- **Null Rate**: 33.49%
- **Range**: -69.05 to 75.37

#### `price_reduced_count_mm` (FLOAT64)
- **Null Rate**: 54.76%
- **Range**: -1.0 to 29.0

#### `price_increased_count_mm` (FLOAT64)
- **Null Rate**: 90.42% (extremely sparse)
- **Range**: -1.0 to 59.0

#### `price_reduced_share_mm` (FLOAT64)
- **Null Rate**: 13.02%
- **Range**: -4.0 to 4.0

#### `price_increased_share_mm` (FLOAT64)
- **Null Rate**: 13.02%
- **Range**: -4.0 to 4.0

### Data Quality Indicator

#### `quality_flag` (FLOAT64)
- **Null Rate**: 11.09%
- **Unique Values**: 2 (binary: 0.0, 1.0)
- **Query Consideration**: Should be used to filter for high-quality records where available

### Temporal Field

#### `month_date_yyyymm` (STRING)
- **Null Rate**: 100% (completely empty)
- **Query Consideration**: Cannot be used for temporal analysis; date context must come from external sources

## Potential Query Considerations

### Excellent for Filtering
1. **`postal_code`**: Primary geographic filter with complete data
2. **`zip_name`**: Human-readable location filter (check for nulls)
3. **`quality_flag`**: Filter for verified data quality
4. **Price ranges**: `median_listing_price`, `average_listing_price`
5. **Inventory levels**: `total_listing_count`, `active_listing_count`
6. **Market velocity**: `median_days_on_market`

### Excellent for Aggregation/Grouping
1. **Geographic grouping**: `postal_code`, `zip_name`
2. **Price bands**: Bucket `median_listing_price` or `average_listing_price`
3. **Market heat categories**: Bucket `median_days_on_market`
4. **Inventory size classes**: Group by `total_listing_count` ranges

### Potential Join Keys
1. **`postal_code`**: Primary key for joining with other ZIP-level datasets
2. **`zip_name`**: Secondary join option, but handle inconsistencies

### Data Quality Considerations for Queries

1. **Null Handling Critical**:
   - YoY and MoM metrics require careful null checking (15-90% null rates)
   - Always use `IS NOT NULL` filters when analyzing trend metrics
   - Consider separate analyses for records with complete vs. incomplete comparison data

2. **Outlier Management**:
   - Extreme price values (up to $279M) suggest filtering may be needed
   - Consider using median over average for robust analysis
   - Square footage outliers (12M+ sq ft) likely indicate data errors

3. **Negative Values**:
   - Comparison metrics (_yy, _mm) use -1.0 to indicate 100% decrease
   - Values near -1.0 should be interpreted as dramatic declines
   - Consider whether to exclude -1.0 values (possible data quality flags)

4. **Sparse Metrics**:
   - `price_increased_count_yy` (89.71% null) and `price_increased_count_mm` (90.42% null) have very limited usability
   - These should only be used when analyzing specific high-activity markets

5. **Temporal Context**:
   - With `month_date_yyyymm` completely null, temporal analysis requires external date context
   - YoY and MoM metrics provide change information but not absolute dates

6. **Ratio Interpretations**:
   - `pending_ratio` ranges to 94.5, suggesting it may be a percentage rather than a true ratio
   - Share metrics (`price_reduced_share`, `price_increased_share`) range to 4.0, indicating these are also percentages or proportions

### Recommended Query Patterns

1. **Basic Inventory Analysis**: Use core metrics with minimal nulls (`total_listing_count`, `median_listing_price`, `postal_code`)

2. **Market Health Analysis**: Combine `median_days_on_market`, `pending_ratio`, and `active_listing_count` with null filters

3. **Price Trend Analysis**: Use YoY/MoM metrics with explicit null handling and outlier filtering

4. **Geographic Comparisons**: Group by state (extract from `zip_name`) or compare specific ZIP codes

5. **Quality-Filtered Analysis**: Always consider including `WHERE quality_flag = 1.0` for high-confidence results