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
# Comprehensive Data Summary: Energy Commodities Summary Table

## Overall Dataset Characteristics

**Total Rows:** 24

**General Description:** This table contains aggregated performance metrics for energy commodities over different time periods. It appears to be a pre-calculated summary table designed for quick access to commodity trading statistics and returns analysis.

**Data Quality:** Excellent - no null values in any column. All 24 rows contain complete data across all 19 columns.

**Notable Patterns:**
- The dataset provides a comprehensive view across 6 different energy commodities
- Data covers 4 distinct time periods (12 weeks, 6 months, 1 year, and 5 years)
- This creates a 6 × 4 matrix structure (6 commodities × 4 time periods = 24 rows)
- Time periods are aligned to specific end dates (Dec 17, 2024; June 17, 2025; Sept 24, 2025; Dec 16, 2025)
- The 5-year lookback period starts from December 18, 2020

---

## Column Details

### **time_period** (STRING)
- **Type:** Categorical dimension
- **Values:** 4 distinct periods: `12_weeks`, `6_months`, `1_year`, `5_years`
- **Null Values:** None (0%)
- **Purpose:** Primary grouping dimension for time-based analysis
- **Pattern:** Uses underscore naming convention; represents rolling time windows

### **commodity_name** (STRING)
- **Type:** Categorical dimension
- **Values:** 6 commodities: `brent`, `coal`, `crude oil`, `gasoline`, `heating oil`, `natural gas`
- **Null Values:** None (0%)
- **Purpose:** Primary grouping dimension for commodity-based analysis
- **Pattern:** Lowercase naming; represents major energy trading commodities
- **Note:** "Brent" likely refers to Brent Crude Oil; "crude oil" may refer to WTI (West Texas Intermediate)

### **period_start_date** (DATE)
- **Type:** Date dimension
- **Values:** 4 unique dates (2020-12-18, 2024-12-18, 2025-06-18, 2025-09-25)
- **Null Values:** None (0%)
- **Pattern:** Each date corresponds to a specific time_period lookback
- **Relationship:** Earlier dates = longer time periods (5-year period starts in 2020)

### **period_end_date** (DATE)
- **Type:** Date dimension
- **Values:** 4 unique dates (2024-12-17, 2025-06-17, 2025-09-24, 2025-12-16)
- **Null Values:** None (0%)
- **Pattern:** Aligned to specific market snapshots
- **Note:** Latest end date suggests data is current through December 16, 2025

### **commodity_unit** (STRING)
- **Type:** Categorical/metadata
- **Values:** 4 different units: `USD/Bbl` (barrel), `USD/Gal` (gallon), `USD/MMBtu` (Million BTU), `USD/T` (ton)
- **Null Values:** None (0%)
- **Purpose:** Indicates pricing unit for each commodity
- **Pattern:** 
  - Oil products (Brent, Crude Oil): USD/Bbl
  - Refined products (Gasoline, Heating Oil): USD/Gal
  - Natural Gas: USD/MMBtu
  - Coal: USD/T

### **trading_days** (INT64)
- **Type:** Count metric
- **Range:** 59 to 1,077 days
- **Null Values:** None (0%)
- **Pattern:** Varies by time_period (12 weeks ≈ 59 days, 5 years ≈ 1,077 days)
- **Purpose:** Total number of trading days in the period
- **Note:** Not calendar days; excludes weekends and market holidays

### **positive_days** (INT64)
- **Type:** Count metric
- **Range:** 25 to 580 days
- **Null Values:** None (0%)
- **Purpose:** Number of days with positive price changes
- **Pattern:** Generally proportional to trading_days; used to calculate win rates

### **negative_days** (INT64)
- **Type:** Count metric
- **Range:** 27 to 513 days
- **Null Values:** None (0%)
- **Purpose:** Number of days with negative price changes
- **Pattern:** Generally proportional to trading_days; complement to positive_days

### **neutral_days** (INT64)
- **Type:** Count metric
- **Range:** 0 to 64 days
- **Null Values:** None (0%)
- **Purpose:** Days with no price change
- **Pattern:** Relatively rare (many commodities show 0 neutral days); small percentage of total trading days
- **Note:** positive_days + negative_days + neutral_days = trading_days

### **total_return_pct** (FLOAT64)
- **Type:** Performance metric (percentage)
- **Range:** -28.35% to +62.94%
- **Null Values:** None (0%)
- **Purpose:** Total percentage return over the period
- **Pattern:** High variability; natural gas shows highest volatility; longer periods tend to show more extreme returns
- **Formula:** ((period_end_price - period_start_price) / period_start_price) × 100

### **volatility_pct** (FLOAT64)
- **Type:** Risk metric (percentage)
- **Range:** 13.86% to 79.91%
- **Null Values:** None (0%)
- **Purpose:** Measure of price variability/risk
- **Pattern:** Natural gas shows highest volatility (79.91%); some commodities are more stable
- **Note:** Likely annualized standard deviation of returns

### **avg_daily_return_pct** (FLOAT64)
- **Type:** Performance metric (percentage)
- **Range:** -0.3769% to +0.6062% per day
- **Null Values:** None (0%)
- **Purpose:** Average daily percentage return
- **Pattern:** Generally small values; compounds over time to total_return_pct

### **win_rate_pct** (FLOAT64)
- **Type:** Performance metric (percentage)
- **Range:** 40.9% to 54.9%
- **Null Values:** None (0%)
- **Purpose:** Percentage of trading days that were positive
- **Formula:** (positive_days / trading_days) × 100
- **Pattern:** Generally clusters around 50%; slight variations indicate directional bias

### **total_price_change** (NUMERIC)
- **Type:** Absolute price metric
- **Values:** Highly varied (24 unique values)
- **Null Values:** None (0%)
- **Purpose:** Absolute dollar change in commodity price
- **Pattern:** Units vary by commodity_unit; can be positive or negative
- **Note:** Not directly comparable across commodities due to different units

### **avg_daily_price_change** (FLOAT64)
- **Type:** Absolute price metric
- **Range:** -0.1886 to +0.0847 (units vary)
- **Null Values:** None (0%)
- **Purpose:** Average daily price change in absolute terms
- **Pattern:** Small decimal values; units correspond to commodity_unit

### **worst_day_change** (NUMERIC)
- **Type:** Extreme value metric (negative)
- **Values:** 23 unique values (one duplicate)
- **Null Values:** None (0%)
- **Purpose:** Largest single-day price drop
- **Pattern:** All negative or zero; shows downside risk
- **Note:** Natural gas shows large swings (e.g., -$2.05)

### **best_day_change** (NUMERIC)
- **Type:** Extreme value metric (positive)
- **Values:** 23 unique values (one duplicate)
- **Null Values:** None (0%)
- **Purpose:** Largest single-day price gain
- **Pattern:** All positive; shows upside potential
- **Note:** Helps assess single-day volatility range

### **period_start_price** (NUMERIC)
- **Type:** Reference price metric
- **Values:** 24 unique values (one per row)
- **Null Values:** None (0%)
- **Purpose:** Commodity price at period start
- **Pattern:** Units correspond to commodity_unit; used as baseline for return calculations
- **Range:** Varies widely by commodity (e.g., Natural Gas: $2-4, Coal: $100+)

### **period_end_price** (NUMERIC)
- **Type:** Reference price metric
- **Values:** 24 unique values (one per row)
- **Null Values:** None (0%)
- **Purpose:** Commodity price at period end
- **Pattern:** Units correspond to commodity_unit; reflects current/recent prices
- **Relationship:** period_end_price - period_start_price = total_price_change

---

## Potential Query Considerations

### **Best Columns for Filtering:**
1. **commodity_name** - Filter by specific energy commodities
2. **time_period** - Filter by analysis timeframe (short-term vs long-term)
3. **period_end_date** - Filter by specific reporting dates
4. **commodity_unit** - Filter by pricing unit type

### **Best Columns for Grouping/Aggregation:**
1. **commodity_name** - Compare performance across commodities
2. **time_period** - Compare performance across different timeframes
3. **commodity_unit** - Group by pricing methodology
4. **period_end_date** - Trend analysis over time

### **Key Aggregation Opportunities:**
- Average returns by commodity across all time periods
- Volatility comparisons across commodities
- Win rate analysis by time period
- Best/worst performing commodities by various metrics

### **Potential Join Keys:**
- **commodity_name + time_period** - Unique identifier for each row
- Could join to detailed daily price data tables
- Could join to commodity metadata tables (e.g., sector, market exchange)

### **Data Quality Considerations for Queries:**

1. **Unit Awareness:** 
   - Do NOT directly compare price_change values across different commodity_units
   - Use percentage-based metrics (total_return_pct) for cross-commodity comparisons

2. **Time Period Consistency:**
   - Each commodity has exactly one row per time_period
   - No missing combinations in the 6×4 matrix

3. **Calculated Field Validation:**
   - Verify: positive_days + negative_days + neutral_days = trading_days
   - Verify: total_return_pct ≈ (total_price_change / period_start_price) × 100

4. **Date Logic:**
   - period_end_date is always after period_start_date
   - Different time_periods have non-overlapping date ranges

5. **Percentage vs Absolute Values:**
   - Use *_pct columns for relative comparisons
   - Use absolute price changes for unit-specific analysis

6. **Volatility Context:**
   - Higher volatility_pct indicates riskier commodities
   - Should be considered alongside return metrics

---

## Keywords

Energy commodities, oil prices, natural gas, coal, Brent crude, WTI crude oil, gasoline prices, heating oil, commodity trading, price returns, volatility analysis, trading performance, win rate, daily returns, price movements, energy markets, commodity futures, financial performance, risk metrics, time series analysis, rolling windows, 12-week performance, annual returns, 5-year returns, USD pricing, barrel pricing, gallon pricing, MMBtu, ton pricing, trading days, positive days, negative days, best day, worst day, total return, average daily return, period analysis, market performance, energy sector

---

## Table and Column Documentation

**Table Comment:** Not provided

**Column Comments:** Not provided

This table appears to be a business intelligence summary table designed for quick performance lookups and comparative analysis of energy commodity trading metrics across different time horizons.