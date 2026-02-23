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
# Table Documentation Summary: compass-bigquery-demo.us_real_estate_data.inventory_core_metrics_metro

## Overall Dataset Characteristics

- **Total Rows**: 102,675
- **Dataset Type**: Real estate inventory metrics aggregated at the metro/CBSA (Core Based Statistical Area) level
- **Time Series Data**: Contains monthly snapshots with month-over-month (mm) and year-over-year (yy) comparisons
- **Geographic Coverage**: 925 unique metropolitan areas across the United States
- **Data Quality**: Generally high quality with systematic null patterns primarily in comparison metrics (mm/yy fields showing ~10-11% nulls, likely for earliest time periods)
- **Critical Issue**: The `month_date_yyyymm` column is 100% null, making temporal analysis challenging without additional date context

## Column Details

### Geographic Identifiers

**cbsa_code** (INT64)
- Unique identifier for metropolitan areas
- Range: 10100 to 49820
- 925 unique codes
- No nulls - reliable join key
- Standard Census Bureau CBSA codes

**cbsa_title** (STRING)
- Human-readable metro area names (e.g., "Indianapolis-Carmel-Greenwood, IN")
- 925 unique values matching cbsa_code count
- No nulls
- Format: City-SubCity-Region, STATE

**householdrank** (INT64)
- Ranking metric (1-925, presumably by household count/market size)
- Lower numbers = larger markets (e.g., rank 1 = largest metro)
- No nulls

### Pricing Metrics

**median_listing_price** (FLOAT64)
- Core pricing metric
- Range: $19,900 to $5,508,750
- No nulls - highly reliable
- 25,318 unique values indicating granular pricing data

**median_listing_price_mm** (FLOAT64)
- Month-over-month change (decimal format: 0.0817 = 8.17% increase)
- 10.81% nulls (likely earliest months lacking comparison data)
- Range: -55.35% to +298.55% (extreme volatility in some markets)

**median_listing_price_yy** (FLOAT64)
- Year-over-year change
- 10.81% nulls
- Range: -77.58% to +498.48%

**average_listing_price** (FLOAT64)
- Mean price (vs median)
- Range: $44,444 to $23,524,874
- 93,676 unique values (very granular)
- Includes mm/yy comparison columns with similar null patterns

**median_listing_price_per_square_foot** (FLOAT64)
- Normalized pricing metric
- Range: $22 to $1,778 per sq ft
- 1,084 unique values
- No nulls in base metric

**median_square_feet** (FLOAT64)
- Property size metric
- Range: 892 to 6,000 sq ft
- 2,075 unique values

### Inventory Counts

**active_listing_count** (INT64)
- Current active listings
- Range: 0 to 69,796
- No nulls
- 7,310 unique values

**new_listing_count** (INT64)
- New listings added in period
- Range: 0 to 27,262
- No nulls
- 3,520 unique values

**total_listing_count** (INT64)
- Total listings (active + pending presumably)
- Range: 1 to 83,125
- No nulls
- 9,160 unique values

**pending_listing_count** (FLOAT64)
- Listings under contract
- Range: 0 to 28,578
- 2.70% nulls (slightly higher than other metrics)
- Critical for market velocity analysis

### Market Velocity Metrics

**median_days_on_market** (FLOAT64)
- Time to sale/contract
- Range: 3 to 322 days
- 0.01% nulls (nearly complete)
- 210 unique values
- Lower values = hotter markets

**pending_ratio** (FLOAT64)
- Ratio metric (pending/active presumably)
- Range: 0.0 to 8.0064
- 2.70% nulls
- 18,056 unique values (highly granular)
- High values suggest strong buyer demand

### Price Change Activity

**price_increased_count** (INT64)
- Listings with price increases
- Range: 0 to 4,978
- High null percentage: 55.50% in mm, 54.41% in yy comparisons
- 801 unique values

**price_increased_share** (FLOAT64)
- Proportion of listings with price increases
- Range: 0.0 to 0.3815 (0% to 38.15%)
- No nulls in base metric
- Indicates seller confidence

**price_reduced_count** (FLOAT64)
- Listings with price reductions
- Range: 0 to 22,456
- 2,750 unique values
- Lower null percentage (~11.5%) than price_increased metrics

**price_reduced_share** (FLOAT64)
- Proportion with price reductions
- Range: 0.0 to 0.6667 (0% to 66.67%)
- No nulls in base metric
- Counter-indicator to price_increased_share

### Data Quality

**quality_flag** (FLOAT64)
- Binary quality indicator (0.0 or 1.0)
- 10.81% nulls
- Appears to flag data quality issues
- Values: null, 0.0 (good), 1.0 (potential issue)

## Table and Column Docs

No table-level or column-level comments were provided in the schema.

## Potential Query Considerations

### Good Filtering Columns
- **cbsa_code/cbsa_title**: Filter by specific metro areas
- **householdrank**: Filter by market size (e.g., top 50 metros)
- **quality_flag**: Exclude low-quality data (WHERE quality_flag = 0.0 OR quality_flag IS NULL)
- **median_days_on_market**: Identify hot/cold markets (e.g., < 30 days)
- **pending_ratio**: High-demand markets (e.g., > 1.0)

### Good Grouping/Aggregation Columns
- **cbsa_code/cbsa_title**: Regional analysis
- **householdrank**: Market tier analysis (bucketing ranks)
- Price range buckets (CASE statements on median_listing_price)

### Potential Join Keys
- **cbsa_code**: Primary key for joining with other geographic datasets
- Likely joins to demographic, economic, or geographic reference tables

### Data Quality Considerations
1. **Missing Time Dimension**: month_date_yyyymm is 100% null - queries requiring time filtering will need workarounds
2. **Null Patterns**: mm/yy comparison fields have ~10-11% nulls (earliest periods)
3. **Price Change Nulls**: price_increased metrics have >50% nulls - use with caution
4. **Quality Flag**: Consider filtering WHERE quality_flag = 0 for reliable analysis
5. **Extreme Values**: Some metrics show extreme ranges (e.g., price changes >400%) - may need outlier handling
6. **Zero Counts**: Many count fields include 0 values, which is valid for small markets

### Analytical Patterns
- **Market Heat**: median_days_on_market (lower = hotter), pending_ratio (higher = hotter)
- **Pricing Pressure**: Compare price_increased_share vs price_reduced_share
- **Market Size**: Use householdrank or active_listing_count
- **Affordability**: median_listing_price_per_square_foot for normalized comparisons
- **Market Trends**: Use mm/yy fields for temporal analysis despite null values

## Keywords

Real estate, housing market, inventory metrics, CBSA, metropolitan statistical area, metro area, listing prices, days on market, pending sales, active listings, new listings, price changes, market velocity, housing affordability, median home prices, price per square foot, market trends, housing inventory, real estate analytics, property listings, market analysis, geographic real estate data, US housing market, residential real estate