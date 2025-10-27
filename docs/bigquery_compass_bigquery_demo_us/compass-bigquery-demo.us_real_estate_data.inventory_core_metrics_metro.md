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
# Table Summary: inventory_core_metrics_metro

## Overall Dataset Characteristics

- **Total Rows**: 102,675
- **Data Quality**: The dataset has significant data quality issues with the `month_date_yyyymm` column being 100% null, indicating missing temporal information. Additionally, many month-over-month and year-over-year comparison metrics have ~10-11% null values, likely representing the first month/year of data for each metro area.
- **Geographic Coverage**: Contains data for 925 unique metropolitan statistical areas (CBSAs) across the United States
- **Data Structure**: Appears to be real estate inventory metrics aggregated at the metro level, with both absolute values and percentage change metrics

## Column Details

### Geographic and Ranking Columns
- **`cbsa_title`** (STRING): Metropolitan area names (0% null, 925 unique values)
  - Examples: "Walla Walla, WA", "Ketchikan, AK", "Jacksonville, TX"
- **`cbsa_code`** (INT64): CBSA identification codes (0% null, 925 unique values, range: 10100-49820)
- **`householdrank`** (INT64): Ranking metric for metros (0% null, 925 unique values, range: 1-925)

### Temporal Column (Data Quality Issue)
- **`month_date_yyyymm`** (STRING): **100% null - major data quality issue**
  - This appears intended to store month/year information but contains no data

### Price Metrics
- **`median_listing_price`** (FLOAT64): Core price metric (0% null, range: $19,900 - $5,508,750)
- **`median_listing_price_mm`** (FLOAT64): Month-over-month price change (10.81% null, range: -55% to +298%)
- **`median_listing_price_yy`** (FLOAT64): Year-over-year price change (10.81% null, range: -78% to +498%)
- **`median_listing_price_per_square_foot`** (FLOAT64): Price per sq ft (0% null, range: $22-$1,778)
- **`average_listing_price`** (FLOAT64): Mean price (0% null, range: $44,444 - $23,524,874)

### Inventory Metrics
- **`active_listing_count`** (INT64): Current active listings (0% null, range: 0-69,796)
- **`new_listing_count`** (INT64): New listings added (0% null, range: 0-27,262)
- **`total_listing_count`** (INT64): Total listings (0% null, range: 1-83,125)
- **`pending_listing_count`** (FLOAT64): Pending sales (2.70% null, range: 0-28,578)

### Market Activity Metrics
- **`median_days_on_market`** (FLOAT64): Days listings stay active (0.01% null, range: 3-322 days)
- **`price_increased_count`** (INT64): Listings with price increases (0% null, range: 0-4,978)
- **`price_reduced_count`** (FLOAT64): Listings with price reductions (0% null, range: 0-22,456)
- **`pending_ratio`** (FLOAT64): Ratio of pending to active listings (2.70% null, range: 0-8.01)

### Share/Percentage Metrics
- **`price_increased_share`** (FLOAT64): % of listings with price increases (0% null, range: 0-38.15%)
- **`price_reduced_share`** (FLOAT64): % of listings with price reductions (0% null, range: 0-66.67%)

### Property Characteristics
- **`median_square_feet`** (FLOAT64): Median home size (0% null, range: 892-6,000 sq ft)

### Data Quality Flag
- **`quality_flag`** (FLOAT64): Data quality indicator (10.81% null, values: 0.0 or 1.0)

### Change Metrics Pattern
Most metrics have corresponding `_mm` (month-over-month) and `_yy` (year-over-year) change columns with ~10-11% null values, indicating these represent percentage changes that cannot be calculated for initial time periods.

## Query Considerations

### Good for Filtering
- `cbsa_title` and `cbsa_code` for geographic filtering
- `householdrank` for metro size filtering
- `quality_flag` for data quality filtering
- Price and inventory ranges for market segment analysis

### Good for Grouping/Aggregation
- Geographic grouping by `cbsa_title` or `cbsa_code`
- Market size grouping by `householdrank` ranges
- Quality-based grouping using `quality_flag`

### Potential Join Keys
- `cbsa_code` - standard identifier for joining with other metro-level datasets
- `cbsa_title` - human-readable metro identifier

### Data Quality Considerations
- **Critical Issue**: `month_date_yyyymm` is completely null - temporal analysis not possible without external date context
- ~10-11% null values in change metrics likely represent first-period observations
- High null percentages (54-55%) in price increase count change metrics suggest data sparsity
- 2.70% nulls in pending metrics may indicate reporting gaps
- `quality_flag` should be considered when filtering for reliable data

### Recommended Query Patterns
- Filter by `quality_flag = 1.0` or exclude nulls for higher quality data
- Use absolute metrics (without `_mm` or `_yy` suffixes) for cross-sectional analysis
- Be cautious with time-series analysis due to missing date information
- Consider `householdrank` for market size stratification

## Keywords
real estate, housing market, inventory, metro areas, CBSA, listing prices, market metrics, days on market, pending sales, price changes, square footage, metropolitan statistical areas, housing data, real estate analytics

## Table and Column Documentation
No table comment or column comments are present in the provided schema information.