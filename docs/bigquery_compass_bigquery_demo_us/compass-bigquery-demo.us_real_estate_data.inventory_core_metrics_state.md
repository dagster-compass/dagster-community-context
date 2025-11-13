---
columns:
- active_listing_count (INT64)
- active_listing_count_mm (FLOAT64)
- active_listing_count_yy (FLOAT64)
- average_listing_price (FLOAT64)
- average_listing_price_mm (FLOAT64)
- average_listing_price_yy (FLOAT64)
- median_days_on_market (INT64)
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
- state (STRING)
- state_id (STRING)
- total_listing_count (INT64)
- total_listing_count_mm (FLOAT64)
- total_listing_count_yy (FLOAT64)
schema_hash: 36323ae9a667a5738e82100dbb5c34f146458c57608d7261989108d26ec763ee

---
# Table Summary: compass-bigquery-demo.us_real_estate_data.inventory_core_metrics_state

## Overall Dataset Characteristics

- **Total Rows**: 5,661
- **Geographic Coverage**: 51 states (including District of Columbia)
- **Data Quality**: Generally high quality with ~89% completeness for time-series comparison metrics
- **Temporal Structure**: Time-series data with month-over-month (mm) and year-over-year (yy) comparisons
- **Notable Pattern**: ~10.81% consistent null percentage across most derived/comparison metrics suggests missing data for earlier time periods or specific state-month combinations

## Column Details

### Primary Identifiers

**state** (STRING)
- No nulls, 51 unique values
- Contains full state names (e.g., "Alabama", "Alaska", "Texas")
- Primary grouping dimension for geographic analysis

**state_id** (STRING)
- No nulls, 51 unique values
- Two-letter state codes (e.g., "AL", "AK", "TX")
- Alternative join key for state-level relationships

**month_date_yyyymm** (STRING)
- 100% null - appears to be unused or deprecated field
- Should not be used for filtering or analysis

### Core Inventory Metrics

**total_listing_count** (INT64)
- No nulls, 5,310 unique values
- Range: 803 to 231,347 listings
- Represents total active inventory for each state-month
- Key metric for market size assessment

**active_listing_count** (INT64)
- No nulls, 5,163 unique values
- Range: 720 to 182,589 listings
- Subset of total listings currently available
- Important for supply-side analysis

**new_listing_count** (INT64)
- No nulls, 3,910 unique values
- Range: 290 to 53,332 new listings
- Measures fresh inventory entering market
- Key indicator of market activity

**pending_listing_count** (FLOAT64)
- 0.48% nulls, 4,726 unique values
- Range: 0.0 to 82,071 pending sales
- Indicates properties under contract
- Strong demand indicator

### Pricing Metrics

**average_listing_price** (FLOAT64)
- No nulls, 5,640 unique values
- Range: $206,417 to $1,730,505
- High variance reflects diverse state market conditions
- Good for understanding premium markets

**median_listing_price** (FLOAT64)
- No nulls, 2,660 unique values
- Range: $129,913 to $886,500
- More stable than average, less affected by outliers
- Primary pricing benchmark

**median_listing_price_per_square_foot** (FLOAT64)
- No nulls, 484 unique values
- Range: $79 to $737 per sq ft
- Normalized pricing metric across different property sizes
- Key for comparative market analysis

### Property Characteristics

**median_square_feet** (FLOAT64)
- No nulls, 1,063 unique values
- Range: 987 to 2,798 square feet
- Indicates typical property size by state
- Useful for understanding housing stock composition

**median_days_on_market** (INT64)
- No nulls, 130 unique values
- Range: 13 to 157 days
- Market velocity indicator (lower = hotter market)
- Critical for timing and demand analysis

### Market Activity Indicators

**pending_ratio** (FLOAT64)
- 0.48% nulls, 4,535 unique values
- Range: 0.0 to 3.212
- Ratio of pending to active listings
- Values >1.0 indicate very high demand relative to supply

**price_reduced_count** (FLOAT64)
- No nulls, 3,275 unique values
- Range: 72 to 71,888 reductions
- Indicates pricing pressure or overpricing

**price_reduced_share** (FLOAT64)
- No nulls, 1,944 unique values
- Range: 0.0254 to 0.4089 (2.5% to 40.9%)
- Percentage of listings with price reductions
- Market strength indicator (lower = stronger)

**price_increased_count** (INT64)
- No nulls, 1,091 unique values
- Range: 0 to 9,466 increases
- Less common than reductions, indicates strong demand

**price_increased_share** (FLOAT64)
- No nulls, 582 unique values
- Range: 0.0 to 0.1302 (0% to 13%)
- Rare metric indicating exceptional market conditions

### Time-Series Comparison Metrics (Month-over-Month)

All "_mm" suffixed columns show monthly change rates with ~10.81% nulls, indicating missing historical data for some periods.

**Key mm metrics**:
- Change rates typically range from -30% to +70%
- Useful for identifying seasonal patterns
- Examples: `total_listing_count_mm`, `median_listing_price_mm`, `pending_listing_count_mm`

### Time-Series Comparison Metrics (Year-over-Year)

All "_yy" suffixed columns show annual change rates with ~10.81-11.45% nulls.

**Key yy metrics**:
- Larger ranges than mm metrics (e.g., -97% to +1,608% for some metrics)
- Better for trend analysis and eliminating seasonality
- Examples: `total_listing_count_yy`, `median_listing_price_yy`, `active_listing_count_yy`

### Data Quality Indicator

**quality_flag** (FLOAT64)
- 10.81% nulls, only 2 unique values (0.0, 1.0)
- Binary flag for data quality issues
- Should be checked when filtering for reliable data

## Query Considerations

### Recommended Filtering Columns
- `state` or `state_id` - Primary geographic filter
- `quality_flag` - Filter for data quality (WHERE quality_flag = 0.0)
- `median_listing_price` - Price range filters
- `total_listing_count` - Market size filters

### Good Aggregation/Grouping Columns
- `state` / `state_id` - Geographic grouping
- Price ranges can be bucketed for cohort analysis
- `median_days_on_market` can be categorized (hot/warm/cold markets)

### Potential Join Keys
- `state_id` - Standard for joining with other state-level data
- `state` - Alternative for state name joins

### Data Quality Considerations
- Always check `quality_flag` = 0.0 for reliable data
- ~10.81% nulls in comparison metrics (_mm, _yy) - exclude or handle appropriately
- `month_date_yyyymm` is completely null and unusable
- 0.48% nulls in `pending_listing_count` and `pending_ratio` may indicate states with no pending sales

### Analysis Patterns
- **Market Health**: Low `median_days_on_market` + high `pending_ratio` = hot market
- **Pricing Pressure**: High `price_reduced_share` = weak market or overpricing
- **Market Size**: Use `total_listing_count` for absolute scale, normalize by population for per-capita analysis
- **Trends**: Use _yy metrics for annual trends, _mm for seasonal patterns
- **Price Points**: `median_listing_price` preferred over `average_listing_price` for typical market conditions

## Keywords
real estate, housing market, property listings, inventory metrics, state-level data, listing prices, days on market, pending sales, market trends, month-over-month, year-over-year, housing supply, demand indicators, price per square foot, market velocity, geographic analysis, US states, residential real estate, market analytics, time series data

## Table and Column Documentation

**Table Comment**: Not provided

**Column Comments**: No column-level comments are present in this table.