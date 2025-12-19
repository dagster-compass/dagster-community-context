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
# Data Summary: global_markets_summary Table

## Overall Dataset Characteristics

**Total Rows:** 65

**General Data Quality:** The dataset has good overall quality with most columns having complete data. However, there's a consistent 20% null pattern across several related columns (asset_type, name, total_return_pct, volatility_pct, period_start_price, period_end_price), suggesting these 13 rows represent some special case or data quality issue.

**Notable Patterns:**
- Data represents ETF (Exchange Traded Fund) performance metrics across different time periods
- Four distinct time periods analyzed: 12_weeks, 6_months, 1_year, and 5_years
- Covers 13 unique market symbols representing different geographic regions (Australia, Mexico, South Africa, Japan, Germany, France, China, Brazil, UK, South Korea, emerging markets, and global markets)
- Trading on two exchanges: ARCX (NYSE Arca) and XNAS (NASDAQ)
- Date ranges span from December 2020 to December 2025

**Table Comment:** Not provided

## Column Details

### Identifiers & Classifications

**symbol** (STRING)
- 13 unique ETF ticker symbols
- No nulls, primary identifier for the security
- Examples: EWA (Australia), EWW (Mexico), EWJ (Japan), EEM (Emerging Markets), ACWI (Global)
- Good for filtering and grouping

**asset_type** (STRING)
- 20% null values (13 rows)
- Only value present: "ETF"
- Limited analytical value due to single category

**name** (STRING)
- 20% null values
- Full names of iShares MSCI ETFs
- Descriptive field corresponding to symbols
- Examples: "ISHARES MSCI AUSTRALIA ETF", "ISHARES MSCI MEXICO ETF"

**exchange** (STRING)
- No nulls, 2 unique values
- ARCX (NYSE Arca) and XNAS (NASDAQ)
- Good for filtering by exchange

### Time Period Information

**time_period** (STRING)
- No nulls, 4 unique values: 12_weeks, 6_months, 1_year, 5_years
- Categorical time frame for analysis
- Essential for temporal comparisons

**period_start_date** (DATE)
- No nulls, 5 unique dates
- Range: 2020-12-18 to 2025-09-25
- Start of measurement period

**period_end_date** (DATE)
- No nulls, 5 unique dates
- Range: 2024-12-16 to 2025-12-16
- End of measurement period

**trading_days** (INT64)
- No nulls, 7 unique values
- Range: 1 to 1,006 days
- Actual trading days in the period (excludes weekends/holidays)
- Values: 1, 58, 68, 123, 1004, 1005, 1006

### Trading Activity Metrics

**positive_days** (INT64)
- No nulls, 38 unique values
- Range: 0 to 342
- Count of days with positive price movement

**negative_days** (INT64)
- No nulls, 36 unique values
- Range: 0 to 308
- Count of days with negative price movement

**neutral_days** (INT64)
- No nulls, 12 unique values
- Range: 0 to 21
- Count of days with no price change
- Relatively rare (small values)

### Performance Metrics

**total_return_pct** (FLOAT64)
- 20% null values
- Range: -6.66% to 23.21%
- Total percentage return over the period
- Key performance indicator

**avg_daily_return_pct** (FLOAT64)
- No nulls, 63 unique values
- Range: -0.4559% to 1.738%
- Average daily return percentage
- Good for normalized performance comparison

**win_rate_pct** (FLOAT64)
- No nulls, 37 unique values
- Range: 0.0% to 100.0%
- Percentage of positive trading days
- Distribution shows typical values around 50-60%

**volatility_pct** (FLOAT64)
- 20% null values
- Range: 5.1% to 25.41%
- Measure of price volatility/risk
- Higher values indicate more volatile markets

### Price Change Metrics

**total_price_change** (FLOAT64)
- No nulls, 61 unique values
- Range: -$11.60 to $17.76
- Absolute price change in dollars

**avg_daily_price_change** (FLOAT64)
- No nulls, 62 unique values
- Range: -$0.15 to $0.41
- Average daily price movement in dollars

**best_day_change** (FLOAT64)
- No nulls, 58 unique values
- Range: -$0.15 to $9.61
- Largest single-day gain (in dollars)

**worst_day_change** (FLOAT64)
- No nulls, 58 unique values
- Range: -$4.74 to $0.41
- Largest single-day loss (in dollars)

### Price Points

**period_start_price** (FLOAT64)
- 20% null values
- Range: $23.55 to $136.61
- Opening price for the period

**period_end_price** (FLOAT64)
- 20% null values
- Range: $24.00 to $139.99
- Closing price for the period

## Potential Query Considerations

### Good for Filtering:
- `time_period` - Compare performance across different time horizons
- `symbol` - Analyze specific markets or regions
- `exchange` - Separate ARCX vs XNAS listed ETFs
- Date ranges using `period_start_date` and `period_end_date`

### Good for Grouping/Aggregation:
- `time_period` - Aggregate performance by time frame
- `symbol` - Compare different geographic markets
- `exchange` - Compare exchange performance
- Calculated groupings like volatility buckets or return categories

### Potential Join Keys:
- `symbol` - Could join with other market data tables
- `exchange` - Could join with exchange metadata
- Date fields - Could join with economic indicators or news data

### Data Quality Considerations:
1. **20% Null Pattern:** Be aware that 13 rows (~20%) have nulls in asset_type, name, total_return_pct, volatility_pct, and price columns. Queries using these columns should handle nulls appropriately or filter them out
2. **Time Period Consistency:** Verify trading_days aligns with the date ranges for accurate period-based calculations
3. **Win Rate Validation:** Ensure positive_days + negative_days + neutral_days = trading_days for data integrity checks
4. **Single Asset Type:** All non-null values show "ETF" - this table is specific to ETF analysis
5. **Price vs Return:** Both absolute price changes and percentage returns are available - choose appropriately for analysis

### Recommended Query Patterns:
- Best/worst performing markets by time period
- Volatility comparisons across regions
- Win rate analysis and correlation with returns
- Time-series performance tracking
- Risk-adjusted return calculations (using volatility)
- Geographic market comparisons

## Keywords

ETF, Exchange Traded Funds, iShares, MSCI, global markets, international markets, stock performance, returns, volatility, trading days, win rate, price changes, market analysis, geographic diversification, emerging markets, developed markets, ARCX, NASDAQ, time series analysis, financial metrics, portfolio performance, risk metrics, daily returns, Australia EWA, Mexico EWW, Japan EWJ, Germany EWG, France EWQ, UK EWU, Brazil EWW, South Africa EZA, South Korea EWY, China FXI, Emerging Markets EEM, Global ACWI, market volatility, investment performance

## Table and Column Documentation

**Table Comment:** Not provided

**Column Comments:** Not provided for any columns