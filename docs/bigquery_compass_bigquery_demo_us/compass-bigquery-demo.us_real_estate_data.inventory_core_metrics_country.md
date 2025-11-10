---
columns:
- active_listing_count (INT64)
- active_listing_count_mm (FLOAT64)
- active_listing_count_yy (FLOAT64)
- average_listing_price (FLOAT64)
- average_listing_price_mm (FLOAT64)
- average_listing_price_yy (FLOAT64)
- country (STRING)
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
- pending_listing_count (INT64)
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
schema_hash: e657215716a559308360810f9c2b29a688e8a830a64b7fd25300c324e416e4f2

---
# Table Summary: inventory_core_metrics_country

## Overall Dataset Characteristics

**Total Rows:** 111

**General Data Quality:**
- The dataset appears to be a time-series of monthly real estate inventory metrics at the country level (United States)
- Approximately 10.81% of rows have null values for most metric columns, suggesting 12 rows lack comparative data (likely the first 12 months where year-over-year and month-over-month comparisons aren't available)
- One column (`month_date_yyyymm`) is completely null (100%), indicating missing temporal identifiers
- One column (`country`) contains only a single value, serving as a constant identifier
- The `quality_flag` column only contains 0.0 or null values

**Notable Patterns:**
- The data contains both absolute metrics (counts, prices) and relative change metrics (year-over-year and month-over-month percentage changes)
- Metrics cover multiple aspects: listing counts, prices, square footage, market timing (days on market), and price adjustments
- Value ranges suggest this is US national-level aggregated data with large absolute numbers (listings in hundreds of thousands to millions)

## Column Details

### Identifier Columns

**country (STRING)**
- Data Type: Categorical identifier
- Null: 0%
- Values: Always "United States"
- Purpose: Geographic identifier (constant for this table)

**month_date_yyyymm (STRING)**
- Data Type: Temporal identifier
- Null: 100% (completely empty)
- Issue: Missing date identifiers make temporal analysis challenging without external joins

### Absolute Count Metrics

**total_listing_count (INT64)**
- Total active + pending listings
- Range: 815,253 to 1,873,209
- Null: 0%
- High variability suggests seasonal patterns or market changes

**active_listing_count (INT64)**
- Properties actively listed
- Range: 346,514 to 1,463,025
- Null: 0%
- Typically represents majority of total listings

**pending_listing_count (INT64)**
- Properties under contract
- Range: 257,571 to 659,596
- Null: 0%
- Generally 15-40% of total listings

**new_listing_count (INT64)**
- New properties added in period
- Range: 215,940 to 584,354
- Null: 0%
- Key indicator of market supply

### Price Metrics

**median_listing_price (FLOAT64)**
- Median asking price
- Range: $249,900 to $449,000
- Null: 0%
- 94 unique values suggest gradual price movements

**average_listing_price (FLOAT64)**
- Mean asking price
- Range: $439,191 to $791,655
- Null: 0%
- Consistently higher than median, indicating right-skewed distribution

**median_listing_price_per_square_foot (FLOAT64)**
- Price efficiency metric
- Range: $125 to $234 per sq ft
- Null: 0%
- Only 55 unique values despite 111 rows

### Property Characteristics

**median_square_feet (FLOAT64)**
- Typical property size
- Range: 1,776 to 1,997 sq ft
- Null: 0%
- Relatively stable with 86 unique values

**median_days_on_market (INT64)**
- Time to sell/pending
- Range: 30 to 88 days
- Null: 0%
- Only 45 unique values, suggesting clustering around common durations

### Price Adjustment Metrics

**price_reduced_count (FLOAT64)**
- Count of price reductions
- Range: 64,958 to 458,240
- Null: 0%
- Significant volume indicates active price discovery

**price_reduced_share (FLOAT64)**
- Proportion with price cuts
- Range: 5.37% to 21.68%
- Null: 0%
- 109 unique values show high variability

**price_increased_count (INT64)**
- Count of price increases
- Range: 12,220 to 61,028
- Null: 0%
- Much lower than reductions

**price_increased_share (FLOAT64)**
- Proportion with price hikes
- Range: 0.86% to 3.47%
- Null: 0%
- Small percentages typical in buyer markets

### Comparative Metrics (Month-over-Month)

All `_mm` suffixed columns:
- Null: 10.81% (12 rows)
- Represent percentage change from previous month
- Range typically -40% to +70% for counts
- Range typically -3% to +5% for ratios and shares

**Key Month-over-Month Metrics:**
- `total_listing_count_mm`: -14.06% to +11.61%
- `pending_listing_count_mm`: -14.61% to +27.17%
- `average_listing_price_mm`: -3.74% to +5.66%
- `median_days_on_market_mm`: -31.36% to +20.59%

### Comparative Metrics (Year-over-Year)

All `_yy` suffixed columns:
- Null: 10.81% (12 rows)
- Represent percentage change from same month prior year
- Generally show wider ranges than month-over-month

**Key Year-over-Year Metrics:**
- `total_listing_count_yy`: -27.12% to +22.68%
- `pending_listing_count_yy`: -36.9% to +58.77%
- `average_listing_price_yy`: -4.08% to +33.37%
- `active_listing_count_yy`: -53.74% to +67.17%

### Ratio Metrics

**pending_ratio (FLOAT64)**
- Pending to active ratio
- Range: 0.2322 to 1.4765
- Null: 0%
- Market velocity indicator

**pending_ratio_mm / pending_ratio_yy (FLOAT64)**
- Changes in pending ratio
- Null: 10.81%
- Wide ranges (-77.88% to +99.31% YoY) indicate market volatility

### Quality Indicator

**quality_flag (FLOAT64)**
- Data quality indicator
- Values: Only 0.0 or null
- Null: 10.81%
- All non-null values are 0.0 (possibly "no issues" flag)

## Query Considerations

### Good for Filtering:
- `country`: Though constant, useful for multi-country datasets
- `quality_flag`: Filter out potential data quality issues (though all are 0.0)
- Date-based filtering would require external temporal data

### Good for Grouping/Aggregation:
- Not applicable - single-country dataset with no natural grouping variables
- Temporal grouping impossible without date field

### Time Series Analysis:
- Dataset appears to be ordered temporally (111 rows likely = ~9 years of monthly data)
- Rows 1-12 likely lack comparative metrics (hence 10.81% nulls ≈ 12/111)
- YoY and MoM metrics enable trend analysis
- Missing `month_date_yyyymm` is critical gap

### Potential Join Keys:
- `country`: Could join to other country-level tables
- Missing date field limits temporal joins
- Row order may implicitly represent chronological sequence

### Data Quality Considerations:
1. **Missing temporal identifier**: Queries requiring specific dates will fail
2. **10.81% nulls in comparative metrics**: Filter or handle first 12 months separately
3. **100% null month_date_yyyymm**: Cannot directly query by date
4. **Consistent null patterns**: All _mm and _yy columns null together
5. **Price vs count metrics**: Different scales require appropriate aggregation functions

### Recommended Query Patterns:
- Use ROW_NUMBER() or implicit ordering for temporal analysis
- Filter WHERE quality_flag = 0.0 or IS NULL for clean data
- Be cautious with aggregations on percentage change columns
- Consider absolute metrics more reliable than derived ones
- Pair median and average prices to understand distribution skew

## Keywords

real estate, housing market, inventory metrics, listing prices, days on market, pending sales, active listings, price reductions, market velocity, housing supply, property metrics, time series, monthly data, United States, national statistics, median price, average price, square footage, price per square foot, year-over-year, month-over-month, market trends, housing inventory

## Table and Column Documentation

**Table Comment:** Not provided

**Column Comments:** Not provided for any columns