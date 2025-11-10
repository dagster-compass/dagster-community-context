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
# Table Summary: US Real Estate Inventory Core Metrics by State

## Overall Dataset Characteristics

**Total Rows:** 5,661

**General Description:** This table contains comprehensive real estate market metrics at the state level, tracking inventory, pricing, and market activity indicators. The data appears to be time-series data with monthly snapshots across all 51 US states (including DC).

**Data Quality Observations:**
- Most core metrics have excellent completeness (0% nulls)
- Year-over-year (yy) and month-over-month (mm) comparison fields consistently have ~10.81% null values, likely representing the first year/month of data collection where comparisons aren't possible
- The `month_date_yyyymm` field is 100% null, suggesting it may be deprecated or unused
- Generally high-quality dataset with consistent patterns across time-based comparison fields

**Notable Patterns:**
- Data covers 51 unique states/territories (all US states plus DC)
- Clear temporal comparison structure with `_mm` (month-over-month) and `_yy` (year-over-year) suffix patterns
- Price metrics span a wide range, reflecting diverse state-level real estate markets (from ~$130K to ~$1.7M median prices)
- Quality flag indicates some data quality tracking mechanism (0.0 or 1.0 values)

## Column Details

### Geographic Identifiers

**state (STRING)**
- Full state names (e.g., "Alabama", "California", "Massachusetts")
- 51 unique values (all US states + DC)
- No nulls - required field
- Primary geographic dimension for analysis

**state_id (STRING)**
- Two-letter state abbreviations (e.g., "AL", "CA", "MA")
- 51 unique values
- No nulls - required field
- Useful for joins and compact display

### Inventory Metrics

**total_listing_count (INT64)**
- Total active listings in the state
- Range: 803 to 231,347 listings
- No nulls
- Key volume indicator
- High cardinality (5,310 unique values)

**active_listing_count (INT64)**
- Currently active listings
- Range: 720 to 182,589
- No nulls
- Subset of total listings
- 5,163 unique values

**new_listing_count (INT64)**
- Newly added listings in the period
- Range: 290 to 53,332
- No nulls
- Measures market supply influx
- 3,910 unique values

**pending_listing_count (FLOAT64)**
- Listings with pending sales
- Range: 0.0 to 82,071
- 0.48% nulls (minimal)
- Indicates buyer demand
- 4,726 unique values

### Price Metrics

**median_listing_price (FLOAT64)**
- Median price across all listings
- Range: $129,913 to $886,500
- No nulls
- Primary price indicator
- 2,660 unique values suggesting granular price tracking

**average_listing_price (FLOAT64)**
- Mean price across all listings
- Range: $206,417 to $1,730,505
- No nulls
- Higher than median due to luxury property influence
- 5,640 unique values (very high cardinality)

**median_listing_price_per_square_foot (FLOAT64)**
- Price efficiency metric
- Range: $79 to $737 per sq ft
- No nulls
- Useful for market comparisons
- 484 unique values

### Property Characteristics

**median_square_feet (FLOAT64)**
- Median property size
- Range: 987 to 2,798 sq ft
- No nulls
- Reflects regional housing size preferences
- 1,063 unique values

### Market Activity Indicators

**pending_ratio (FLOAT64)**
- Ratio of pending to active listings
- Range: 0.0 to 3.212
- 0.48% nulls (minimal)
- Market velocity indicator
- Higher values = faster moving market

**median_days_on_market (INT64)**
- Time to sale/contract
- Range: 13 to 157 days
- No nulls
- Key market speed metric
- Only 130 unique values (relatively discrete)

**price_reduced_count (FLOAT64)**
- Number of listings with price reductions
- Range: 72 to 71,888
- No nulls
- Market softness indicator
- 3,275 unique values

**price_reduced_share (FLOAT64)**
- Proportion of listings with price cuts
- Range: 0.0254 to 0.4089 (2.5% to 41%)
- No nulls
- Normalized market softness metric
- 1,944 unique values

**price_increased_count (INT64)**
- Number of listings with price increases
- Range: 0 to 9,466
- No nulls
- Market strength indicator
- 1,091 unique values (lower than price_reduced_count)

**price_increased_share (FLOAT64)**
- Proportion of listings with price increases
- Range: 0.0 to 0.1302 (0% to 13%)
- No nulls
- Generally much lower than price_reduced_share
- 582 unique values

### Temporal Comparison Metrics (Month-over-Month)

All `_mm` suffixed fields show month-over-month percentage changes with consistent ~10.81% null pattern:

**total_listing_count_mm, active_listing_count_mm, new_listing_count_mm, pending_listing_count_mm**
- Growth rates for inventory metrics
- Range typically -0.3 to +0.8 (-30% to +80%)

**median_listing_price_mm, average_listing_price_mm, median_listing_price_per_square_foot_mm**
- Price change metrics
- More stable ranges (~-0.1 to +0.1, or ±10%)

**median_days_on_market_mm, median_square_feet_mm**
- Property characteristic changes
- Similar volatility to inventory metrics

**price_reduced_count_mm, price_increased_count_mm, price_reduced_share_mm, price_increased_share_mm**
- Pricing behavior changes
- Moderate volatility

**pending_ratio_mm**
- Market velocity changes
- Range: -0.87 to +1.20

### Temporal Comparison Metrics (Year-over-Year)

All `_yy` suffixed fields show year-over-year percentage changes with consistent ~10.81-11.45% null pattern:

**Similar structure to `_mm` metrics but with generally larger ranges**
- Example: `total_listing_count_yy` ranges from -0.50 to +1.17 (-50% to +117%)
- Captures longer-term trends and seasonality

**pending_ratio_yy**
- Extreme range: -2.59 to +2.59
- Shows significant year-over-year market velocity shifts

### Data Quality Indicator

**quality_flag (FLOAT64)**
- Binary indicator: 0.0 or 1.0
- 10.81% nulls
- Likely flags data quality issues when set to 1.0
- Values of 0.0 observed in sample data suggest good quality records

### Deprecated Field

**month_date_yyyymm (STRING)**
- 100% null
- Appears to be unused/deprecated
- Likely replaced by external date dimension

## Potential Query Considerations

### Best Filtering Columns
- `state` / `state_id`: Geographic filtering
- `quality_flag`: Filter for reliable data (WHERE quality_flag = 0.0 OR quality_flag IS NULL)
- Date fields (external): Time-based filtering
- Price ranges on `median_listing_price`, `average_listing_price`
- Inventory thresholds on `total_listing_count`, `active_listing_count`

### Best Grouping/Aggregation Columns
- `state` / `state_id`: Geographic aggregation
- Time dimensions (external): Temporal trends
- Price segments (created from price metrics)
- Market speed categories (from `median_days_on_market`)

### Potential Join Keys
- `state_id`: Join to state demographic/economic data
- External date dimension for time-series analysis
- Could join to county or metro-level data if available

### Key Analytical Metrics
- **Supply indicators**: `total_listing_count`, `new_listing_count`, inventory changes (`_mm`, `_yy`)
- **Demand indicators**: `pending_listing_count`, `pending_ratio`
- **Price trends**: All price metrics and their temporal changes
- **Market health**: `price_reduced_share`, `pending_ratio`, `median_days_on_market`
- **Growth rates**: All `_mm` and `_yy` fields for trend analysis

### Data Quality Considerations
1. **Null handling**: ~11% nulls in comparison fields likely represent first periods
2. **Filter on quality_flag**: Consider excluding records where `quality_flag = 1.0`
3. **Outlier detection**: Some extreme values in `_yy` fields (e.g., pending_ratio_yy > 2.5)
4. **State-level aggregation**: Be aware of vastly different market sizes (CA vs WY)
5. **Price skew**: Average prices consistently higher than median, indicating right-skewed distributions

## Keywords

real estate, housing market, inventory metrics, listing prices, state level data, market trends, property metrics, days on market, pending sales, price reductions, year over year growth, month over month changes, market velocity, housing supply, housing demand, median prices, average prices, square footage, active listings, new listings, pending listings, price per square foot, market indicators, US states, real estate analytics, housing statistics

## Table and Column Documentation

**Table Comment:** Not provided in the analysis report.

**Column Comments:** No column-level comments were included in the source data analysis.