---
columns:
- active_listing_count (INT64)
- active_listing_count_mm (FLOAT64)
- active_listing_count_yy (FLOAT64)
- average_listing_price (FLOAT64)
- average_listing_price_mm (FLOAT64)
- average_listing_price_yy (FLOAT64)
- cbsa_code (INT64)
- cbsa_title (STRING)
- householdrank (INT64)
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
- new_listing_count (INT64)
- new_listing_count_mm (FLOAT64)
- new_listing_count_yy (FLOAT64)
- pending_listing_count (FLOAT64)
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
schema_hash: 6270d365685bef4b40bf9d4f9061148c6ee6c0642b9d6a5bf4f5860252556ccf

---
# Table Documentation: US Real Estate Inventory Core Metrics by Metro Area

## Overview

This table contains comprehensive real estate inventory metrics for 925 metropolitan areas (CBSAs - Core Based Statistical Areas) across the United States. The dataset consists of **102,675 total rows** representing time-series data tracking various housing market indicators.

### Data Quality Observations
- **Critical Issue**: The `month_date_yyyymm` column is 100% null, indicating missing temporal reference data
- Most core metrics have high data quality (0-3% null rates)
- Change metrics (_mm and _yy suffixes) consistently show ~11% null rates, likely representing periods without prior comparison data
- Price increase metrics have notably higher null rates (54-55%), suggesting these are conditionally calculated fields
- Overall data quality is good for primary metrics but variable for derived/comparative metrics

## Column Documentation

### Geographic Identifiers

**cbsa_title** (STRING)
- Metro area names (e.g., "Minneapolis-St. Paul-Bloomington, MN-WI")
- 925 unique metro areas
- 0% null - complete coverage
- Use for: Human-readable filtering, grouping, and reporting

**cbsa_code** (INT64)
- Standardized CBSA identifier codes
- Range: 10100 to 49820
- 925 unique values matching title count
- 0% null
- Use for: Joins with other census/geographic datasets, unique identifiers

**householdrank** (INT64)
- Metro area ranking (presumably by household count/size)
- Range: 1 (largest) to 925 (smallest)
- Examples: 16 = Minneapolis-St. Paul, 676 = Columbus NE
- Use for: Market size segmentation and filtering

### Temporal Reference

**month_date_yyyymm** (STRING)
- **100% NULL - CRITICAL DATA QUALITY ISSUE**
- Intended to store month/year in YYYYMM format
- Without this field, temporal analysis requires external date context

### Price Metrics

**median_listing_price** (FLOAT64)
- Current median listing price
- Range: $19,900 to $5,508,750
- 25,318 unique values, 0% null
- High-quality metric for price analysis

**median_listing_price_mm** (FLOAT64)
- Month-over-month price change (decimal format: 0.0103 = 1.03% increase)
- Range: -55.35% to +298.55%
- 10.81% null (first months without prior comparison)

**median_listing_price_yy** (FLOAT64)
- Year-over-year price change
- Range: -77.58% to +498.48%
- 10.81% null

**median_listing_price_per_square_foot** (FLOAT64)
- Price per square foot metric
- Range: $22 to $1,778
- 1,084 unique values, 0% null
- Includes _mm and _yy variants (10.81% null)

**average_listing_price** (FLOAT64)
- Mean listing price (vs median)
- Range: $44,444 to $23,524,874
- 93,676 unique values showing high granularity
- More sensitive to luxury outliers than median

### Inventory Count Metrics

**active_listing_count** (INT64)
- Current active listings
- Range: 0 to 69,796
- 7,310 unique values, 0% null
- Key metric for inventory availability

**new_listing_count** (INT64)
- New listings added in period
- Range: 0 to 27,262
- 3,520 unique values, 0% null

**total_listing_count** (INT64)
- Total listings (active + pending)
- Range: 1 to 83,125
- 9,160 unique values, 0% null

**pending_listing_count** (FLOAT64)
- Listings under contract
- Range: 0 to 28,578
- 2.70% null (slightly higher than other counts)

All count metrics include _mm and _yy change variants (~11% null)

### Market Velocity Metrics

**median_days_on_market** (FLOAT64)
- Days listings remain active
- Range: 3 to 322 days
- 210 unique values, 0.01% null
- Key indicator of market pace

**pending_ratio** (FLOAT64)
- Ratio of pending to active listings
- Range: 0.0 to 8.0064
- 2.70% null
- Higher values indicate stronger demand

### Price Change Behavior

**price_increased_count** (INT64)
- Number of listings with price increases
- Range: 0 to 4,978
- **55.50% null for _mm variant** - only calculated when sufficient data
- **54.41% null for _yy variant**

**price_increased_share** (FLOAT64)
- Percentage of listings with price increases
- Range: 0.0 to 0.3815 (38.15%)
- 0% null for base metric, 10.81% for change variants

**price_reduced_count** (FLOAT64)
- Number of listings with price reductions
- Range: 0 to 22,456
- ~11.5% null for change variants
- Indicator of market softness

**price_reduced_share** (FLOAT64)
- Percentage of listings with reductions
- Range: 0.0 to 0.6667 (66.67%)
- More complete than price increase data

### Property Characteristics

**median_square_feet** (FLOAT64)
- Median property size
- Range: 892 to 6,000 sq ft
- 2,075 unique values, 0% null
- Includes _mm and _yy change variants

### Data Quality Flag

**quality_flag** (FLOAT64)
- Binary quality indicator (0.0 or 1.0)
- 10.81% null
- Appears to flag data quality issues or special conditions

## Keywords

real estate, housing market, inventory metrics, CBSA, metro areas, listing prices, market trends, days on market, pending sales, active listings, price changes, housing inventory, real estate analytics, metropolitan statistical areas, market velocity, price per square foot, housing supply, market dynamics, time series, real estate data

## Table and Column Comments

**Table Comment**: Not provided in the analysis report.

**Column Comments**: No individual column comments were provided in the source data.

## Query Considerations

### Excellent for Filtering
- **cbsa_title/cbsa_code**: Filter by specific metros or regions
- **householdrank**: Segment by market size (top 50, mid-market, small markets)
- **quality_flag**: Exclude questionable data points
- **Date ranges**: Currently impossible due to null month_date_yyyymm - requires external date context

### Excellent for Grouping/Aggregation
- **cbsa_title/cbsa_code**: Metro-level analysis
- **householdrank ranges**: Market tier analysis (1-50, 51-200, 201+)
- Time periods: Requires external date field

### Potential Join Keys
- **cbsa_code**: Primary key for joining with census, economic, or demographic data
- Combination of cbsa_code + month_date (when available) for time-series joins

### Data Quality Considerations
1. **Critical**: month_date_yyyymm is 100% null - temporal queries require external date context
2. All percentage change metrics (_mm, _yy) have ~11% nulls - use COALESCE or filter appropriately
3. Price increase metrics have 54-55% nulls - likely only calculated under certain conditions
4. pending_listing_count has slightly higher nulls (2.7%) than other counts
5. Some extreme outliers exist (e.g., average_listing_price up to $23.5M) - consider using MEDIAN over AVG for robust statistics
6. Change metrics can show extreme values (e.g., 91.5x increase) - validate or cap for visualization

### Recommended Query Patterns
- Use `WHERE quality_flag = 0.0` or `IS NULL` to filter for standard data
- Use `COALESCE(metric_mm, 0)` when nulls should be treated as no change
- Filter by householdrank for market size segments
- Join on cbsa_code for enrichment with external datasets
- Be cautious with price_increased metrics due to high null rates