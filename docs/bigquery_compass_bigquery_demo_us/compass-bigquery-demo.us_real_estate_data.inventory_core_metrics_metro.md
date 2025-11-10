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
# Comprehensive Table Summary: US Real Estate Inventory Core Metrics by Metro Area

## Overall Dataset Characteristics

**Total Rows:** 102,675

**General Purpose:** This table contains comprehensive real estate inventory and pricing metrics for 925 different metropolitan statistical areas (MSAs/CBSAs) across the United States, tracked over time with month-over-month and year-over-year comparisons.

**Data Quality Observations:**
- High data completeness for core metrics (most columns <1% null)
- One column (`month_date_yyyymm`) is completely null (100%), suggesting it may be deprecated or unused
- Moderate null percentages (10-15%) in growth rate columns (mm/yy comparisons), likely representing first time periods where comparisons aren't possible
- Higher null percentages (50-55%) in price increase metrics, possibly due to data availability or market conditions
- Quality flag present (10.81% null) for data validation purposes

**Notable Patterns:**
- Data covers 925 unique metropolitan areas with consistent geographic coverage
- Household rank suggests metro areas are ordered by size/importance (1-925)
- All metrics include both absolute values and relative changes (month-over-month and year-over-year)
- Time series nature with comparative metrics enables trend analysis

## Column Details

### Geographic Identifiers

**cbsa_title (STRING)**
- Metro area name in "City, State" format
- 0% null, 925 unique values (one per metro area)
- Examples: "Aberdeen, SD", "Tulsa, OK", "McMinnville, TN"
- **Purpose:** Human-readable location identifier

**cbsa_code (INT64)**
- Numeric CBSA (Core Based Statistical Area) identifier
- 0% null, 925 unique values
- Range: 10,100 to 49,820
- **Purpose:** Official census bureau identifier for metro areas; ideal for joins with other census data

**householdrank (INT64)**
- Metro area ranking (presumably by household count/population)
- 0% null, 925 unique values
- Range: 1 to 925 (rank 1 = largest metro)
- **Purpose:** Filtering by market size; useful for segmenting major vs. minor markets

### Date/Time Column

**month_date_yyyymm (STRING)**
- **COMPLETELY NULL (100%)** - appears to be unused/deprecated
- Not suitable for any queries or analysis

### Pricing Metrics

**median_listing_price (FLOAT64)**
- Primary price metric for each metro
- 0% null, 25,318 unique values
- Range: $19,900 to $5,508,750
- Examples: $245,000, $155,000, $372,425
- **Purpose:** Core metric for market affordability and pricing trends

**median_listing_price_mm (FLOAT64)**
- Month-over-month price change (as decimal, e.g., 0.0798 = 7.98% increase)
- 10.81% null
- Range: -55.35% to +298.55%
- **Purpose:** Short-term price trend analysis

**median_listing_price_yy (FLOAT64)**
- Year-over-year price change
- 10.81% null
- Range: -77.58% to +498.48%
- **Purpose:** Long-term price trend analysis

**median_listing_price_per_square_foot (FLOAT64)**
- Price efficiency metric
- 0% null, 1,084 unique values
- Range: $22 to $1,778 per sq ft
- Examples: $121, $219, $194
- **Purpose:** Comparing value across different property sizes

**average_listing_price (FLOAT64)**
- Mean listing price (vs median)
- 0% null, 93,676 unique values (highly granular)
- Range: $44,444 to $23,524,874
- **Purpose:** Capturing high-end outliers that median might miss

### Inventory Metrics

**active_listing_count (INT64)**
- Current properties available for sale
- 0% null, 7,310 unique values
- Range: 0 to 69,796
- Examples: 63, 114, 224
- **Purpose:** Market supply indicator; high values suggest buyer's market

**new_listing_count (INT64)**
- Fresh inventory coming to market
- 0% null, 3,520 unique values
- Range: 0 to 27,262
- **Purpose:** Market momentum indicator

**pending_listing_count (FLOAT64)**
- Properties under contract
- 2.70% null (relatively low)
- Range: 0 to 28,578
- **Purpose:** Leading indicator for closed sales

**total_listing_count (INT64)**
- All listings regardless of status
- 0% null, 9,160 unique values
- Range: 1 to 83,125
- **Purpose:** Overall market size/activity

### Market Velocity Metrics

**median_days_on_market (FLOAT64)**
- Time to sell indicator
- 0.01% null (excellent completeness)
- Range: 3 to 322 days
- Examples: 49, 93, 35 days
- **Purpose:** Market temperature gauge; low values = hot market

### Pricing Strategy Metrics

**price_increased_count (INT64)**
- Listings with price increases
- 0% null, 801 unique values
- Range: 0 to 4,978
- **Note:** High null percentage (54-55%) in growth rate metrics

**price_increased_share (FLOAT64)**
- Proportion of listings with price increases
- 0% null, 1,248 unique values
- Range: 0% to 38.15%
- **Purpose:** Seller confidence indicator

**price_reduced_count (FLOAT64)**
- Listings with price reductions
- 0% null, 2,750 unique values
- Range: 0 to 22,456
- Examples: 50, 38, 32

**price_reduced_share (FLOAT64)**
- Proportion with reductions
- 0% null, 3,233 unique values
- Range: 0% to 66.67%
- **Purpose:** Market distress/oversupply indicator; high values suggest seller pressure

### Property Characteristics

**median_square_feet (FLOAT64)**
- Typical property size in metro
- 0% null, 2,075 unique values
- Range: 892 to 6,000 sq ft
- Examples: 1,823, 1,649, 2,026
- **Purpose:** Understanding property types/sizes by market

### Composite Metrics

**pending_ratio (FLOAT64)**
- Pending listings / active listings
- 2.70% null
- Range: 0 to 8.0064
- Examples: 0.386, 1.028, 0.519
- **Purpose:** Demand/supply balance; >1.0 suggests high demand

### Data Quality Indicator

**quality_flag (FLOAT64)**
- Data validation indicator
- 10.81% null
- Values: 0.0 or 1.0
- **Purpose:** Filtering unreliable data points; 0.0 = good quality

## Query Considerations

### Excellent Filtering Columns:
- **cbsa_code / cbsa_title**: Geographic filtering
- **householdrank**: Market size segmentation (e.g., top 50 metros)
- **quality_flag**: Data quality filtering (WHERE quality_flag = 0.0)

### Ideal Grouping/Aggregation Columns:
- **householdrank ranges**: Size-based cohorts (top 100, mid-tier, small markets)
- **cbsa_title/code**: Metro-level aggregations

### Key Metrics for Analysis:
- **Price metrics**: median_listing_price, median_listing_price_per_square_foot
- **Inventory metrics**: active_listing_count, new_listing_count
- **Market health**: median_days_on_market, pending_ratio, price_reduced_share

### Growth Rate Columns (mm/yy suffix):
- All have ~11% nulls (expected for time series)
- Enable trend identification and momentum analysis
- Month-over-month (mm): Short-term trends
- Year-over-year (yy): Long-term trends, seasonal adjustment

### Potential Join Keys:
- **cbsa_code**: Standard census identifier for joining demographic/economic data
- Combined with time dimension for temporal joins

### Data Quality Considerations:
1. Always filter on `quality_flag = 0.0` for reliable analysis
2. Handle nulls in growth rate metrics (first periods won't have comparisons)
3. `month_date_yyyymm` is unusable (100% null)
4. Price increase metrics have higher null rates (50-55%) - may need special handling
5. Consider outliers in pricing data (ranges are very wide)
6. Pending metrics have slightly higher null rates (~3-14%)

### Common Query Patterns:
- **Market comparison**: Compare metros by pricing, inventory, or velocity metrics
- **Market tier analysis**: Group by householdrank ranges
- **Trend identification**: Use mm/yy growth columns
- **Supply/demand analysis**: Compare pending_ratio, days_on_market, price_reduced_share
- **Affordability studies**: Use median_listing_price and median_listing_price_per_square_foot

## Keywords

real estate, housing market, inventory, metro areas, CBSA, metropolitan statistical areas, listing prices, median prices, days on market, housing supply, housing demand, pending sales, price reductions, price increases, market velocity, market trends, monthly trends, yearly trends, housing affordability, property metrics, square footage, real estate analytics, market analysis, geographic analysis, census data, US housing data

## Table and Column Documentation

**Table Comment:** Not provided in the analysis report.

**Column Comments:** No column-level comments were provided in the analysis report.