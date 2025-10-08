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

- **Total Rows**: 111
- **Data Quality**: Generally good data quality with consistent null patterns (10.81% nulls for derived metrics, 0% nulls for base counts and prices)
- **Geographic Scope**: Country-level data exclusively for the United States
- **Time Series Nature**: Contains month-over-month (mm) and year-over-year (yy) percentage change metrics
- **Data Completeness**: One column (`month_date_yyyymm`) is entirely null (100%), suggesting it may be unused or deprecated

## Column Details

### Base Count Metrics (No Nulls)
- **total_listing_count** (INT64): Total property listings (815K-1.87M range)
- **pending_listing_count** (INT64): Properties under contract (257K-659K range) 
- **active_listing_count** (INT64): Currently available listings (346K-1.46M range)
- **new_listing_count** (INT64): New market entries (215K-584K range)
- **price_increased_count** (INT64): Properties with price increases (12K-61K range)
- **price_reduced_count** (FLOAT64): Properties with price reductions (64K-458K range)

### Price and Property Metrics (No Nulls)
- **average_listing_price** (FLOAT64): Mean listing price ($439K-$791K range)
- **median_listing_price** (FLOAT64): Median listing price ($249K-$449K range)
- **median_listing_price_per_square_foot** (FLOAT64): Price per sq ft ($125-$234 range)
- **median_square_feet** (FLOAT64): Property sizes (1,776-1,997 sq ft range)
- **median_days_on_market** (INT64): Time to sell (30-88 days range)

### Market Share Metrics (No Nulls)
- **price_reduced_share** (FLOAT64): Proportion of price reductions (5.37%-21.68%)
- **price_increased_share** (FLOAT64): Proportion of price increases (0.86%-3.47%)
- **pending_ratio** (FLOAT64): Pending to total listing ratio (0.23-1.48)

### Change Metrics (10.81% Nulls)
All month-over-month (mm) and year-over-year (yy) percentage change columns have consistent null patterns:
- Price change metrics (average_listing_price_mm/yy, median_listing_price_mm/yy)
- Count change metrics (total_listing_count_mm/yy, pending_listing_count_mm/yy, etc.)
- Market metrics changes (pending_ratio_mm/yy, price_reduced_share_mm/yy, etc.)
- Property characteristic changes (median_square_feet_mm/yy, median_days_on_market_mm/yy)

### Metadata Columns
- **country** (STRING): Geographic identifier (always "United States")
- **quality_flag** (FLOAT64): Data quality indicator (always 0.0 when present)
- **month_date_yyyymm** (STRING): Time identifier (100% null - potentially unused)

## Query Considerations

### Filtering Opportunities
- **country**: Single value filter (United States only)
- **quality_flag**: Data quality filtering (though values appear consistent)
- **Date ranges**: Would require time-based filtering if month_date_yyyymm were populated
- **Null handling**: 10.81% of rows lack change metrics, important for trend analysis

### Aggregation Potential
- **Time-based grouping**: Limited without populated date column
- **Market segment analysis**: Could group by price ranges, property sizes, or market activity levels
- **Regional analysis**: Not possible at country level (single value)

### Join Considerations
- **Primary key**: No obvious single primary key; likely time-series data
- **Geographic joins**: Country field could join to other geographic datasets
- **Time-based joins**: Limited without proper date column

### Data Quality Considerations
- **Consistent null patterns**: 10.81% null rate suggests systematic data collection gaps
- **Price validation**: Wide price ranges may indicate different market segments or time periods
- **Change metric reliability**: Null values in change metrics may indicate calculation limitations
- **Temporal consistency**: Missing date column limits time-series analysis capabilities

## Keywords
real estate, housing market, property listings, inventory metrics, price trends, market analysis, United States housing, property values, days on market, listing counts, pending sales, price changes, square footage, market share, time series

## Table and Column Documentation
No table comment or column comments were provided in the source data.