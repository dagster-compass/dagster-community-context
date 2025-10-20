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
# Dataset Summary: US Real Estate Inventory Core Metrics (Metro Level)

## Overall Dataset Characteristics

- **Total Rows**: 102,675
- **Geographic Coverage**: 925 unique metropolitan statistical areas (CBSA codes)
- **Data Quality**: High completeness for core metrics, with some planned missingness in month-over-month and year-over-year comparison fields
- **Time Series Nature**: Contains current values plus monthly (mm) and yearly (yy) percentage change calculations
- **Notable Patterns**: The `month_date_yyyymm` field is completely null, suggesting this may be a snapshot or the date information is stored elsewhere

## Column Details

### Geographic Identifiers
- **`cbsa_code`** (INT64): Core-based statistical area codes, range 10100-49820, no nulls, 925 unique metros
- **`cbsa_title`** (STRING): Metro area names (e.g., "Aberdeen, SD", "Akron, OH"), no nulls, 925 unique values
- **`householdrank`** (INT64): Ranking from 1-925, likely by household count or market size, no nulls

### Price Metrics
- **`median_listing_price`** (FLOAT64): Current median price ($19,900 to $5.5M), no nulls, 25,318 unique values
- **`median_listing_price_mm/yy`** (FLOAT64): Monthly/yearly % changes, 10.81% nulls, ranges ±50-500%
- **`average_listing_price`** (FLOAT64): Current average price ($44K to $23.5M), no nulls, highly granular
- **`average_listing_price_mm/yy`** (FLOAT64): Monthly/yearly % changes, 10.81% nulls

### Inventory Counts
- **`active_listing_count`** (INT64): Current active listings (0-69,796), no nulls
- **`new_listing_count`** (INT64): New listings (0-27,262), no nulls
- **`total_listing_count`** (INT64): Total listings (1-83,125), no nulls
- **`pending_listing_count`** (FLOAT64): Pending listings, 2.70% nulls (likely metros with no pending data)

### Market Dynamics
- **`median_days_on_market`** (FLOAT64): Time to sell (3-322 days), minimal nulls (0.01%)
- **`price_increased_count`** (INT64): Properties with price increases (0-4,978), no nulls
- **`price_reduced_count`** (FLOAT64): Properties with price reductions (0-22,456), no nulls
- **`price_increased_share/price_reduced_share`** (FLOAT64): Proportions of price changes, no nulls

### Property Characteristics
- **`median_listing_price_per_square_foot`** (FLOAT64): Price per sq ft ($22-$1,778), no nulls
- **`median_square_feet`** (FLOAT64): Property sizes (892-6,000 sq ft), no nulls

### Calculated Ratios
- **`pending_ratio`** (FLOAT64): Pending to active ratio (0-8.0), 2.70% nulls
- **`quality_flag`** (FLOAT64): Data quality indicator (0 or 1), 10.81% nulls

### Change Metrics Pattern
All `_mm` and `_yy` fields show ~10.81% nulls, suggesting these represent periods where comparison data wasn't available (likely the first month/year of data collection for newer metros).

## Query Considerations

### Good for Filtering
- **`cbsa_code`** and **`cbsa_title`**: Geographic filtering
- **`householdrank`**: Market size segmentation (1-50 for largest metros)
- **`quality_flag`**: Data quality filtering (0 = good quality)
- Price ranges on **`median_listing_price`** and **`average_listing_price`**

### Good for Grouping/Aggregation
- **`cbsa_code`** / **`cbsa_title`**: Geographic grouping
- **`householdrank`** ranges: Market size tiers
- Calculated fields like **`price_increased_share`** and **`price_reduced_share`**: Market condition analysis

### Potential Join Keys
- **`cbsa_code`**: Primary key for joining with other metro-level datasets
- **`cbsa_title`**: Human-readable identifier for geographic joins

### Data Quality Considerations
- **Missing Month/Year Data**: ~10.81% null rate for all comparison fields suggests newer markets or data gaps
- **Pending Data**: 2.70% null rate may indicate markets where pending sales aren't tracked
- **Quality Flag**: Use `quality_flag = 0` for highest quality data
- **Extreme Values**: Some very high prices and counts may need outlier handling
- **Date Field**: `month_date_yyyymm` is completely null - date context must come from elsewhere

## Keywords
real estate, housing market, inventory metrics, CBSA, metropolitan areas, listing prices, days on market, price changes, housing supply, market dynamics, pending sales, price per square foot, home sizes

## Table and Column Documentation
No table comment or column comments are present in the provided analysis.