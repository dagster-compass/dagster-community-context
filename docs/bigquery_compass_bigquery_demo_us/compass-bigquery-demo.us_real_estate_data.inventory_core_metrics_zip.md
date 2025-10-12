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
# Dataset Summary: US Real Estate Inventory Core Metrics by ZIP Code

## Keywords
real estate data, inventory metrics, ZIP code analysis, housing market, listing prices, property metrics, market trends, real estate analytics, housing inventory, property listings

## Overall Dataset Characteristics

- **Total Rows**: 3,142,815 records
- **Geographic Granularity**: ZIP code level data with 34,141 unique postal codes and 26,083 unique ZIP names
- **Data Quality**: Generally good with most core metrics having low null rates (0.1-1%), though some derived metrics have higher null rates (13-90%)
- **Temporal Nature**: Contains year-over-year (yy) and month-over-month (mm) comparison metrics alongside current values
- **Notable Issue**: The `month_date_yyyymm` column is 100% null, indicating missing temporal identification

## Column Analysis by Category

### Core Listing Counts and Activity
- **total_listing_count** (FLOAT64): Current total listings (0.1% nulls, range 0-2,860)
- **active_listing_count** (FLOAT64): Currently active listings (0.15% nulls, range 0-2,646)
- **new_listing_count** (FLOAT64): New listings in period (0.1% nulls, range 0-802)
- **pending_listing_count** (FLOAT64): Pending sales (20.69% nulls, range 0-976)

### Price Metrics
- **average_listing_price** (FLOAT64): Mean listing price (0.25% nulls, range $1-$279M)
- **median_listing_price** (FLOAT64): Median listing price (0.25% nulls, range $1-$279M)
- **median_listing_price_per_square_foot** (FLOAT64): Price per sq ft (0.96% nulls, range $0-$795K)

### Property Characteristics
- **median_square_feet** (FLOAT64): Median property size (0.95% nulls, range 1-12.5M sq ft)
- **median_days_on_market** (FLOAT64): Time to sale/pending (0.93% nulls, range 1-365 days)

### Market Activity Ratios
- **pending_ratio** (FLOAT64): Pending/total ratio (21.63% nulls, range 0-94.5%)
- **price_increased_share** (FLOAT64): Share with price increases (0.46% nulls, range 0-4.0)
- **price_reduced_share** (FLOAT64): Share with price reductions (0.46% nulls, range 0-4.0)

### Price Change Counts
- **price_increased_count** (FLOAT64): Count of price increases (0.1% nulls, range 0-268)
- **price_reduced_count** (FLOAT64): Count of price reductions (0.1% nulls, range 0-628)

### Temporal Comparisons (Higher Null Rates)
- **Year-over-Year metrics (_yy suffix)**: 15-90% null rates, indicating sparse historical data
- **Month-over-Month metrics (_mm suffix)**: 12-90% null rates
- Values often range from -1.0 to positive numbers, with -1.0 likely indicating no prior period data

### Geographic Identifiers
- **postal_code** (INT64): ZIP codes (0% nulls, 34,141 unique values, range 501-99929)
- **zip_name** (STRING): City, state format (2.3% nulls, 26,083 unique values)

### Data Quality
- **quality_flag** (FLOAT64): Binary quality indicator (11.09% nulls, values 0.0 or 1.0)

## Query Considerations

### Good for Filtering
- **postal_code**: Primary geographic filter with complete data
- **quality_flag**: Filter for data quality when not null
- Core listing counts and price metrics (low null rates)

### Good for Grouping/Aggregation
- **postal_code**: Geographic aggregation
- **zip_name**: State-level analysis (extract state from city, state format)
- Price ranges and market segments

### Potential Join Keys
- **postal_code**: Primary key for joining with other geographic datasets
- **zip_name**: Secondary geographic identifier

### Data Quality Considerations
1. **Missing temporal identifier**: `month_date_yyyymm` is completely null
2. **High null rates in derived metrics**: Year-over-year and month-over-month comparisons have 13-90% null rates
3. **Extreme values**: Some metrics show very high maximums that may be outliers
4. **Negative values in comparison metrics**: -1.0 values likely indicate missing baseline data
5. **Price increase/decrease counts**: Very high null rates (89-90%) limit usefulness

### Recommended Query Patterns
- Filter by `quality_flag = 1.0` for higher quality data
- Use core metrics (listing counts, prices, square footage) for reliable analysis
- Be cautious with temporal comparison metrics due to high null rates
- Consider geographic aggregation by state (extracting from zip_name)

## Table and Column Docs
No table comment or column comments were provided in the source data.