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
# Data Summary: US Real Estate Inventory Core Metrics by Metro Area

## Overall Dataset Characteristics

- **Total Rows**: 102,675 records
- **Dataset Type**: Time-series real estate inventory metrics at the CBSA (Core Based Statistical Area/Metro) level
- **Data Quality**: Generally high quality with systematic null patterns
- **Notable Issue**: The `month_date_yyyymm` column is 100% null, which is problematic as this appears to be time-series data
- **Coverage**: 925 unique metro areas (CBSAs) across the United States
- **Temporal Granularity**: Monthly data (despite the date column being null, the presence of _mm (month-over-month) and _yy (year-over-year) columns confirms this)

## Column-by-Column Analysis

### Identifier & Geographic Columns

**cbsa_code** (INT64)
- Primary identifier for metro areas
- 925 unique values (range: 10100 to 49820)
- No nulls, perfectly populated
- Use for: Filtering by specific metro areas, joining with geographic reference tables

**cbsa_title** (STRING)
- Human-readable metro area names (e.g., "McAllen-Edinburg-Mission, TX")
- 925 unique values matching cbsa_code count
- No nulls
- Use for: Display purposes, text-based filtering

**householdrank** (INT64)
- Ranking metric for metro areas (1-925)
- Likely ranks by household/population size
- Lower numbers = larger/more important markets
- Use for: Filtering top markets, market size analysis

**month_date_yyyymm** (STRING)
- **CRITICAL ISSUE**: 100% null - temporal dimension is missing
- Should contain YYYYMM format dates but completely unpopulated
- This limits time-based analysis despite having temporal metrics

### Price Metrics

**median_listing_price** (FLOAT64)
- Current median listing price by metro
- Range: $19,900 to $5,508,750
- No nulls (0.00%)
- 25,318 unique values indicate high granularity
- Use for: Price comparisons, market affordability analysis

**median_listing_price_mm** (FLOAT64)
- Month-over-month price change (proportional)
- Range: -55.35% to +298.55%
- 10.81% nulls (likely early periods without prior data)
- Negative values = price decreases

**median_listing_price_yy** (FLOAT64)
- Year-over-year price change (proportional)
- Range: -77.58% to +498.48%
- 10.81% nulls
- Use for: Identifying appreciating/depreciating markets

**average_listing_price** (FLOAT64)
- Mean listing price (vs median)
- Range: $44,444 to $23,524,874
- 93,676 unique values (higher than median, indicating more variability)
- Use with median to identify markets with extreme price outliers

**median_listing_price_per_square_foot** (FLOAT64)
- Price efficiency metric
- Range: $22 to $1,778 per sq ft
- No nulls
- Use for: Cross-market price comparisons normalized for size

### Inventory Count Metrics

**active_listing_count** (INT64)
- Current available listings
- Range: 0 to 69,796
- No nulls
- 7,310 unique values
- Use for: Supply analysis, market activity assessment

**new_listing_count** (INT64)
- New listings added in period
- Range: 0 to 27,262
- No nulls
- Use for: Market momentum, seller activity

**total_listing_count** (INT64)
- Total listings (active + pending)
- Range: 1 to 83,125
- No nulls
- Use for: Overall market size

**pending_listing_count** (FLOAT64)
- Listings under contract
- Range: 0 to 28,578
- 2.70% nulls (relatively low)
- Use for: Demand indicator, buyer activity

### Market Dynamics Metrics

**median_days_on_market** (FLOAT64)
- How long listings stay active
- Range: 3 to 322 days
- Only 0.01% nulls (excellent coverage)
- 210 unique values
- Use for: Market speed/competitiveness analysis

**price_increased_count** (INT64)
- Listings with price increases
- Range: 0 to 4,978
- **54.41% nulls** - high null rate suggests this metric isn't tracked in all periods/markets
- Use cautiously due to data quality

**price_reduced_count** (FLOAT64)
- Listings with price reductions
- Range: 0 to 22,456
- No nulls
- Better coverage than price_increased_count
- Use for: Seller desperation/market weakness indicators

**price_increased_share** (FLOAT64)
- Proportion of listings with price increases
- Range: 0% to 38.15%
- No nulls
- Use for: Market strength indicator

**price_reduced_share** (FLOAT64)
- Proportion of listings with price reductions
- Range: 0% to 66.67%
- No nulls
- Use for: Market weakness/inventory overhang indicator

### Ratio & Efficiency Metrics

**pending_ratio** (FLOAT64)
- Pending listings / Active listings
- Range: 0 to 8.0064
- 2.70% nulls
- Values >1 indicate strong demand exceeding supply
- Use for: Market heat/competitiveness assessment

### Property Size Metrics

**median_square_feet** (FLOAT64)
- Median property size
- Range: 892 to 6,000 sq ft
- No nulls
- 2,075 unique values
- Use for: Property size analysis, market characterization

### Change Metrics Pattern

All metrics with **_mm** suffix: Month-over-month change (10.81% nulls typically)
All metrics with **_yy** suffix: Year-over-year change (10.81% nulls typically)

The consistent 10.81% null pattern suggests approximately 11,117 records represent either:
- The first month of data (no prior period for _mm)
- The first year of data (no prior year for _yy)

### Quality Flag

**quality_flag** (FLOAT64)
- Binary indicator (0.0 or 1.0)
- 10.81% nulls
- Likely indicates data quality or completeness issues
- Use for: Filtering reliable records

## Query Considerations

### Recommended Filtering Columns
1. **cbsa_code/cbsa_title**: Specific metro analysis
2. **householdrank**: Top N markets (e.g., TOP 50 metros)
3. **quality_flag**: Filter for quality_flag = 0 or IS NULL depending on needs
4. **median_listing_price**: Price range filters
5. **active_listing_count**: Minimum inventory thresholds

### Aggregation Opportunities
1. **By market size**: GROUP BY householdrank ranges
2. **By price tier**: Create price buckets from median_listing_price
3. **By market performance**: Bucket metros by price_yy changes
4. **By inventory levels**: Categorize by active_listing_count

### Join Considerations
- **cbsa_code** is the primary key for joining with other geographic datasets
- No apparent foreign keys to other tables in this dataset
- Time-based joins impossible due to null month_date_yyyymm

### Data Quality Considerations
1. **Critical**: month_date_yyyymm is entirely null - time-based queries impossible without external date context
2. **High null rates** (54%+) for price_increased_count metrics - avoid or use cautiously
3. **Consistent ~11% nulls** in change metrics indicate first-period records
4. **pending_listing_count** has 2.70% nulls vs 0% for other counts
5. Consider filtering WHERE quality_flag = 0.0 for analysis

### Potential Analysis Queries
1. **Market Rankings**: Top metros by price, inventory, days on market
2. **Price Analysis**: Markets with highest/lowest prices per sq ft
3. **Market Heat**: Using pending_ratio, days_on_market, price_reduced_share
4. **Supply/Demand**: Active vs pending counts, new listing trends
5. **Market Segments**: Small vs large metros (by householdrank)

## Keywords

real estate, housing market, metro areas, CBSA, inventory, listings, median price, active listings, pending listings, days on market, price per square foot, market metrics, housing supply, housing demand, price changes, month over month, year over year, property listings, real estate analytics, metro statistics, market trends, price reductions, new listings, pending ratio, square footage, average price, market rankings, household rank, quality flag, time series, monthly data

## Table and Column Documentation

**Table Comment**: Not provided

**Column Comments**: None provided for any columns

The absence of formal documentation suggests this table would benefit from:
- Clear definition of the measurement period each row represents
- Explanation of quality_flag values
- Documentation of null value patterns
- Clarification of month_date_yyyymm population issues
- Definition of householdrank methodology