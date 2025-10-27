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
# US Real Estate Data - County Inventory Core Metrics

## Overall Dataset Characteristics

- **Total Rows**: 344,538 records
- **Geographic Coverage**: County-level real estate data across the United States
- **Data Quality**: Generally high quality with most columns having very low null percentages (0.01-0.11%), though some derivative metrics have higher null rates (10-75%)
- **Time Series Nature**: Contains month-over-month (mm) and year-over-year (yy) change metrics
- **Notable Issues**: The `month_date_yyyymm` column is 100% null, indicating missing temporal identifiers

## Column Details

### Geographic Identifiers
- **county_name** (STRING): County names with state abbreviations (e.g., "abbeville, sc"). No nulls, 3,135 unique values covering US counties
- **county_fips** (INT64): Federal Information Processing Standards county codes. No nulls, 3,141 unique values ranging from 1001 to 56045

### Pricing Metrics
- **median_listing_price** (FLOAT64): Primary price metric ranging from $1,311 to $13M. Virtually no nulls (0.02%)
- **median_listing_price_mm/yy** (FLOAT64): Month-over-month and year-over-year price changes. ~11% nulls, ranges from -99% to +570% (mm) and -99% to +222% (yy)
- **median_listing_price_per_square_foot** (FLOAT64): Price per sq ft from $0 to $56,250. Minimal nulls (0.10%)
- **average_listing_price** (FLOAT64): Mean prices ranging from $5K to $142M. Very low nulls (0.02%)

### Inventory Metrics
- **active_listing_count** (FLOAT64): Current inventory from 0 to 23,258 listings. Virtually no nulls
- **new_listing_count** (FLOAT64): New listings from 0 to 9,888. Higher null rate (19%) for change metrics
- **total_listing_count** (FLOAT64): Total listings from 0 to 33,580. Low nulls (0.01%)
- **pending_listing_count** (FLOAT64): Pending sales from 0 to 14,211. Moderate nulls (7.28%)

### Market Activity Metrics
- **median_days_on_market** (FLOAT64): Time to sale from 1 to 365 days. Minimal nulls (0.11%)
- **price_increased/reduced_count** (FLOAT64): Count of price changes. High null rates for change metrics (70%+)
- **price_increased/reduced_share** (FLOAT64): Proportion of listings with price changes (0.0 to 4.0)
- **pending_ratio** (FLOAT64): Ratio of pending to active listings (0.0 to 11.5). Moderate nulls (7.32%)

### Property Characteristics
- **median_square_feet** (FLOAT64): Property sizes from 4 to 30,902 sq ft. Minimal nulls (0.10%)

### Data Quality
- **quality_flag** (FLOAT64): Binary quality indicator (0.0 or 1.0). Moderate nulls (10.72%)

## Query Considerations

### Filtering Columns
- **county_name**: Excellent for geographic filtering
- **county_fips**: Precise geographic identification
- **quality_flag**: Filter for data quality (when not null)
- **median_listing_price**: Price range filtering

### Grouping/Aggregation Columns
- **county_name**: Geographic grouping
- **county_fips**: Alternative geographic grouping
- State can be extracted from county_name for state-level analysis

### Potential Join Keys
- **county_fips**: Standard for joining with other county-level datasets
- **county_name**: Human-readable join key (with careful handling of formatting)

### Data Quality Considerations
1. **Missing Time Dimension**: `month_date_yyyymm` is completely null - temporal analysis requires external date context
2. **High Null Rates**: Price change counts have 70%+ nulls, limiting usefulness for comprehensive analysis
3. **Change Metrics**: Month-over-month and year-over-year columns have 10-25% nulls, suggesting incomplete time series
4. **Quality Flag**: 10.72% nulls in quality indicator - consider filtering or handling appropriately
5. **Extreme Values**: Some metrics show very high maximum values that may be outliers

### Keywords
real estate, housing, inventory, county, FIPS, listing price, days on market, active listings, pending sales, price per square foot, market metrics, time series, geographic analysis, housing market

### Table and Column Documentation
**Table Comment**: Not provided

**Column Comments**: Not provided