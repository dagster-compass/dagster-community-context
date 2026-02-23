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
# Comprehensive Data Summary: US Real Estate County Inventory Metrics

## Overall Dataset Characteristics

**Total Rows:** 344,538

**General Description:** This table contains monthly real estate inventory metrics at the county level across the United States. Each row represents a snapshot of real estate market conditions for a specific county, including pricing, listing activity, days on market, and various year-over-year and month-over-month change metrics.

**Data Quality Observations:**
- The `month_date_yyyymm` column is 100% null, indicating temporal information may be stored elsewhere or missing
- High null percentages (70-75%) in price increase metrics suggest these are less commonly tracked or available
- Moderate null percentages (10-20%) in various month-over-month and year-over-year comparison fields
- Base metrics (prices, counts) have very low null rates (<1%), indicating good core data quality
- The `quality_flag` column (10.72% null) appears to mark data quality concerns

**Notable Patterns:**
- Data covers 3,135+ unique counties across the US
- Metrics span listing activity, pricing, market velocity (days on market), and price adjustments
- Extensive use of percentage change fields (mm = month-over-month, yy = year-over-year)
- Pending ratio metrics suggest supply/demand dynamics tracking

## Column Details

### Geographic Identifiers

**county_name (STRING)**
- Full county names with state abbreviations (e.g., "abbeville, sc")
- 3,135 unique values covering US counties
- 0% null - complete coverage
- Format: lowercase county name, state abbreviation
- **Query Use:** Primary dimension for geographic filtering and grouping

**county_fips (INT64)**
- Federal Information Processing Standards county codes
- Range: 1001 to 56045 (standard 5-digit FIPS codes)
- 3,141 unique values (slightly more than county names, possibly versioning)
- 0% null - complete coverage
- **Query Use:** Reliable join key for geographic data, preferred over names for consistency

### Temporal Field

**month_date_yyyymm (STRING)**
- **100% NULL** - completely empty column
- Intended format appears to be YYYYMM based on name
- **Query Consideration:** Time-based queries not possible with this field; temporal data may exist in table partitioning or external metadata

### Pricing Metrics

**median_listing_price (FLOAT64)**
- Current median listing price in dollars
- Range: $1,311 to $13,000,000
- 52,273 unique values
- 0.02% null - excellent coverage
- **Query Use:** Primary price metric for filtering, aggregation, and trending

**median_listing_price_mm (FLOAT64)**
- Month-over-month price change (decimal percentage)
- Range: -0.9971 to 570.32 (extreme outliers present)
- 10.89% null
- **Query Use:** Identifying rapidly changing markets, filtering for price momentum

**median_listing_price_yy (FLOAT64)**
- Year-over-year price change (decimal percentage)
- Range: -0.9968 to 222.87
- 11.27% null
- **Query Use:** Annual trend analysis, market appreciation/depreciation

**average_listing_price (FLOAT64)**
- Mean listing price in dollars
- Range: $5,000 to $142,882,807 (extreme high-end outliers)
- 252,993 unique values (highest diversity)
- 0.02% null
- **Query Use:** Alternative to median, sensitive to luxury market segments

**average_listing_price_mm / average_listing_price_yy (FLOAT64)**
- Change metrics for average price
- Similar null patterns (10.89% and 11.27%)
- Extreme ranges indicate volatility in some markets

### Price Per Square Foot Metrics

**median_listing_price_per_square_foot (FLOAT64)**
- Price density metric
- Range: $0 to $56,250/sqft (extreme luxury)
- 0.10% null
- **Query Use:** Normalized price comparison across different sized properties

**median_listing_price_per_square_foot_mm / yy (FLOAT64)**
- Change metrics for price per square foot
- 10.96% and 11.37% null respectively
- **Query Use:** Tracking value changes independent of property size

### Property Size Metrics

**median_square_feet (FLOAT64)**
- Median property size
- Range: 4 to 30,902 square feet
- 3,322 unique values
- 0.10% null
- **Query Use:** Property size segmentation, market characterization

**median_square_feet_mm / yy (FLOAT64)**
- Size change metrics (10.96% and 11.37% null)
- **Query Use:** Tracking shifts in property type mix

### Listing Count Metrics

**active_listing_count (FLOAT64)**
- Current active listings
- Range: 0 to 23,258
- 0.01% null - excellent coverage
- **Query Use:** Market inventory levels, supply analysis

**new_listing_count (FLOAT64)**
- New listings in period
- Range: 0 to 9,888
- 0.01% null
- **Query Use:** Market activity indicator, supply flow

**pending_listing_count (FLOAT64)**
- Listings under contract
- Range: 0 to 14,211
- 7.28% null - moderate coverage
- **Query Use:** Demand signal, market velocity

**total_listing_count (FLOAT64)**
- Total listings (active + pending)
- Range: 0 to 33,580
- 0.01% null
- **Query Use:** Overall market size

**Change metrics (_mm / _yy):**
- All listing counts have corresponding month-over-month and year-over-year changes
- Null rates: 10-20% range
- **Query Use:** Growth/decline analysis

### Market Velocity Metrics

**median_days_on_market (FLOAT64)**
- Time to sale indicator
- Range: 1 to 365 days
- 365 unique values (likely capped at 1 year)
- 0.11% null
- **Query Use:** Market hotness indicator, buyer demand signal

**median_days_on_market_mm / yy (FLOAT64)**
- Change in market velocity
- 10.98% and 11.40% null
- **Query Use:** Identifying accelerating/decelerating markets

### Price Adjustment Metrics

**price_increased_count / price_reduced_count (FLOAT64)**
- Number of listings with price changes
- Price increases: 0-1,666 listings
- Price reductions: 0-12,596 listings
- Very low null rates (0.01%)
- **Pattern:** Reductions far more common than increases

**price_increased_share / price_reduced_share (FLOAT64)**
- Proportion of listings with price changes
- Ranges: 0.0 to 4.0 (appears to be decimal representation)
- 0.04% null
- **Query Use:** Market sentiment, pricing pressure indicators

**Change metrics for price adjustments:**
- **High null rates (25-75%)** - particularly for price increases (73.67%-74.31%)
- Indicates these metrics less consistently tracked
- **Query Consideration:** Use with caution, check for sufficient data

### Supply/Demand Indicators

**pending_ratio (FLOAT64)**
- Ratio of pending to active listings
- Range: 0.0 to 11.5
- 7.32% null
- **Query Use:** Key demand/supply balance metric, market strength indicator

**pending_ratio_mm / yy (FLOAT64)**
- Changes in pending ratio
- 17.29% and 19.69% null
- Wide ranges (-10.39 to 11.23) indicate volatile markets
- **Query Use:** Identifying demand shifts

### Data Quality

**quality_flag (FLOAT64)**
- Binary indicator (0.0 or 1.0)
- 10.72% null
- **Query Use:** Filter for data quality, exclude questionable records

## Table and Column Documentation

**Table Comment:** Not provided in the analysis report.

**Column Comments:** No explicit column comments were provided in the source data.

## Potential Query Considerations

### Excellent for Filtering:
- **county_name / county_fips:** Geographic segmentation
- **median_listing_price:** Price range filtering ($100K-$500K, etc.)
- **median_days_on_market:** Hot vs. cold market identification (<30 days, >90 days)
- **quality_flag:** Data quality filtering (WHERE quality_flag = 0)
- **active_listing_count:** Market size filtering (exclude small markets)

### Excellent for Grouping/Aggregation:
- **county_name / county_fips:** Geographic rollups
- **Price ranges:** Bucket properties by price tier
- **State extraction:** Parse from county_name for state-level analysis
- **Quality flag:** Separate analysis of flagged data

### Good for Trending Analysis:
- All **_yy fields:** Year-over-year comparisons
- All **_mm fields:** Month-over-month momentum
- **median_listing_price + temporal joins:** Price trending (requires external date dimension)
- **pending_ratio:** Market balance trending

### Potential Join Keys:
- **county_fips:** Standard geographic join (census data, demographics, economic indicators)
- **county_name:** Human-readable joins (requires standardization)
- Note: No direct time dimension for temporal joins within this table

### Data Quality Considerations:
1. **Missing temporal data:** month_date_yyyymm is entirely null - time analysis requires external context
2. **High nulls in price adjustment metrics:** 70%+ null rates make these unreliable for broad analysis
3. **Outliers:** Extreme values in prices ($142M) and changes (570x increase) may require outlier handling
4. **Quality flag:** Always consider filtering WHERE quality_flag = 0 or IS NULL
5. **Change metric nulls:** 10-20% null rates in comparison fields suggest not all periods have historical data
6. **Pending listing gaps:** 7.28% null suggests not all markets track pending status

### Recommended Query Patterns:
- **Current market snapshots:** Use base metrics (prices, counts) with quality filtering
- **Market comparisons:** Compare counties using median metrics
- **Growth analysis:** Use _yy fields for year-over-year analysis where not null
- **Hot market identification:** Combine low days_on_market with high pending_ratio
- **Price pressure:** Use price_reduced_share vs price_increased_share ratios
- **Market size filtering:** Filter by active_listing_count to focus on statistically significant markets

## Keywords

real estate, housing, inventory, county, FIPS, median price, listing price, days on market, DOM, active listings, pending listings, new listings, price per square foot, square footage, year-over-year, month-over-month, price reduction, price increase, market metrics, supply and demand, pending ratio, housing market, property listings, MLS data, real estate analytics, market velocity, pricing trends, geographic analysis, US counties, housing inventory, market analysis, real estate KPIs