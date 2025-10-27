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

- **Total Rows**: 111 records
- **Geographic Coverage**: United States only (single country dataset)
- **Data Quality**: Generally good with consistent patterns of missing data
- **Missing Data Pattern**: 10.81% null values across most analytical columns, suggesting systematic data collection limitations for certain time periods
- **Time Series Nature**: Contains month-over-month (mm) and year-over-year (yy) change metrics, indicating longitudinal real estate market analysis
- **Completeness Issue**: The `month_date_yyyymm` column is completely null (100%), indicating missing temporal identifiers

## Column Details

### Geographic and Identifier Columns
- **country** (STRING): Single value "United States" - perfect for filtering but not useful for grouping
- **month_date_yyyymm** (STRING): Completely null - temporal identifier missing from dataset

### Core Inventory Metrics (Absolute Values)
- **total_listing_count** (INT64): Range 815K-1.9M, no nulls - good for aggregation and trend analysis
- **active_listing_count** (INT64): Range 347K-1.5M, no nulls - key inventory metric
- **pending_listing_count** (INT64): Range 258K-660K, no nulls - market activity indicator
- **new_listing_count** (INT64): Range 216K-584K, no nulls - supply indicator

### Pricing Metrics (Absolute Values)
- **average_listing_price** (FLOAT64): Range $439K-$792K, no nulls - premium pricing indicator
- **median_listing_price** (FLOAT64): Range $250K-$449K, no nulls - more representative pricing
- **median_listing_price_per_square_foot** (FLOAT64): Range $125-$234, no nulls - standardized pricing

### Property Characteristics
- **median_square_feet** (FLOAT64): Range 1,776-1,997 sq ft, no nulls - property size indicator
- **median_days_on_market** (INT64): Range 30-88 days, no nulls - market velocity metric

### Market Activity Metrics
- **price_reduced_count** (FLOAT64): Range 65K-458K, no nulls - price adjustment activity
- **price_increased_count** (INT64): Range 12K-61K, no nulls - market strength indicator
- **price_reduced_share** (FLOAT64): Range 5.4%-21.7%, no nulls - percentage of listings with price cuts
- **price_increased_share** (FLOAT64): Range 0.9%-3.5%, no nulls - percentage of listings with price increases

### Market Health Indicators
- **pending_ratio** (FLOAT64): Range 0.23-1.48, no nulls - demand/supply balance
- **quality_flag** (FLOAT64): Single value 0.0 where present - data quality indicator

### Change Metrics (Month-over-Month)
All _mm columns have 10.81% nulls, representing percentage changes:
- **total_listing_count_mm**: Range -14.1% to +11.6%
- **average_listing_price_mm**: Range -3.7% to +5.7%
- **median_listing_price_mm**: Range -3.4% to +5.0%
- **pending_listing_count_mm**: Range -14.6% to +27.2%
- **active_listing_count_mm**: Range -15.4% to +26.2%

### Change Metrics (Year-over-Year)
All _yy columns have 10.81% nulls, representing percentage changes:
- **total_listing_count_yy**: Range -27.1% to +22.7%
- **average_listing_price_yy**: Range -4.1% to +33.4%
- **median_listing_price_yy**: Range -2.2% to +18.2%
- **pending_listing_count_yy**: Range -36.9% to +58.8%
- **active_listing_count_yy**: Range -53.7% to +67.2%

## Query Considerations

### Good for Filtering
- Absolute value columns (no nulls): `total_listing_count`, `average_listing_price`, `median_listing_price`
- Market timing: `median_days_on_market` ranges
- Geographic: `country` (though single value)

### Good for Grouping/Aggregation
- Market velocity ranges: `median_days_on_market` (45 unique values)
- Price ranges: All pricing columns
- Time-based grouping limited due to missing `month_date_yyyymm`

### Potential Join Keys
- `country` could join with other geographic datasets
- Missing temporal key limits time-series joins

### Data Quality Considerations
- **Systematic Missing Data**: 10.81% pattern suggests missing months/periods
- **Complete Temporal Loss**: `month_date_yyyymm` 100% null eliminates time-based analysis
- **Change Metrics Reliability**: mm/yy changes have same null pattern as temporal data
- **Quality Flag**: Present but minimal variance (single value 0.0)

## Keywords

real estate, housing market, inventory metrics, listing prices, market analysis, property data, housing statistics, market trends, price changes, days on market, pending sales, active listings, new listings, price per square foot, market velocity, housing supply, demand indicators, market health, property characteristics, real estate analytics

## Table and Column Documentation

**Table Comment**: Not provided

**Column Comments**: No column comments provided in the source data