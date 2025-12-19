---
columns:
- exchange (STRING)
- month_date (DATE)
- monthly_avg_close (FLOAT64)
- monthly_avg_high (FLOAT64)
- monthly_avg_low (FLOAT64)
- monthly_avg_open (FLOAT64)
- monthly_avg_volume (FLOAT64)
- pct_change_q1_forward (FLOAT64)
- pct_change_q2_forward (FLOAT64)
- pct_change_q3_forward (FLOAT64)
- pct_change_q4_forward (FLOAT64)
- quarter_num (INT64)
- quarterly_avg_close (FLOAT64)
- quarterly_avg_high (FLOAT64)
- quarterly_avg_low (FLOAT64)
- quarterly_avg_open (FLOAT64)
- quarterly_avg_volume (FLOAT64)
- symbol (STRING)
- year_month (STRING)
- year_quarter (STRING)
- year_val (INT64)
schema_hash: ca13aab0a3e34c6baa11c8cbd6bdf61ed004c023101b0570d9cbd2c31d7bdf9d

---
# Table Summary: global_markets_analysis_return

## Overall Dataset Characteristics

**Total Rows:** 2,184

This table contains comprehensive monthly and quarterly market analysis data for global equity ETFs spanning from 2012 to 2025 (approximately 14 years). The dataset tracks 13 different market symbols across 168 unique months, with complete data coverage (no nulls) for base metrics, but intentional nulls in forward-looking performance indicators for recent periods.

**Data Quality:**
- Excellent completeness for historical data (0% nulls for all base columns)
- Forward-looking metrics (pct_change_q*_forward) have expected nulls for recent periods (1.79% to 7.14%)
- All records have complete temporal and identifier information
- High cardinality in price-related columns indicates granular tracking

**Notable Patterns:**
- Data covers major global markets including US (ACWI), emerging markets (EEM), and country-specific ETFs
- Two exchanges represented: ARCX (primary) and XNAS
- Time-series data with monthly granularity, aggregated to quarterly metrics
- Forward-looking percentage changes calculated for up to 4 quarters ahead

## Column Details

### Temporal Columns

**month_date (DATE)**
- Primary date dimension with 168 unique months
- Spans 2012-01-01 to 2025-09-01 (14 years)
- No nulls, complete coverage
- Use for: Time-series analysis, date filtering, chronological ordering

**year_month (STRING)**
- Format: "YYYY-MM" (e.g., "2025-09", "2017-12")
- 168 unique values matching month_date
- Alternative text-based date representation
- Use for: Date grouping, string-based filtering

**year_quarter (STRING)**
- Format: "YYYY-Q#" (e.g., "2020-Q4", "2013-Q3")
- 56 unique values (14 years × 4 quarters)
- Directly maps to quarter_num
- Use for: Quarterly aggregations, period comparisons

**quarter_num (INT64)**
- Values: 1, 2, 3, 4 only
- Represents calendar quarter within year
- Use for: Seasonal analysis, quarter-based filtering

**year_val (INT64)**
- Range: 2012 to 2025
- 14 unique years
- Use for: Year-over-year comparisons, annual trends

### Identifier Columns

**symbol (STRING)**
- 13 unique ETF ticker symbols
- Values include: ACWI (global), EEM (emerging markets), EPI, EWA (Australia), EWG (Germany), EWJ (Japan), EWQ (France), EWU (UK), EWW (Mexico), EWY (South Korea), EWZ (Brazil), and others
- No nulls, complete coverage
- Use for: Filtering by market/country, grouping by security

**exchange (STRING)**
- Only 2 values: ARCX (primary), XNAS
- ARCX = NYSE Arca (most common)
- XNAS = NASDAQ
- Use for: Exchange-based filtering (limited utility given low cardinality)

### Monthly Price Metrics

**monthly_avg_close (FLOAT64)**
- Range: 8.99 to 141.72
- 2,173 unique values (high granularity)
- Average closing price for the month
- Use for: Price analysis, month-end valuations, trend identification

**monthly_avg_open (FLOAT64)**
- Range: 8.99 to 141.77
- 2,180 unique values
- Average opening price for the month
- Use for: Gap analysis, monthly entry points

**monthly_avg_high (FLOAT64)**
- Range: 9.03 to 142.22
- 2,180 unique values
- Average high price for the month
- Use for: Resistance levels, volatility analysis

**monthly_avg_low (FLOAT64)**
- Range: 8.94 to 141.16
- 2,180 unique values
- Average low price for the month
- Use for: Support levels, risk assessment

**monthly_avg_volume (FLOAT64)**
- Range: 93,155 to 112,784,014
- 2,184 unique values (all unique per row)
- Extreme variance across securities
- Use for: Liquidity analysis, trading activity patterns

### Quarterly Aggregated Metrics

**quarterly_avg_close (FLOAT64)**
- Range: 9.17 to 140.35
- 728 unique values
- Three-month rolling average close
- Use for: Smoothed trend analysis, quarterly performance

**quarterly_avg_open (FLOAT64)**
- Range: 9.17 to 140.40
- 728 unique values
- Three-month rolling average open

**quarterly_avg_high (FLOAT64)**
- Range: 9.21 to 141.01
- 727 unique values
- Three-month rolling average high

**quarterly_avg_low (FLOAT64)**
- Range: 9.14 to 139.64
- 728 unique values
- Three-month rolling average low

**quarterly_avg_volume (FLOAT64)**
- Range: 137,927 to 96,886,293
- 728 unique values
- Three-month rolling average volume

### Forward-Looking Performance Indicators

**pct_change_q1_forward (FLOAT64)**
- Range: -32.92% to 188.32%
- 1.79% nulls (39 rows) - most recent data
- Percentage change one quarter ahead
- Use for: Short-term performance prediction, next-quarter analysis

**pct_change_q2_forward (FLOAT64)**
- Range: -40.39% to 320.35%
- 3.57% nulls (78 rows)
- Percentage change two quarters ahead
- Use for: Medium-term trend analysis

**pct_change_q3_forward (FLOAT64)**
- Range: -39.40% to 339.59%
- 5.36% nulls (117 rows)
- Percentage change three quarters ahead

**pct_change_q4_forward (FLOAT64)**
- Range: -46.23% to 354.65%
- 7.14% nulls (156 rows)
- Percentage change four quarters ahead
- Use for: Annual performance projections

## Query Considerations

### Optimal Filtering Columns
- **symbol**: Primary filter for specific markets/countries
- **year_val**: Year-based analysis
- **year_quarter**: Quarterly reporting periods
- **month_date**: Date range queries
- **exchange**: Limited utility (only 2 values)

### Optimal Grouping/Aggregation Columns
- **symbol**: Compare performance across markets
- **year_val**: Annual trends
- **quarter_num**: Seasonal patterns
- **year_quarter**: Quarterly comparisons
- **exchange**: Exchange-level analysis

### Join Keys and Relationships
- **symbol**: Can join to security master tables, company information
- **month_date/year_month**: Time-based joins to economic indicators, other time-series data
- **exchange**: Join to exchange reference data

### Data Quality Considerations

1. **Null Handling**: Forward-looking columns have expected nulls for recent periods; use `IS NOT NULL` filters or `COALESCE` for complete analysis

2. **Time Alignment**: Multiple date representations (month_date, year_month, year_quarter) - choose appropriate granularity

3. **Volume Variance**: Massive range (93K to 112M) - consider LOG transformations or normalized metrics

4. **Price Ranges**: Different symbols have vastly different price ranges (8.99 to 141.72) - percentage changes more comparable than absolute prices

5. **Forward-Looking Metrics**: Increasing null percentages in q1→q4 forward changes reflect data recency; queries should account for varying available horizons

6. **Quarterly vs Monthly**: Decide whether to use monthly granularity (more precise) or quarterly aggregates (smoother trends)

## Keywords

global markets, ETF analysis, stock market returns, equity performance, international markets, emerging markets, country ETFs, monthly returns, quarterly performance, forward returns, market indices, ACWI, EEM, iShares, time series analysis, financial data, trading volume, price movements, percentage changes, market trends, investment analysis, portfolio returns, global equities, NYSE Arca, NASDAQ, Australia EWA, Germany EWG, Japan EWJ, France EWQ, UK EWU, Mexico EWW, South Korea EWY, Brazil EWZ

## Table and Column Documentation

**Table Comment:** Not provided in the source data

**Column Comments:** No column-level comments were provided in the source analysis. All descriptions above are inferred from the data values and column names.