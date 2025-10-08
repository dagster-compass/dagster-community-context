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
# Table Summary: compass-bigquery-demo.us_real_estate_data.inventory_core_metrics_zip

## Overall Dataset Characteristics

- **Total Rows**: 3,142,815
- **Dataset Type**: US real estate inventory metrics aggregated by ZIP code
- **Time Series Data**: Contains year-over-year (yy) and month-over-month (mm) comparisons
- **Data Quality**: Generally good with most core metrics having low null rates, though some derived metrics have higher null percentages
- **Coverage**: Spans 34,141 unique postal codes across 26,083 unique ZIP name locations

## Column Details

### **Identifier Columns**
- **postal_code** (INT64): Primary geographic identifier
  - No null values, 34,141 unique ZIP codes
  - Range: 501 to 99,929 (standard US ZIP code format)
  - Ideal for filtering and grouping by location

- **zip_name** (STRING): Human-readable location names
  - 2.30% null rate, 26,083 unique values
  - Format: "city, state" (e.g., "richardson, tx")
  - Good for display purposes and location-based filtering

### **Core Inventory Metrics**
- **total_listing_count** (FLOAT64): Current total listings
  - Very low null rate (0.10%), range 0-2,860
  - Key metric for market activity analysis

- **active_listing_count** (FLOAT64): Currently active listings
  - Low null rate (0.15%), range 0-2,646
  - Primary indicator of available inventory

- **new_listing_count** (FLOAT64): New listings added
  - Very low null rate (0.10%), range 0-802
  - Important for market momentum tracking

- **pending_listing_count** (FLOAT64): Listings under contract
  - Higher null rate (20.69%), range 0-976
  - Indicates buyer demand and market velocity

### **Pricing Metrics**
- **median_listing_price** (FLOAT64): Current median price
  - Low null rate (0.25%), wide range $1-$279M
  - Primary pricing indicator, excellent for analysis

- **average_listing_price** (FLOAT64): Current average price
  - Low null rate (0.25%), wide range $1-$279M
  - Complementary pricing metric to median

- **median_listing_price_per_square_foot** (FLOAT64): Price efficiency metric
  - Low null rate (0.96%), range $0-$795K per sq ft
  - Key for comparing value across markets

### **Property Characteristics**
- **median_square_feet** (FLOAT64): Typical property size
  - Very low null rate (0.95%), range 1-12.5M sq ft
  - Important for understanding market segments

- **median_days_on_market** (FLOAT64): Time to sell indicator
  - Low null rate (0.93%), range 1-365 days
  - Critical for market velocity analysis

### **Market Activity Ratios**
- **pending_ratio** (FLOAT64): Pending/Active ratio
  - Higher null rate (21.63%), range 0-94.5%
  - Key demand indicator when available

- **price_reduced_share** (FLOAT64): Percentage of listings with price cuts
  - Very low null rate (0.46%), range 0-4.0
  - Important market sentiment indicator

- **price_increased_share** (FLOAT64): Percentage of listings with price increases
  - Very low null rate (0.46%), range 0-4.0
  - Market strength indicator

### **Temporal Comparison Metrics (Year-over-Year)**
All "_yy" suffixed columns show year-over-year changes:
- Higher null rates (15-90% depending on metric)
- Negative values indicate decreases, positive indicate increases
- Critical for trend analysis but require careful null handling

### **Temporal Comparison Metrics (Month-over-Month)**
All "_mm" suffixed columns show month-over-month changes:
- Moderate to high null rates (13-90% depending on metric)
- Similar interpretation to YoY metrics but for shorter-term trends

### **Data Quality Indicators**
- **quality_flag** (FLOAT64): Data reliability indicator
  - 11.09% null rate, binary values (0.0 or 1.0)
  - Should be used to filter for reliable data

- **month_date_yyyymm** (STRING): Completely null (100%)
  - Non-functional column, likely a data loading artifact

## Query Considerations

### **Excellent for Filtering**
- `postal_code`: Primary geographic filter
- `zip_name`: Location-based filtering with readable names
- `quality_flag`: Data quality filtering
- Core metrics with low null rates for threshold filtering

### **Ideal for Grouping/Aggregation**
- Geographic: `postal_code`, `zip_name`
- Market segments: `median_square_feet`, price ranges
- Time-based analysis using YoY/MM comparison fields

### **Key Relationships**
- ZIP codes can be joined to other geographic datasets
- Price metrics correlate with square footage for value analysis
- Inventory counts relate to market activity ratios

### **Data Quality Considerations**
- Filter by `quality_flag = 1.0` for reliable data
- Many comparison metrics (_yy, _mm) have high null rates
- `month_date_yyyymm` is entirely null and unusable
- Pending-related metrics have higher null rates (20-38%)
- Price change count metrics are heavily null (54-90%)

### **Recommended Analysis Patterns**
- Use core metrics (total_listing_count, median_listing_price, etc.) for primary analysis
- Apply quality flag filtering for critical analyses
- Handle nulls carefully in temporal comparison metrics
- Consider geographic clustering by state (extractable from zip_name)

## Keywords
real estate, inventory, listings, pricing, ZIP code, market analysis, pending ratio, days on market, square feet, price per square foot, year over year, month over month, market metrics, housing data, property analytics

## Table and Column Documentation
No table comment or column comments are provided in the source data.