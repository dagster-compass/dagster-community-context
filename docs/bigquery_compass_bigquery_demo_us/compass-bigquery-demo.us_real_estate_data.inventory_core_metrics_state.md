---
columns:
- active_listing_count (INT64)
- active_listing_count_mm (FLOAT64)
- active_listing_count_yy (FLOAT64)
- average_listing_price (FLOAT64)
- average_listing_price_mm (FLOAT64)
- average_listing_price_yy (FLOAT64)
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
- state (STRING)
- state_id (STRING)
- total_listing_count (INT64)
- total_listing_count_mm (FLOAT64)
- total_listing_count_yy (FLOAT64)
schema_hash: 36323ae9a667a5738e82100dbb5c34f146458c57608d7261989108d26ec763ee

---
# Table Analysis Summary: compass-bigquery-demo.us_real_estate_data.inventory_core_metrics_state

## Keywords
real estate, inventory, metrics, state, housing, listings, prices, market data, property, median, pending, active, new listings, price changes, days on market, square footage

## Overall Dataset Characteristics

- **Total Rows**: 5,661 records
- **Data Quality**: Generally good with consistent null patterns across year-over-year (yy) and month-over-month (mm) comparison columns
- **Coverage**: All 50 US states plus District of Columbia (51 unique states)
- **Time Series Nature**: Contains current values and comparative metrics (monthly and yearly changes)
- **Notable Issue**: `month_date_yyyymm` column is 100% null, indicating missing temporal dimension data

## Column Details

### Geographic Identifiers
- **state** (STRING): Full state names, no nulls, 51 unique values
- **state_id** (STRING): Two-letter state abbreviations, no nulls, 51 unique values
- Primary keys for geographic grouping and filtering

### Core Inventory Metrics
- **total_listing_count** (INT64): Active inventory counts, range 803-231,347, no nulls
- **active_listing_count** (INT64): Currently active listings, range 720-182,589, no nulls
- **new_listing_count** (INT64): New listings added, range 290-53,332, no nulls
- **pending_listing_count** (FLOAT64): Pending sales, range 0-82,071, 0.48% nulls

### Price Metrics
- **median_listing_price** (FLOAT64): $129,913-$886,500, no nulls, high variability
- **average_listing_price** (FLOAT64): $206,417-$1,730,505, no nulls
- **median_listing_price_per_square_foot** (FLOAT64): $79-$737/sqft, no nulls

### Property Characteristics
- **median_square_feet** (FLOAT64): 987-2,798 sqft, no nulls
- **median_days_on_market** (INT64): 13-157 days, no nulls, discrete values

### Market Activity Ratios
- **pending_ratio** (FLOAT64): 0.0-3.212, measures pending/active ratio, 0.48% nulls
- **price_reduced_share** (FLOAT64): 0.0254-0.4089, percentage of price reductions, no nulls
- **price_increased_share** (FLOAT64): 0.0-0.1302, percentage of price increases, no nulls

### Price Change Counts
- **price_reduced_count** (FLOAT64): 72-71,888 properties, no nulls
- **price_increased_count** (INT64): 0-9,466 properties, no nulls

### Temporal Comparison Columns (10.81-11.45% nulls)
All year-over-year (*_yy) and month-over-month (*_mm) columns show consistent null patterns around 10-11%, indicating these are calculated fields that may not be available for all time periods or states.

### Data Quality Indicator
- **quality_flag** (FLOAT64): Binary indicator (0.0/1.0), 10.81% nulls, appears to flag data quality issues

### Missing Data Column
- **month_date_yyyymm** (STRING): 100% null, temporal dimension data completely missing

## Table and Column Docs
No table comment or column comments are present in the provided analysis.

## Potential Query Considerations

### Good for Filtering
- `state` and `state_id`: Primary geographic filters
- `quality_flag`: Filter out potentially problematic data (when not null and = 0.0)
- Date ranges (when `month_date_yyyymm` is populated)

### Good for Grouping/Aggregation
- `state`/`state_id`: Geographic aggregation
- Market size categories (could derive from `total_listing_count`)
- Price tiers (could derive from `median_listing_price`)

### Potential Join Keys
- `state_id`: Standard for joining with other state-level datasets
- `state`: Alternative state identifier
- `month_date_yyyymm`: Time-based joins (when available)

### Data Quality Considerations
- **Null Handling**: Year-over-year and month-over-month columns have ~11% nulls - queries should handle appropriately
- **Quality Flag**: Consider filtering WHERE `quality_flag` = 0.0 or IS NULL for reliable data
- **Missing Temporal Data**: Current dataset lacks time dimension - cannot perform time-series analysis
- **Outlier Sensitivity**: Price and count metrics have wide ranges - consider using medians over averages for robust analysis
- **Ratio Calculations**: Some ratios may be extreme (pending_ratio up to 3.2) - validate calculations and consider capping