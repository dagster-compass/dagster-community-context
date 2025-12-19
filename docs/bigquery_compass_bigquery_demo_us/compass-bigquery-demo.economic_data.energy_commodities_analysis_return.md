---
columns:
- commodity_name (STRING)
- commodity_unit (STRING)
- month_date (DATE)
- monthly_avg_price (FLOAT64)
- pct_change_q1_forward (FLOAT64)
- pct_change_q2_forward (FLOAT64)
- pct_change_q3_forward (FLOAT64)
- pct_change_q4_forward (FLOAT64)
- quarter_num (INT64)
- quarterly_avg_price (FLOAT64)
- year_month (STRING)
- year_quarter (STRING)
- year_val (INT64)
schema_hash: fbba46c0528f2d25e50a522fd6fba0519895139e12b34ec03ff9d3ce9ddea148

---
# Data Summary: Energy Commodities Analysis Return Table

## Overall Dataset Characteristics

- **Total Rows**: 1,008
- **Time Period Coverage**: 2012-2025 (14 years)
- **Data Quality**: Excellent - minimal null values (max 2.38% in one column)
- **Granularity**: Monthly data with quarterly aggregations
- **Primary Focus**: Energy commodity price tracking and forward-looking percentage changes
- **Data Completeness**: 168 unique months tracked across 6 different energy commodities

## Column Details

### Commodity Identification
**commodity_name** (STRING)
- No null values (100% complete)
- 6 distinct energy commodities tracked:
  - brent (crude oil benchmark)
  - coal
  - crude oil
  - gasoline
  - heating oil
  - natural gas
- Consistent naming convention (lowercase)

**commodity_unit** (STRING)
- No null values (100% complete)
- 4 measurement units:
  - USD/Bbl (Barrel - for crude oil products)
  - USD/Gal (Gallon - for refined products)
  - USD/MMBtu (Million British Thermal Units - for natural gas)
  - USD/T (Ton - for coal)

### Time Dimensions
**year_month** (STRING)
- Format: YYYY-MM (e.g., "2015-05", "2018-12")
- 168 unique month values
- No null values

**month_date** (DATE)
- Date representation of monthly data
- 168 unique dates
- No null values

**year_quarter** (STRING)
- Quarterly grouping identifier
- 56 unique quarters (14 years × 4 quarters)

**quarter_num** (INT64)
- Values: 1, 2, 3, 4 (representing Q1-Q4)
- Uniform distribution expected

**year_val** (INT64)
- Range: 2012-2025
- 14 distinct years

### Price Metrics
**monthly_avg_price** (FLOAT64)
- Average commodity price for the month
- Range: $0.74 to $439.08
- 998 unique values (high granularity)
- Wide range reflects different commodity types and units
- No null values

**quarterly_avg_price** (FLOAT64)
- Quarterly average prices
- Range: $0.96 to $417.55
- 334 unique values
- Smoother than monthly prices (aggregated)

### Forward-Looking Returns (Percentage Changes)
**pct_change_q1_forward** (FLOAT64)
- 1-quarter forward percentage change
- Range: -55.42% to +68.18%
- 0.60% null values (6 rows)
- Many zero values in samples (possible data pattern)

**pct_change_q2_forward** (FLOAT64)
- 2-quarter forward percentage change
- Range: -55.42% to +68.18%
- 1.19% null values (12 rows)
- Sample values show both positive and negative changes

**pct_change_q3_forward** (FLOAT64)
- 3-quarter forward percentage change
- Range: -55.42% to +68.18%
- 1.79% null values (18 rows)

**pct_change_q4_forward** (FLOAT64)
- 4-quarter forward percentage change
- Range: -65.14% to +96.97%
- 2.38% null values (24 rows)
- Widest range (expected for longer forecast horizon)

## Potential Query Considerations

### Excellent Filtering Columns
- `commodity_name`: Perfect for isolating specific commodities
- `year_val`: Year-based analysis
- `quarter_num`: Seasonal pattern analysis
- `year_quarter`: Specific quarterly periods

### Strong Grouping/Aggregation Candidates
- `commodity_name`: Compare performance across commodities
- `year_val`: Year-over-year trends
- `quarter_num`: Seasonal patterns
- `commodity_unit`: Group by measurement type

### Time-Series Analysis
- Use `month_date` for chronological ordering
- `year_month` for period-based filtering
- Forward return columns for predictive analysis

### Join Key Candidates
- `commodity_name + year_month`: Composite key for linking to other commodity datasets
- `year_quarter`: For quarterly economic data joins
- `month_date`: Standard date join key

### Data Quality Considerations
1. **Null Patterns**: Forward return columns have increasing null percentages (0.6% to 2.4%) - likely due to most recent periods lacking future data
2. **Zero Values**: Many zeros in `pct_change_q1_forward` - investigate if this indicates no change or data issues
3. **Date Range**: Data extends to 2025 (future dates) - verify if these are projections
4. **Price Ranges**: Wide variation ($0.74 to $439) requires unit-aware comparisons

### Recommended Query Patterns
- **Trend Analysis**: Use `month_date` or `year_quarter` with `ORDER BY`
- **Commodity Comparison**: Group by `commodity_name` with aggregations
- **Return Analysis**: Filter out nulls in forward return columns for complete periods
- **Seasonal Patterns**: Group by `quarter_num` across multiple years
- **Volatility Studies**: Use standard deviation on forward return columns

## Keywords
energy commodities, crude oil, brent, natural gas, coal, gasoline, heating oil, commodity prices, forward returns, percentage change, quarterly returns, monthly prices, time series, commodity trading, energy market analysis, price forecasting, USD/Bbl, USD/Gal, USD/MMBtu, USD/T, quarterly analysis, seasonal patterns, commodity units, price volatility

## Table and Column Documentation
*No table comment or column comments were provided in the source analysis report.*