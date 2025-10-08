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
# Table Summary: compass-bigquery-demo.us_real_estate_data.inventory_core_metrics_metro

## Overall Dataset Characteristics

- **Total Rows**: 102,675
- **Data Quality**: The dataset has significant data quality issues with the primary date field (`month_date_yyyymm`) being 100% null, making temporal analysis challenging
- **Notable Patterns**: 
  - Approximately 10.81% null values in most month-over-month and year-over-year comparison fields
  - Higher null percentages (50%+) in price increase metrics
  - Contains real estate inventory metrics for 925 unique metro areas (CBSAs)
- **Distribution**: Data appears to cover a comprehensive range of US metropolitan areas with varying market sizes and characteristics

## Column Details

### Geographic and Temporal Identifiers
- **`month_date_yyyymm` (STRING)**: Completely null (100%), making temporal filtering impossible
- **`cbsa_code` (INT64)**: Core-Based Statistical Area codes (10100-49820), no nulls, 925 unique values - primary geographic identifier
- **`cbsa_title` (STRING)**: Metropolitan area names, no nulls, 925 unique values - human-readable geographic identifier
- **`householdrank` (INT64)**: Metro area ranking by households (1-925), no nulls - useful for market size analysis

### Pricing Metrics
- **`median_listing_price` (FLOAT64)**: Current median price ($19,900-$5.5M), no nulls
- **`median_listing_price_mm` (FLOAT64)**: Month-over-month price change (-55% to +299%), 10.81% nulls
- **`median_listing_price_yy` (FLOAT64)**: Year-over-year price change (-78% to +498%), 10.81% nulls
- **`median_listing_price_per_square_foot` (FLOAT64)**: Price per sq ft ($22-$1,778), no nulls
- **`median_listing_price_per_square_foot_mm/yy` (FLOAT64)**: Respective change metrics, 10.81% nulls
- **`average_listing_price` (FLOAT64)**: Mean listing price ($44K-$23.5M), no nulls
- **`average_listing_price_mm/yy` (FLOAT64)**: Respective change metrics, 10.81% nulls

### Inventory Counts
- **`active_listing_count` (INT64)**: Current active listings (0-69,796), no nulls
- **`active_listing_count_mm/yy` (FLOAT64)**: Change metrics, 10.81% nulls
- **`new_listing_count` (INT64)**: New listings (0-27,262), no nulls
- **`new_listing_count_mm/yy` (FLOAT64)**: Change metrics, ~11% nulls
- **`total_listing_count` (INT64)**: Total listings (1-83,125), no nulls
- **`total_listing_count_mm/yy` (FLOAT64)**: Change metrics, 10.81% nulls

### Market Activity Metrics
- **`median_days_on_market` (FLOAT64)**: Days on market (3-322), minimal nulls (0.01%)
- **`median_days_on_market_mm/yy` (FLOAT64)**: Change metrics, ~10.8% nulls
- **`pending_listing_count` (FLOAT64)**: Pending sales (0-28,578), 2.70% nulls
- **`pending_listing_count_mm/yy` (FLOAT64)**: Change metrics, 13-14% nulls
- **`pending_ratio` (FLOAT64)**: Pending to active ratio (0-8.0), 2.70% nulls
- **`pending_ratio_mm/yy` (FLOAT64)**: Change metrics, 13-14% nulls

### Price Change Behavior
- **`price_increased_count` (INT64)**: Listings with price increases (0-4,978), no nulls
- **`price_increased_count_mm/yy` (FLOAT64)**: Change metrics, 54-55% nulls (high missingness)
- **`price_increased_share` (FLOAT64)**: Share of listings with price increases (0-38%), no nulls
- **`price_increased_share_mm/yy` (FLOAT64)**: Change metrics, 10.81% nulls
- **`price_reduced_count` (FLOAT64)**: Listings with price reductions (0-22,456), no nulls
- **`price_reduced_count_mm/yy` (FLOAT64)**: Change metrics, ~11.5% nulls
- **`price_reduced_share` (FLOAT64)**: Share of listings with price reductions (0-67%), no nulls
- **`price_reduced_share_mm/yy` (FLOAT64)**: Change metrics, 10.81% nulls

### Property Characteristics
- **`median_square_feet` (FLOAT64)**: Median home size (892-6,000 sq ft), no nulls
- **`median_square_feet_mm/yy` (FLOAT64)**: Change metrics, 10.81% nulls

### Data Quality
- **`quality_flag` (FLOAT64)**: Binary quality indicator (0.0 or 1.0), 10.81% nulls

## Query Considerations

### Filtering Columns
- **`cbsa_code`** and **`cbsa_title`**: Primary geographic filters
- **`householdrank`**: Market size filtering (top/bottom markets)
- **`quality_flag`**: Data quality filtering when not null
- Price ranges using **`median_listing_price`** or **`average_listing_price`**

### Grouping/Aggregation Opportunities
- **Geographic analysis**: Group by `cbsa_title` or `cbsa_code`
- **Market size analysis**: Group by `householdrank` ranges
- **Price tier analysis**: Create buckets from `median_listing_price`
- **Regional patterns**: Extract state/region from `cbsa_title`

### Potential Join Keys
- **`cbsa_code`**: Standard identifier for joining with other CBSA-level datasets
- **`cbsa_title`**: Human-readable identifier for geographic matching

### Data Quality Considerations
- **Critical Issue**: `month_date_yyyymm` is completely null, preventing time series analysis
- **Missing Data**: ~10.81% nulls in most comparative metrics (_mm, _yy fields)
- **High Missingness**: Price increase count changes have 50%+ null rates
- **Data Validation**: Use `quality_flag` to filter for reliable records when available
- **Outliers**: Extreme values in price ranges and percentage changes should be validated

## Keywords
real estate, housing market, inventory metrics, CBSA, metropolitan areas, listing prices, market activity, days on market, pending sales, price changes, square footage, housing supply, market trends

## Table and Column Docs
No table comment or column comments are present in this dataset.