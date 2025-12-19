---
columns:
- asset_type (STRING)
- avg_daily_price_change (FLOAT64)
- avg_daily_return_pct (FLOAT64)
- best_day_change (FLOAT64)
- exchange (STRING)
- name (STRING)
- negative_days (INT64)
- neutral_days (INT64)
- period_end_date (DATE)
- period_end_price (FLOAT64)
- period_start_date (DATE)
- period_start_price (FLOAT64)
- positive_days (INT64)
- symbol (STRING)
- time_period (STRING)
- total_price_change (FLOAT64)
- total_return_pct (FLOAT64)
- trading_days (INT64)
- volatility_pct (FLOAT64)
- win_rate_pct (FLOAT64)
- worst_day_change (FLOAT64)
schema_hash: 2ac666c6ed8d128ac602e9d3c2a171bf3c10f062c25ee8960d7856019efb2f1f

---
# Table Analysis Summary: compass-bigquery-demo.economic_data.us_sector_summary

## Overall Dataset Characteristics

**Total Rows:** 63

**General Description:** This table contains performance metrics and trading statistics for US sector ETFs tracked by SPDR Select Sector funds over various time periods. The data represents 11 different sector symbols (XLB, XLC, XLE, XLF, XLI, XLK, XLP, XLRE, XLU, XLV) across 4 different time periods (12 weeks, 1 year, 5 years, 6 months), resulting in approximately 63 combinations.

**Data Quality Observations:**
- High data quality for core trading metrics (0% nulls in most key columns)
- Moderate null percentages (17.46-22.22%) in descriptive and derived financial metrics (asset_type, name, total_return_pct, volatility_pct, period_start_price, period_end_price)
- All records share common characteristics: exchange is consistently "ARCX" and asset_type is "ETF" (where not null)

**Notable Patterns:**
- Date ranges span from December 2020 to December 2025, suggesting both historical and potentially forecasted data
- Trading days range significantly (1 to 1006 days) depending on time_period
- Win rates vary widely from 0% to 100%, indicating diverse sector performance
- Volatility ranges from 8.53% to 31.15%, reflecting different sector risk profiles

## Column Details

### Identifiers & Classifications

**symbol (STRING)**
- Primary identifier for sector ETFs
- 0% nulls, 11 unique values
- Values: XLB (Materials), XLC (Communication Services), XLE (Energy), XLF (Financials), XLI (Industrials), XLK (Technology), XLP (Consumer Staples), XLRE (Real Estate), XLU (Utilities), XLV (Healthcare), plus one unspecified
- *Query Consideration:* Primary key component for filtering and grouping by sector

**time_period (STRING)**
- Defines the analysis window
- 0% nulls, 4 unique values: "12_weeks", "1_year", "5_years", "6_months"
- *Query Consideration:* Critical for time-based comparisons and trend analysis

**asset_type (STRING)**
- 17.46% nulls
- Single unique value: "ETF"
- *Query Consideration:* Not useful for filtering as all non-null values are identical

**exchange (STRING)**
- 0% nulls, single value: "ARCX" (NYSE Arca)
- *Query Consideration:* Not useful for filtering (no variation)

**name (STRING)**
- 17.46% nulls, 16 unique values
- Full descriptive names for sector funds (e.g., "Energy Select Sector SPDR Fund")
- Some entries show formatting variations with trailing spaces
- *Query Consideration:* Useful for display/reporting but symbol is more reliable for joins

### Date & Time Metrics

**period_start_date (DATE)**
- 0% nulls, 8 unique values
- Range: 2020-12-18 to 2025-12-16
- *Query Consideration:* Essential for date-based filtering and time series analysis

**period_end_date (DATE)**
- 0% nulls, 8 unique values
- Range: 2024-12-16 to 2025-12-16
- *Query Consideration:* Defines end of analysis window; use for current vs. historical comparisons

**trading_days (INT64)**
- 0% nulls, 11 unique values
- Range: 1 to 1006 days
- Correlates with time_period (e.g., 5_years ≈ 1000+ trading days)
- *Query Consideration:* Important denominator for calculating average metrics

### Trading Activity Metrics

**negative_days (INT64)**
- 0% nulls, 36 unique values
- Range: 0 to 499 days
- *Query Consideration:* Use for calculating loss frequency and risk metrics

**neutral_days (INT64)**
- 0% nulls, 8 unique values
- Range: 0 to 9 days (very small relative to trading_days)
- *Query Consideration:* Minimal impact on analysis; represents no-change trading days

**positive_days (INT64)**
- 0% nulls, 40 unique values
- Range: 0 to 533 days
- *Query Consideration:* Use for calculating win frequency and momentum

**win_rate_pct (FLOAT64)**
- 0% nulls, 43 unique values
- Range: 0.0% to 100.0%
- Calculated as (positive_days / trading_days) * 100
- *Query Consideration:* Key performance indicator; good for ranking and filtering top performers

### Return & Performance Metrics

**total_return_pct (FLOAT64)**
- 17.46% nulls, 44 unique values
- Range: -51.5% to 15.12%
- *Query Consideration:* Primary performance metric; nulls may indicate incomplete data periods

**volatility_pct (FLOAT64)**
- 22.22% nulls, 49 unique values
- Range: 8.53% to 31.15%
- Represents price variability/risk
- *Query Consideration:* Critical for risk-adjusted return analysis; higher null rate suggests calculation constraints

**avg_daily_return_pct (FLOAT64)**
- 0% nulls, 63 unique values (highest uniqueness)
- Range: -2.2753% to 0.3677%
- *Query Consideration:* Normalized performance metric; use for cross-period comparisons

### Price Change Metrics

**total_price_change (FLOAT64)**
- 0% nulls, 58 unique values
- Range: -43.45 to 58.45
- Absolute price movement in dollars
- *Query Consideration:* Raw price movement; combine with return_pct for context

**avg_daily_price_change (FLOAT64)**
- 0% nulls, 62 unique values
- Range: -1.02 to 0.5902
- *Query Consideration:* Normalized daily movement; useful for volatility analysis

**worst_day_change (FLOAT64)**
- 0% nulls, 60 unique values
- Range: -15.29 to 0.51
- *Query Consideration:* Downside risk indicator; useful for maximum drawdown analysis

**best_day_change (FLOAT64)**
- 0% nulls, 61 unique values
- Range: -1.02 to 23.76
- *Query Consideration:* Upside potential indicator

### Price Level Metrics

**period_start_price (FLOAT64)**
- 17.46% nulls, 44 unique values
- Range: $41.62 to $275.96
- *Query Consideration:* Required for return calculations; nulls align with total_return_pct nulls

**period_end_price (FLOAT64)**
- 17.46% nulls, 44 unique values
- Range: $40.55 to $278.49
- *Query Consideration:* Current valuation; nulls align with other price metrics

## Query Considerations

### Good for Filtering:
- **symbol**: Filter by specific sector(s)
- **time_period**: Compare performance across different timeframes
- **period_start_date / period_end_date**: Date range filtering
- **win_rate_pct**: Find sectors with high success rates
- **total_return_pct**: Filter by performance thresholds (WHERE total_return_pct > 10)
- **volatility_pct**: Risk-based filtering

### Good for Grouping/Aggregation:
- **symbol**: Aggregate across time periods for sector analysis
- **time_period**: Compare metrics across different timeframes
- **exchange**: (Limited utility due to single value)

### Potential Join Keys:
- **symbol**: Primary key for joining with other sector/ETF tables
- **symbol + time_period**: Composite key for unique record identification
- **period_end_date**: Temporal joins with market data

### Data Quality Considerations:

1. **Null Handling**: Approximately 17-22% of records missing descriptive and derived metrics (name, asset_type, return calculations, prices). Queries should use `IS NOT NULL` checks or `COALESCE()` for these columns.

2. **Calculation Dependencies**: Metrics like `win_rate_pct` can be recalculated from `positive_days` and `trading_days` if needed for validation.

3. **Date Consistency**: Verify that `period_end_date - period_start_date` aligns logically with `time_period` categories.

4. **Time Period Mapping**:
   - "12_weeks" ≈ 60 trading days
   - "6_months" ≈ 120-130 trading days  
   - "1_year" ≈ 250-252 trading days
   - "5_years" ≈ 1000-1260 trading days

5. **Price Change Validation**: `total_price_change` should equal `period_end_price - period_start_price`

## Keywords

US sectors, SPDR ETFs, sector performance, trading statistics, market analysis, financial returns, volatility analysis, sector rotation, equity sectors, XLB, XLC, XLE, XLF, XLI, XLK, XLP, XLRE, XLU, XLV, NYSE Arca, ARCX, time series analysis, win rate, daily returns, price momentum, sector comparison, risk metrics, trading days, market performance, historical data

## Table and Column Documentation

**Table Comment:** Not provided

**Column Comments:** Not provided