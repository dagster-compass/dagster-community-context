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
# Comprehensive Data Summary: US Real Estate Inventory Core Metrics by State

## Overall Dataset Characteristics

**Total Rows:** 5,661

**General Description:** This dataset contains time-series real estate inventory metrics aggregated at the US state level. It tracks various listing characteristics, price movements, and market activity indicators across all 51 US states (including DC).

**Data Quality Observations:**
- High-quality dataset with most core metrics having 0% null values
- Approximately 10.81% null values appear consistently across year-over-year (yy) and month-over-month (mm) comparison metrics, likely due to insufficient historical data for recent time periods
- The `month_date_yyyymm` column is completely null (100%), suggesting date information may be stored elsewhere or the column is deprecated
- `pending_ratio` and `pending_listing_count` have slightly higher null percentages (~0.48-11.45%)

**Notable Patterns:**
- Dataset appears to track monthly snapshots of real estate markets
- Each row represents a state's metrics for a specific time period
- Includes both absolute values and percentage changes (mm = month-over-month, yy = year-over-year)
- Price-related metrics show both increases and decreases, indicating market volatility

## Column Details

### Geographic Identifiers

**state (STRING)**
- No null values (0.00%)
- 51 unique values representing all US states plus DC
- Examples: Alabama, Alaska, Arizona, California, New York, Pennsylvania
- **Primary grouping dimension for state-level analysis**

**state_id (STRING)**
- No null values (0.00%)
- 51 unique values (standard 2-letter state abbreviations)
- Examples: AK, AL, NY, PA, CA
- **Ideal for joins and compact representations**

### Listing Volume Metrics

**total_listing_count (INT64)**
- No null values (0.00%)
- 5,310 unique values
- Range: 803 to 231,347 listings
- Represents total active inventory in the market
- **Key metric for market size and filtering**

**active_listing_count (INT64)**
- No null values (0.00%)
- 5,163 unique values
- Range: 720 to 182,589 listings
- Subset of total listings currently active
- **Primary inventory metric**

**new_listing_count (INT64)**
- No null values (0.00%)
- 3,910 unique values
- Range: 290 to 53,332 new listings
- Measures fresh inventory entering market
- **Indicator of market supply dynamics**

**pending_listing_count (FLOAT64)**
- Null: 0.48% (minimal)
- 4,726 unique values
- Range: 0.0 to 82,071 pending listings
- Represents listings under contract
- **Demand signal and market velocity indicator**

### Price Metrics (Absolute Values)

**median_listing_price (FLOAT64)**
- No null values (0.00%)
- 2,660 unique values
- Range: $129,913 to $886,500
- **Primary price point metric for market comparison**

**average_listing_price (FLOAT64)**
- No null values (0.00%)
- 5,640 unique values (highly granular)
- Range: $206,417 to $1,730,505
- Higher than median, indicating right-skewed price distributions
- **Useful for high-end market analysis**

**median_listing_price_per_square_foot (FLOAT64)**
- No null values (0.00%)
- 484 unique values
- Range: $79 to $737 per sq ft
- **Standardized price metric for cross-market comparison**

### Property Size Metrics

**median_square_feet (FLOAT64)**
- No null values (0.00%)
- 1,063 unique values
- Range: 987 to 2,798 square feet
- **Property size characteristic**

### Market Velocity Metrics

**median_days_on_market (INT64)**
- No null values (0.00%)
- 130 unique values
- Range: 13 to 157 days
- **Key indicator of market liquidity and demand**

**pending_ratio (FLOAT64)**
- Null: 0.48%
- 4,535 unique values
- Range: 0.0 to 3.212
- Ratio of pending to active listings
- **Market absorption rate indicator**

### Price Action Metrics

**price_reduced_count (FLOAT64)**
- No null values (0.00%)
- 3,275 unique values
- Range: 72 to 71,888 listings with price reductions
- **Seller desperation/market weakness indicator**

**price_reduced_share (FLOAT64)**
- No null values (0.00%)
- 1,944 unique values
- Range: 0.0254 to 0.4089 (2.54% to 40.89%)
- Percentage of listings with price reductions
- **Market sentiment metric**

**price_increased_count (INT64)**
- No null values (0.00%)
- 1,091 unique values
- Range: 0 to 9,466 listings with price increases
- **Seller confidence/market strength indicator**

**price_increased_share (FLOAT64)**
- No null values (0.00%)
- 582 unique values
- Range: 0.0 to 0.1302 (0% to 13.02%)
- Much lower than price reduction share
- **Bullish market indicator**

### Change Metrics - Month-over-Month (mm suffix)

All _mm metrics show approximately 10.81% null values, representing percentage changes from previous month:

**Key Month-over-Month Metrics:**
- `total_listing_count_mm`: Range -35.92% to +77.39%
- `active_listing_count_mm`: Range -30.74% to +61.16%
- `median_listing_price_mm`: Range -10.38% to +11.35%
- `average_listing_price_mm`: Range -45.12% to +92.44%
- `pending_listing_count_mm`: Range -97.34% to +1,594.03% (extreme volatility)
- `median_days_on_market_mm`: Range -60.23% to +58.73%

**Use Case:** Short-term trend analysis and seasonal adjustments

### Change Metrics - Year-over-Year (yy suffix)

All _yy metrics show approximately 10.81% null values, representing percentage changes from same month previous year:

**Key Year-over-Year Metrics:**
- `total_listing_count_yy`: Range -49.54% to +116.88%
- `active_listing_count_yy`: Range -71.73% to +235.32%
- `median_listing_price_yy`: Range -20.71% to +41.01%
- `average_listing_price_yy`: Range -38.96% to +105.08%
- `pending_ratio_yy`: Range -258.72% to +259.49% (extreme changes)
- `median_days_on_market_yy`: Range -71.55% to +162.71%

**Use Case:** Long-term trend analysis, annual comparisons, removing seasonality

### Data Quality Indicator

**quality_flag (FLOAT64)**
- Null: 10.81%
- Only 2 unique values: 0.0 and 1.0
- Binary flag likely indicating data quality or completeness
- **Filter criterion for high-quality records**

### Deprecated Column

**month_date_yyyymm (STRING)**
- 100% null values
- Appears to be unused or replaced by another date mechanism
- **Should not be used in queries**

## Potential Query Considerations

### Ideal Filtering Columns
1. **state / state_id**: Geographic filtering (51 distinct regions)
2. **quality_flag**: Data quality filtering (0.0 vs 1.0)
3. **median_days_on_market**: Market speed filtering (< 30 days = hot, > 90 days = slow)
4. **price_reduced_share**: Market stress filtering (> 0.3 = high stress)
5. **pending_ratio**: Demand filtering (> 1.0 = high demand)

### Ideal Grouping/Aggregation Columns
1. **state / state_id**: Primary geographic dimension
2. **Quality segments**: Based on median_listing_price ranges
3. **Market speed tiers**: Based on median_days_on_market
4. **Inventory levels**: Based on total_listing_count
5. **Time-based**: Despite null month_date_yyyymm, temporal patterns exist in data

### Potential Join Keys
- **state_id**: Can join to other state-level demographic, economic, or geographic datasets
- **state**: Human-readable joins to state reference tables
- Combination of state + time period (if temporal dimension identified)

### Data Quality Considerations for Queries

1. **Null Handling**:
   - All _mm and _yy metrics have ~10.81% nulls - use COALESCE or WHERE clauses
   - pending_ratio and pending_listing_count have slight nulls (~0.48%)
   - Always exclude month_date_yyyymm from queries

2. **Outlier Awareness**:
   - pending_listing_count_mm shows extreme ranges (-97% to +1,594%)
   - pending_ratio ranges to 3.212 (unusual ratio values)
   - Consider filtering extreme values for realistic analysis

3. **Derived Metrics Possible**:
   - Calculate inventory months: `active_listing_count / new_listing_count`
   - Price to square foot ratios already provided
   - Absorption rate from pending_ratio
   - Market health scores combining multiple indicators

4. **Temporal Considerations**:
   - Despite null month_date_yyyymm, data clearly has time series structure
   - _mm and _yy metrics confirm monthly granularity
   - May need external date mapping or time-based ordering

5. **Statistical Analysis**:
   - High unique value counts in metrics like average_listing_price (5,640) enable detailed analysis
   - Wide ranges in most metrics indicate significant interstate variation
   - Year-over-year metrics show substantial market volatility (e.g., +235% to -72% in active_listing_count_yy)

## Keywords

real estate, housing market, inventory metrics, listing prices, state-level data, market trends, days on market, pending sales, active listings, new listings, price reductions, price increases, square footage, market velocity, absorption rate, housing supply, real estate analytics, property metrics, US states, time series, month-over-month, year-over-year, market indicators, listing counts, median prices, average prices, price per square foot, market health, real estate trends, geographic analysis

## Table and Column Documentation

**Table Comment:** Not provided in the analysis report.

**Column Comments:** No specific column comments were provided in the analysis report. The column names are self-descriptive with clear naming conventions:
- Base metrics (no suffix): Absolute current values
- _mm suffix: Month-over-month percentage change
- _yy suffix: Year-over-year percentage change
- _count: Integer counts
- _share: Percentage/ratio metrics
- _price: Dollar amounts
- _ratio: Calculated ratios