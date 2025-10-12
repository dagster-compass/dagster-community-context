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
# Table Summary: compass-bigquery-demo.us_real_estate_data.inventory_core_metrics_country

## Overall Dataset Characteristics

- **Total Rows**: 111
- **General Data Quality**: The dataset appears to be time-series real estate market data at a country level with good overall quality. However, there's a systematic missing data pattern affecting approximately 10.81% of rows across most analytical columns.
- **Notable Patterns**: 
  - Most analytical metrics (year-over-year and month-over-month changes) have consistent null patterns (10.81%)
  - The `month_date_yyyymm` column is completely null (100%), suggesting potential data pipeline issues
  - All data is for "United States" only, indicating this is a country-level aggregation
  - Data ranges suggest this covers multiple time periods with various market conditions

## Column Details

### Geographic/Categorical Columns
- **country (STRING)**: Single value "United States" across all rows, serves as identifier
- **month_date_yyyymm (STRING)**: Completely null (100%) - likely a data quality issue

### Core Inventory Metrics
- **total_listing_count (INT64)**: Complete data, ranges 815,253-1,873,209 listings
- **active_listing_count (INT64)**: Complete data, ranges 346,514-1,463,025 listings  
- **pending_listing_count (INT64)**: Complete data, ranges 257,571-659,596 listings
- **new_listing_count (INT64)**: Complete data, ranges 215,940-584,354 listings

### Price Metrics
- **average_listing_price (FLOAT64)**: Complete data, ranges $439,191-$791,655
- **median_listing_price (FLOAT64)**: Complete data, ranges $249,900-$449,000
- **median_listing_price_per_square_foot (FLOAT64)**: Complete data, ranges $125-$234/sqft

### Property Size Metrics
- **median_square_feet (FLOAT64)**: Complete data, ranges 1,776-1,997 sqft
- **median_days_on_market (INT64)**: Complete data, ranges 30-88 days

### Price Change Activity
- **price_reduced_count (FLOAT64)**: Complete data, ranges 64,958-458,240 reductions
- **price_increased_count (INT64)**: Complete data, ranges 12,220-61,028 increases
- **price_reduced_share (FLOAT64)**: Complete data, ranges 5.37%-21.68%
- **price_increased_share (FLOAT64)**: Complete data, ranges 0.86%-3.47%

### Derived Ratios
- **pending_ratio (FLOAT64)**: Complete data, ranges 0.23-1.48
- **quality_flag (FLOAT64)**: Only contains 0.0 values where not null

### Year-over-Year Change Metrics (10.81% null)
All YoY metrics show percentage changes, with ranges indicating significant market volatility:
- **total_listing_count_yy**: -27.12% to +22.68%
- **average_listing_price_yy**: -4.08% to +33.37%
- **median_listing_price_yy**: -2.2% to +18.19%
- **pending_listing_count_yy**: -36.9% to +58.77%
- **new_listing_count_yy**: -36.84% to +40.99%

### Month-over-Month Change Metrics (10.81% null)
MoM metrics show shorter-term fluctuations:
- **total_listing_count_mm**: -14.06% to +11.61%
- **average_listing_price_mm**: -3.74% to +5.66%
- **median_listing_price_mm**: -3.39% to +5.02%

## Query Considerations

### Good for Filtering
- **country**: Single value, useful for validation
- **median_days_on_market**: Discrete values (30-88), good for market speed analysis
- **quality_flag**: Binary indicator for data quality filtering

### Good for Grouping/Aggregation
- Time-based grouping would require the missing `month_date_yyyymm` field
- **median_days_on_market** ranges for market categorization (fast/medium/slow markets)
- Price ranges could be created from listing price metrics

### Potential Relationships
- Strong correlation likely between listing counts and market activity
- Price per square foot relationships with overall pricing metrics
- Pending ratio as market health indicator

### Data Quality Considerations
- **Critical Issue**: `month_date_yyyymm` is completely null - time-series analysis severely limited
- **Systematic Nulls**: 10.81% missing pattern across analytical metrics suggests specific time periods or data collection issues
- **Quality Flag**: Available but limited value (only 0.0 where present)
- **Complete Metrics**: Core inventory and price metrics are complete and reliable

## Keywords

real estate, inventory, listings, market metrics, pricing, United States, time series, month over month, year over year, pending listings, active listings, days on market, price changes, square footage, market analysis

## Table and Column Documentation

**Table Comment**: Not provided in the analysis data.

**Column Comments**: No individual column comments were provided in the analysis data.