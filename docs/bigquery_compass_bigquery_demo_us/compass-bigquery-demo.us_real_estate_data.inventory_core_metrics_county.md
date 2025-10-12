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
- **Data Coverage**: County-level real estate inventory metrics across the United States
- **Geographic Scope**: 3,135 unique counties represented by county names and 3,141 unique FIPS codes
- **Data Quality**: Generally high quality with most columns having very low null percentages (<1%), though some derivative metrics have higher null rates (10-20%)
- **Notable Issues**: The `month_date_yyyymm` column is completely null (100%), indicating missing temporal dimension data

## Column Details

### Geographic Identifiers
- **county_name** (STRING): County names with state abbreviations (e.g., "fayette, ga") - No nulls, 3,135 unique values
- **county_fips** (INT64): Federal Information Processing Standards county codes - No nulls, range 1001-56045, 3,141 unique values

### Temporal Dimension
- **month_date_yyyymm** (STRING): Completely null - intended to store year-month data but unusable in current state

### Core Pricing Metrics
- **median_listing_price** (FLOAT64): Median home listing prices ranging $1,311-$13M, minimal nulls (0.02%)
- **average_listing_price** (FLOAT64): Average listing prices with wide range ($5K-$142M), minimal nulls (0.02%)
- **median_listing_price_per_square_foot** (FLOAT64): Price per sq ft ($0-$56,250), minimal nulls (0.10%)

### Inventory Counts
- **active_listing_count** (FLOAT64): Current active listings (0-23,258), minimal nulls (0.01%)
- **new_listing_count** (FLOAT64): New listings in period (0-9,888), minimal nulls (0.01%)
- **total_listing_count** (FLOAT64): Total listings (0-33,580), minimal nulls (0.01%)
- **pending_listing_count** (FLOAT64): Pending sales (0-14,211), moderate nulls (7.28%)

### Market Activity Metrics
- **median_days_on_market** (FLOAT64): Time to sell (1-365 days), minimal nulls (0.11%)
- **price_increased_count** (FLOAT64): Properties with price increases (0-1,666), minimal nulls (0.01%)
- **price_reduced_count** (FLOAT64): Properties with price reductions (0-12,596), minimal nulls (0.01%)

### Property Characteristics
- **median_square_feet** (FLOAT64): Median home size (4-30,902 sq ft), minimal nulls (0.10%)

### Derived Ratios and Shares
- **price_increased_share** (FLOAT64): Proportion of listings with price increases (0-4.0), minimal nulls (0.04%)
- **price_reduced_share** (FLOAT64): Proportion of listings with price reductions (0-4.0), minimal nulls (0.04%)
- **pending_ratio** (FLOAT64): Pending to active listing ratio (0-11.5), moderate nulls (7.32%)

### Period-over-Period Changes
Most metrics include month-over-month (mm) and year-over-year (yy) percentage changes:
- **_mm columns**: Month-over-month changes, typically 10-20% null rates
- **_yy columns**: Year-over-year changes, typically 11-20% null rates
- Changes expressed as decimal percentages (e.g., 0.05 = 5% increase, -0.10 = 10% decrease)

### Data Quality Indicator
- **quality_flag** (FLOAT64): Binary flag (0.0 or 1.0) with 10.72% nulls, likely indicating data reliability

## Potential Query Considerations

### Good for Filtering
- **county_fips**: Precise geographic filtering
- **county_name**: Human-readable geographic filtering
- **quality_flag**: Data quality filtering
- **median_listing_price**: Price range filtering
- **active_listing_count**: Market size filtering

### Good for Grouping/Aggregation
- **county_name/county_fips**: Geographic aggregation
- Price ranges (created from **median_listing_price**)
- Market size tiers (created from **active_listing_count**)

### Potential Join Keys
- **county_fips**: Primary key for joining with other county-level datasets
- **county_name**: Alternative join key (less reliable due to formatting)

### Data Quality Considerations
- **month_date_yyyymm** is completely unusable - temporal analysis not possible with this column
- Period-over-period metrics have significant null rates (10-20%) - consider filtering or handling nulls
- **quality_flag** should be considered for data reliability filtering
- Very wide ranges in price metrics suggest potential outliers
- Some counties may have very small sample sizes affecting metric reliability

### Keywords
real estate, housing, inventory, county, FIPS, listing prices, market metrics, days on market, pending sales, price changes, square footage, geographic analysis, housing market trends

### Table and Column Documentation
No table comment or column comments are provided in the source data.