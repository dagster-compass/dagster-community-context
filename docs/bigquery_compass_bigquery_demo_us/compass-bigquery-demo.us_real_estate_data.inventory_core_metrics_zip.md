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
# Summary: US Real Estate Inventory Core Metrics by ZIP Code

## Overall Dataset Characteristics

- **Total Rows**: 3,142,815 records
- **Data Quality**: Generally high quality with most core metrics having low null percentages (< 1%), though some derived metrics have higher null rates
- **Geographic Coverage**: 34,141 unique postal codes across the United States
- **Notable Patterns**: 
  - Many metrics include year-over-year (yy) and month-over-month (mm) change calculations
  - Negative values in change metrics likely represent percentage decreases
  - `month_date_yyyymm` column is completely null, suggesting temporal data may be implicit in the dataset structure

## Column Details

### Geographic Identifiers
- **postal_code** (INT64): Primary key, 0% null, 34,141 unique ZIP codes (range: 501-99929)
- **zip_name** (STRING): Location names, 2.30% null, 26,083 unique values (format: "city, state")

### Core Listing Metrics
- **total_listing_count** (FLOAT64): Current total listings, 0.10% null, ranges 0-2,860
- **active_listing_count** (FLOAT64): Active listings, 0.15% null, ranges 0-2,646  
- **new_listing_count** (FLOAT64): New listings, 0.10% null, ranges 0-802
- **pending_listing_count** (FLOAT64): Pending listings, 20.69% null, ranges 0-976

### Price Metrics
- **median_listing_price** (FLOAT64): Current median price, 0.25% null, ranges $1-$279M
- **average_listing_price** (FLOAT64): Current average price, 0.25% null, ranges $1-$279M
- **median_listing_price_per_square_foot** (FLOAT64): Price per sqft, 0.96% null, ranges $0-$795K

### Property Characteristics  
- **median_square_feet** (FLOAT64): Median property size, 0.95% null, ranges 1-12.5M sqft
- **median_days_on_market** (FLOAT64): Market time, 0.93% null, ranges 1-365 days

### Market Activity Metrics
- **pending_ratio** (FLOAT64): Pending/total ratio, 21.63% null, ranges 0-94.5%
- **price_reduced_count** (FLOAT64): Price reduction count, 0.10% null, ranges 0-628
- **price_increased_count** (FLOAT64): Price increase count, 0.10% null, ranges 0-268
- **price_reduced_share** (FLOAT64): % with price reductions, 0.46% null, ranges 0-4.0
- **price_increased_share** (FLOAT64): % with price increases, 0.46% null, ranges 0-4.0

### Change Metrics (Year-over-Year)
High null percentages (15-45%) suggest these are calculated only when historical data exists:
- **total_listing_count_yy** (15.86% null): YoY listing change
- **median_listing_price_yy** (16.67% null): YoY price change  
- **active_listing_count_yy** (17.31% null): YoY active listing change
- **new_listing_count_yy** (45.00% null): YoY new listing change
- **pending_listing_count_yy** (37.49% null): YoY pending change

### Change Metrics (Month-over-Month)
Moderate null percentages (12-55%):
- **total_listing_count_mm** (12.72% null): MoM listing change
- **median_listing_price_mm** (13.53% null): MoM price change
- **active_listing_count_mm** (13.94% null): MoM active change
- **new_listing_count_mm** (44.80% null): MoM new listing change

### Data Quality Indicator
- **quality_flag** (FLOAT64): Data quality indicator, 11.09% null, binary values (0.0/1.0)

### Missing Data
- **month_date_yyyymm** (STRING): Completely null (100%), likely indicates temporal dimension is handled elsewhere

## Query Considerations

### Good for Filtering
- **postal_code**: Primary geographic filter
- **zip_name**: Location-based searches  
- **quality_flag**: Data quality filtering
- **total_listing_count**: Market size filtering
- **median_listing_price**: Price range filtering

### Good for Grouping/Aggregation
- **postal_code**: Geographic aggregation
- **zip_name**: State/city level grouping (extract state from name)
- Market activity ranges (small/medium/large markets based on listing counts)
- Price tiers based on median_listing_price

### Potential Join Keys
- **postal_code**: Primary key for joining with other geographic datasets
- **zip_name**: Could join with demographic or economic data

### Data Quality Considerations
- Many year-over-year metrics have high null rates (15-45%) - filter by quality_flag or handle nulls appropriately
- Month-over-month metrics generally more complete (12-33% null)
- Price and size outliers exist (properties up to $279M, 12.5M sqft) - consider filtering extremes
- Negative values in change metrics represent decreases, not missing data
- Some metrics like price_reduced_share have theoretical max of 4.0, suggesting percentage calculations

## Keywords
real estate, housing market, ZIP code, postal code, listing prices, inventory metrics, market trends, property data, housing analytics, residential real estate, market statistics, price changes, days on market, listing activity

## Table and Column Documentation
**Table Comment**: Not provided
**Column Comments**: Not provided