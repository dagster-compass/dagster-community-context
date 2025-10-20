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
# Table Summary: compass-bigquery-demo.us_real_estate_data.inventory_core_metrics_county

## Overall Dataset Characteristics

- **Total Rows**: 344,538 records
- **Data Quality**: Generally good with most columns having very low null percentages (0-1%), though some month-over-month and year-over-year columns have higher null rates (10-25%)
- **Geographic Coverage**: Covers 3,141 counties across the United States (based on FIPS codes)
- **Time Series Nature**: Contains comparative metrics with month-over-month (mm) and year-over-year (yy) calculations
- **Notable Issues**: The `month_date_yyyymm` column is completely null (100%), indicating missing temporal reference data

## Column Details

### Geographic Identifiers
- **county_fips** (INT64): County FIPS codes ranging from 1001 to 56045, no nulls, 3,141 unique values
- **county_name** (STRING): County names with state abbreviations (e.g., "cass, nd"), no nulls, 3,135 unique values

### Core Pricing Metrics
- **median_listing_price** (FLOAT64): Property prices from $1,311 to $13M, minimal nulls (0.02%)
- **average_listing_price** (FLOAT64): Average prices from $5K to $142M, minimal nulls (0.02%)
- **median_listing_price_per_square_foot** (FLOAT64): Price per sqft from $0 to $56,250, minimal nulls (0.10%)

### Inventory Metrics
- **active_listing_count** (FLOAT64): Active listings from 0 to 23,258, minimal nulls (0.01%)
- **new_listing_count** (FLOAT64): New listings from 0 to 9,888, minimal nulls (0.01%)
- **pending_listing_count** (FLOAT64): Pending sales from 0 to 14,211, moderate nulls (7.28%)
- **total_listing_count** (FLOAT64): Total listings from 0 to 33,580, minimal nulls (0.01%)

### Market Timing Metrics
- **median_days_on_market** (FLOAT64): Days on market from 1 to 365, minimal nulls (0.11%)
- **pending_ratio** (FLOAT64): Ratio of pending to active listings from 0 to 11.5, moderate nulls (7.32%)

### Price Change Metrics
- **price_increased_count** (FLOAT64): Count of price increases, minimal nulls (0.01%)
- **price_reduced_count** (FLOAT64): Count of price reductions, minimal nulls (0.01%)
- **price_increased_share** (FLOAT64): Share of listings with price increases (0-4.0), minimal nulls (0.04%)
- **price_reduced_share** (FLOAT64): Share of listings with price reductions (0-4.0), minimal nulls (0.04%)

### Property Characteristics
- **median_square_feet** (FLOAT64): Property sizes from 4 to 30,902 sqft, minimal nulls (0.10%)

### Comparative Metrics (Month-over-Month)
All `_mm` suffixed columns show month-over-month changes with higher null rates (10-25%):
- Values typically range from -1.0 to positive values indicating percentage changes
- Negative values suggest decreases, positive values suggest increases

### Comparative Metrics (Year-over-Year)
All `_yy` suffixed columns show year-over-year changes with similar null patterns to mm columns:
- Generally wider ranges than mm columns, reflecting longer-term trends

### Quality Indicator
- **quality_flag** (FLOAT64): Binary flag (0.0 or 1.0) with 10.72% nulls, likely indicating data quality issues

## Query Considerations

### Good for Filtering
- `county_fips` and `county_name`: Geographic filtering
- `quality_flag`: Data quality filtering
- Price ranges on `median_listing_price` and `average_listing_price`
- `active_listing_count` for market activity levels

### Good for Grouping/Aggregation
- `county_fips` and `county_name`: Geographic grouping
- Price tiers based on `median_listing_price`
- Market size categories based on `total_listing_count`

### Potential Join Keys
- `county_fips`: Standard geographic identifier for joining with other county-level datasets
- `county_name`: Alternative geographic join key (though less reliable due to formatting)

### Data Quality Considerations
- **Missing temporal data**: `month_date_yyyymm` is completely null, limiting time-based analysis
- **Moderate nulls**: Pending listing metrics and comparative metrics have 7-25% null rates
- **Extreme values**: Some outliers in pricing data (e.g., $142M average price) may need investigation
- **Price change metrics**: High null percentages (70%+) in some price change count metrics suggest data sparsity

## Keywords
real estate, housing, inventory, county, FIPS, median price, listing count, days on market, price changes, pending sales, square footage, market metrics, geographic data, time series, month-over-month, year-over-year

## Table and Column Documentation
No table comment or column comments were provided in the source data.