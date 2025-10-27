---
columns:
- active_listing_count (FLOAT64)
- active_listing_count_mm (FLOAT64)
- active_listing_count_yy (FLOAT64)
- average_listing_price (FLOAT64)
- average_listing_price_mm (FLOAT64)
- average_listing_price_yy (FLOAT64)
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
- postal_code (INT64)
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
- zip_name (STRING)
schema_hash: 298de63c9f54c4d2298f4427674befa32a437912cf25f7841e703aa50148138b

---
# Table Analysis Summary: compass-bigquery-demo.us_real_estate_data.inventory_core_metrics_zip

## Overall Dataset Characteristics

**Total Rows:** 3,142,815

**General Data Quality:** The dataset has significant data quality challenges with high null percentages across many columns (ranging from 0.10% to 100%). Notable issues include:
- The `month_date_yyyymm` column is completely null (100%)
- Many year-over-year (yy) and month-over-month (mm) comparison columns have high null rates (15-90%)
- Several price-related metrics have substantial missing data

**Notable Patterns:**
- Many columns contain negative values close to -1.0 (e.g., -0.9999, -0.9998), likely indicating missing or invalid data points
- Year-over-year and month-over-month columns show percentage changes, with values typically ranging from -1.0 to positive percentages
- The dataset appears to track real estate inventory metrics at the ZIP code level over time

## Column Details

### Geographic Identifiers
- **postal_code (INT64):** Complete data (0% null), 34,141 unique ZIP codes ranging from 501 to 99929
- **zip_name (STRING):** 2.30% null, 26,083 unique location names in "city, state" format

### Core Listing Metrics
- **total_listing_count (FLOAT64):** Nearly complete (0.10% null), ranges 0-2,860, good for aggregation
- **active_listing_count (FLOAT64):** Nearly complete (0.15% null), ranges 0-2,646
- **new_listing_count (FLOAT64):** Nearly complete (0.10% null), ranges 0-802
- **pending_listing_count (FLOAT64):** 20.69% null, ranges 0-976

### Price Metrics
- **average_listing_price (FLOAT64):** Nearly complete (0.25% null), wide range $1-$279M
- **median_listing_price (FLOAT64):** Nearly complete (0.25% null), wide range $1-$279M
- **median_listing_price_per_square_foot (FLOAT64):** Nearly complete (0.96% null), ranges $0-$795K

### Property Characteristics
- **median_square_feet (FLOAT64):** Nearly complete (0.95% null), ranges 1-12.5M sq ft
- **median_days_on_market (FLOAT64):** Nearly complete (0.93% null), ranges 1-365 days

### Market Activity Ratios
- **pending_ratio (FLOAT64):** 21.63% null, ranges 0-94.5
- **price_reduced_share (FLOAT64):** Nearly complete (0.46% null), ranges 0-4.0
- **price_increased_share (FLOAT64):** Nearly complete (0.46% null), ranges 0-4.0

### Change Metrics (Month-over-Month)
Most "_mm" columns have 12-55% null values and contain percentage changes (typically -1.0 to positive values)

### Change Metrics (Year-over-Year)
"_yy" columns have 15-90% null values, representing annual percentage changes

### Data Quality Indicator
- **quality_flag (FLOAT64):** 11.09% null, binary values (0.0, 1.0) indicating data quality

### Problematic Columns
- **month_date_yyyymm (STRING):** Completely null (100%), unusable
- Various price count columns have 54-90% null values

## Query Considerations

### Excellent for Filtering
- `postal_code`: Complete, numeric, ideal for geographic filtering
- `zip_name`: Good for location-based queries (minor nulls)
- `quality_flag`: Good for filtering reliable data

### Good for Grouping/Aggregation
- Geographic: `postal_code`, `zip_name`
- Core metrics: `total_listing_count`, `active_listing_count`, `median_listing_price`
- Time-based analysis using change metrics (where data exists)

### Potential Join Keys
- `postal_code`: Primary key for joining with other geographic datasets
- `zip_name`: Alternative join key for location-based data

### Data Quality Considerations
1. **High Null Rates:** Many analytical columns have substantial missing data
2. **Negative Sentinel Values:** Values near -1.0 likely represent missing/invalid data
3. **Wide Value Ranges:** Price columns have extreme outliers that may need filtering
4. **Temporal Data Issues:** The date column is completely unusable
5. **Change Metrics Reliability:** Year-over-year and month-over-month calculations have high null rates

### Recommended Query Patterns
- Filter by `quality_flag = 1.0` for reliable data
- Use core listing and price columns for primary analysis
- Be cautious with change metrics due to high null rates
- Consider geographic aggregation using `postal_code` or `zip_name`

## Keywords
real estate, inventory, listings, ZIP code, housing market, property prices, market metrics, days on market, pending ratio, price changes, geographic analysis, monthly data, annual changes, data quality

## Table and Column Documentation
No table comment or column comments were provided in the source data.