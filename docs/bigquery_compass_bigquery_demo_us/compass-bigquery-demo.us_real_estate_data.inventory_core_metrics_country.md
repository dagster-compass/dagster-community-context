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
# Table Analysis Summary: compass-bigquery-demo.us_real_estate_data.inventory_core_metrics_country

## Overall Dataset Characteristics

- **Total rows**: 111 records
- **Geographic scope**: Country-level data (United States only)
- **Data quality**: Generally high with consistent non-null values for core metrics, but 10.81% null values for month-over-month and year-over-year comparison metrics
- **Time series nature**: Contains current values and percentage changes (month-over-month "_mm" and year-over-year "_yy" suffixes)
- **Notable patterns**: 
  - One completely null column (`month_date_yyyymm`)
  - Quality flag column with only zeros where not null
  - Single country dataset (all records are "United States")

## Column Details

### Core Inventory Metrics
- **total_listing_count** (INT64): Total property listings, ranging from 815,253 to 1,873,209
- **active_listing_count** (INT64): Active listings, ranging from 346,514 to 1,463,025
- **pending_listing_count** (INT64): Pending listings, ranging from 257,571 to 659,596
- **new_listing_count** (INT64): New listings, ranging from 215,940 to 584,354

### Price Metrics
- **average_listing_price** (FLOAT64): Average price from $439,191 to $791,655
- **median_listing_price** (FLOAT64): Median price from $249,900 to $449,000
- **median_listing_price_per_square_foot** (FLOAT64): Price per sq ft from $125 to $234

### Property Characteristics
- **median_square_feet** (FLOAT64): Property sizes from 1,776 to 1,997 sq ft
- **median_days_on_market** (INT64): Market time from 30 to 88 days

### Price Change Metrics
- **price_reduced_count** (FLOAT64): Properties with price reductions, 64,958 to 458,240
- **price_reduced_share** (FLOAT64): Share of price reductions, 5.37% to 21.68%
- **price_increased_count** (INT64): Properties with price increases, 12,220 to 61,028
- **price_increased_share** (FLOAT64): Share of price increases, 0.86% to 3.47%

### Market Ratios
- **pending_ratio** (FLOAT64): Pending to active listings ratio, 0.23 to 1.48

### Temporal Comparison Metrics (10.81% null)
All "_mm" (month-over-month) and "_yy" (year-over-year) columns show percentage changes with varying ranges, typically between -50% to +50% for most metrics.

### Data Quality and Geographic Identifiers
- **country** (STRING): Single value "United States"
- **quality_flag** (FLOAT64): Only contains 0.0 where not null
- **month_date_yyyymm** (STRING): Completely null column

## Potential Query Considerations

### Good for Filtering
- **country**: Though single-valued in this dataset
- **median_days_on_market**: Discrete ranges for market speed analysis
- **quality_flag**: Data quality filtering (though limited utility here)

### Good for Grouping/Aggregation
- **median_days_on_market**: Market speed categories
- Value ranges of price metrics for bucketing analysis
- Time-based groupings if temporal data were available

### Key Analytical Columns
- Core inventory counts for supply analysis
- Price metrics for market valuation trends
- Ratio metrics for market dynamics
- Change metrics for trend analysis

### Data Quality Considerations
- **Missing temporal data**: 10.81% of records lack comparison metrics
- **Single geographic scope**: All data is US-level
- **Null month_date_yyyymm**: Completely missing temporal identifier
- **Quality flag uniformity**: May indicate data preprocessing or quality standards

### Potential Relationships
- Strong correlations likely between listing counts and market activity
- Price metrics should correlate with market conditions
- Pending ratios indicate market velocity
- Change metrics provide trend context

## Keywords
real estate, inventory, listings, housing market, property prices, market metrics, pending sales, active listings, price changes, days on market, square footage, United States housing data, real estate analytics, market trends

## Table and Column Documentation
No table comment or column comments are present in the provided analysis.