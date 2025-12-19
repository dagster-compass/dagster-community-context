---
columns:
- avg_daily_price_change (FLOAT64)
- avg_daily_return_pct (FLOAT64)
- best_day_change (NUMERIC)
- commodity_name (STRING)
- commodity_unit (STRING)
- negative_days (INT64)
- neutral_days (INT64)
- period_end_date (DATE)
- period_end_price (NUMERIC)
- period_start_date (DATE)
- period_start_price (NUMERIC)
- positive_days (INT64)
- time_period (STRING)
- total_price_change (NUMERIC)
- total_return_pct (FLOAT64)
- trading_days (INT64)
- volatility_pct (FLOAT64)
- win_rate_pct (FLOAT64)
- worst_day_change (NUMERIC)
schema_hash: bee04bb62ee4eed80db7ea406e53b2e3731c6b6af82f1944f44436120bd6f61c

---
# Table Summary: compass-bigquery-demo.economic_data.input_commodities_summary

## Overall Dataset Characteristics

**Total Rows:** 92

**General Description:** This table contains commodity price performance summaries across different time periods. It tracks 20 different commodities with various trading metrics including returns, volatility, and daily price movements. The data represents a time-series analysis of commodity performance with multiple time horizons (12 weeks, 6 months, 1 year, and 5 years).

**Data Quality:** 
- Excellent completeness - 0% null values across all columns
- Data spans from December 2020 to December 2025
- Consistent data structure with well-defined metrics
- All commodities have multiple time period snapshots

**Notable Patterns:**
- 20 unique commodities tracked with different units of measurement (USD, CNY, various weight/volume units)
- 4 distinct time periods analyzed: 12_weeks, 6_months, 1_year, 5_years
- Wide range of returns: from -36.59% to +556.11%
- Volatility ranges dramatically from 1.92% to over 190,000%
- Trading days vary by period: 39 to 1,051 days

## Column Details

### **commodity_name** (STRING)
- **Type:** Categorical identifier
- **Unique Values:** 20 commodities including aluminum, bitumen, copper, gallium, germanium, gold, iron ore, lead, lithium, lumber, and others
- **Null Pattern:** No nulls (0%)
- **Usage:** Primary grouping/filtering dimension for commodity analysis

### **commodity_unit** (STRING)
- **Type:** Unit of measurement
- **Unique Values:** 10 different units
- **Common Values:** CNY/T, CNY/Kg, USD/T, USD/Lbs, USD/t.oz, USD/1000 board feet, USD Cents/Kg, CNY/mtu
- **Note:** Mix of currencies (USD, CNY) and measurement units (T=ton, Kg=kilogram, Lbs=pounds, t.oz=troy ounce, mtu=metric ton unit)
- **Usage:** Important for understanding price scales and cross-commodity comparisons

### **time_period** (STRING)
- **Type:** Categorical time window
- **Unique Values:** 4 periods
- **Values:** 12_weeks, 6_months, 1_year, 5_years
- **Usage:** Key dimension for temporal analysis and comparing short vs long-term performance

### **period_start_date** (DATE)
- **Type:** Date
- **Unique Values:** 6 distinct start dates
- **Range:** 2020-12-18 to 2025-09-25
- **Common Values:** 2020-12-18 (5-year lookbacks), 2024-12-18, 2025-06-18, 2025-09-25
- **Usage:** Time-based filtering and trend analysis

### **period_end_date** (DATE)
- **Type:** Date
- **Unique Values:** 7 distinct end dates
- **Range:** 2023-10-31 to 2025-12-16
- **Common Values:** 2025-12-16, 2025-09-24, 2025-06-17
- **Usage:** Defines analysis window endpoint; useful for current/recent data filtering

### **trading_days** (INT64)
- **Type:** Count of trading days
- **Range:** 39 to 1,051 days
- **Unique Values:** 37 different counts
- **Pattern:** Correlates with time_period (longer periods = more trading days)
- **Usage:** Normalizing metrics, understanding data completeness

### **positive_days** (INT64)
- **Type:** Count of days with price increases
- **Range:** 0 to 550 days
- **Unique Values:** 57 different counts
- **Usage:** Win/loss analysis, performance consistency metrics

### **negative_days** (INT64)
- **Type:** Count of days with price decreases
- **Range:** 0 to 517 days
- **Unique Values:** 57 different counts
- **Usage:** Risk assessment, downside frequency analysis

### **neutral_days** (INT64)
- **Type:** Count of days with no price change
- **Range:** 0 to 877 days
- **Unique Values:** 40 different counts
- **Pattern:** Some commodities (like manganese) show very high neutral days (711 out of 748)
- **Usage:** Liquidity/activity indicator

### **total_return_pct** (FLOAT64)
- **Type:** Percentage return over period
- **Range:** -36.59% to +556.11%
- **Unique Values:** 83 distinct returns
- **Distribution:** Wide variance; includes both significant gains and losses
- **Usage:** Primary performance metric for filtering top/bottom performers

### **volatility_pct** (FLOAT64)
- **Type:** Price volatility measure (likely standard deviation)
- **Range:** 1.92% to 190,956.72%
- **Unique Values:** 78 distinct values
- **Note:** Extreme outlier at 190,956.72% suggests highly volatile or thin-market commodity
- **Usage:** Risk assessment, identifying stable vs volatile commodities

### **avg_daily_return_pct** (FLOAT64)
- **Type:** Average daily percentage return
- **Range:** -0.3152% to 1,446.62%
- **Unique Values:** 78 distinct values
- **Usage:** Normalized performance comparison across different time periods

### **win_rate_pct** (FLOAT64)
- **Type:** Percentage of trading days with positive returns
- **Range:** 0% to 64.4%
- **Unique Values:** 72 distinct values
- **Pattern:** Most values cluster around 40-60% (near random walk)
- **Usage:** Consistency analysis, trend strength indicator

### **total_price_change** (NUMERIC)
- **Type:** Absolute price change in commodity units
- **Unique Values:** 78 distinct values
- **Note:** Scale varies dramatically by commodity unit (e.g., cents vs thousands)
- **Usage:** Absolute magnitude analysis (must consider commodity_unit)

### **avg_daily_price_change** (FLOAT64)
- **Type:** Average daily absolute price change
- **Range:** -130.93 to 415.09
- **Unique Values:** 80 distinct values
- **Usage:** Daily movement magnitude analysis

### **worst_day_change** (NUMERIC)
- **Type:** Largest single-day price decline
- **Unique Values:** 79 distinct values
- **Usage:** Downside risk assessment, worst-case scenarios

### **best_day_change** (NUMERIC)
- **Type:** Largest single-day price increase
- **Unique Values:** 72 distinct values
- **Usage:** Upside potential analysis, volatility events

### **period_start_price** (NUMERIC)
- **Type:** Commodity price at period start
- **Unique Values:** 80 distinct values
- **Range:** Varies widely by commodity and unit
- **Usage:** Price level context, calculating derived metrics

### **period_end_price** (NUMERIC)
- **Type:** Commodity price at period end
- **Unique Values:** 80 distinct values
- **Range:** Varies widely by commodity and unit
- **Usage:** Current price reference, return validation

## Query Considerations

### **Good for Filtering:**
- `commodity_name` - Essential for commodity-specific analysis
- `time_period` - Critical for comparing different time horizons
- `period_end_date` - For getting most recent data
- `total_return_pct` - Finding best/worst performers
- `volatility_pct` - Risk-based filtering
- `win_rate_pct` - Consistency filtering

### **Good for Grouping/Aggregation:**
- `commodity_name` - Primary grouping dimension
- `time_period` - Temporal aggregation
- `commodity_unit` - Currency/unit-based analysis
- Combination: commodity_name + time_period for complete performance view

### **Potential Join Keys:**
- `commodity_name` - Could join to commodity metadata tables
- `period_start_date`, `period_end_date` - Time-based joins to market events or economic indicators
- No obvious primary key - combination of (commodity_name, time_period, period_start_date) likely unique

### **Data Quality Considerations:**
- **Unit Awareness:** Always consider `commodity_unit` when comparing prices across commodities
- **Scale Variance:** Metrics like volatility and returns span extreme ranges - use appropriate filtering
- **Time Period Context:** Different time_periods have different trading_days - normalize when comparing
- **Neutral Days:** High neutral_days (like manganese with 711/748) may indicate data quality issues or illiquid markets
- **Outliers:** Extreme volatility values (190,000%+) may need investigation or exclusion
- **Currency Mix:** CNY vs USD prices not directly comparable without exchange rates

### **Common Query Patterns:**
1. **Latest performance:** Filter by recent period_end_date
2. **Top performers:** ORDER BY total_return_pct DESC with time_period filter
3. **Risk-adjusted returns:** Compare total_return_pct / volatility_pct
4. **Consistency analysis:** Filter by win_rate_pct > 55%
5. **Cross-period comparison:** GROUP BY commodity_name with different time_periods
6. **Volatility screening:** Filter on volatility_pct ranges

## Keywords

commodities, commodity prices, trading performance, returns, volatility, metals, precious metals, industrial commodities, aluminum, copper, gold, silver, lead, lithium, lumber, iron ore, bitumen, manganese, polypropylene, gallium, germanium, time series, financial data, price analysis, trading days, win rate, daily returns, price changes, USD, CNY, market data, economic indicators, raw materials, 12 weeks, 6 months, 1 year, 5 years, performance metrics, risk metrics

## Table and Column Documentation

**Table Comment:** Not provided

**Column Comments:** Not provided

---

*Note: This table appears to be a pre-aggregated summary table designed for commodity performance analysis dashboards and reporting. Each row represents a summary of one commodity's performance over a specific time period.*