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
# Summary: Agriculture Commodities Summary Table

## Overall Dataset Characteristics

**Total Rows:** 36

This table contains **performance metrics for agricultural commodity futures** across different time periods. The dataset represents a comprehensive analysis of 9 different agricultural commodities (corn, cotton, eggs, feeder cattle, live cattle, poultry, soybeans, sugar, and wheat) measured over 4 distinct time periods (12 weeks, 6 months, 1 year, and 5 years).

**Data Quality:** Excellent - no null values detected across all columns (0% null percentage for all fields). Each commodity appears to be analyzed across multiple time periods, creating a complete performance matrix.

**Notable Patterns:**
- The data captures both historical (starting from 2020-12-18 for 5-year periods) and recent trading periods (up to 2025-12-16)
- Performance metrics range dramatically, from extreme losses (-40.88% return) to extraordinary gains (539.44% return over 5 years)
- Trading days vary significantly based on time period (56 to 1,039 days)
- Most commodities show relatively balanced win rates around 45-55%

## Column Details

### **commodity_name** (STRING)
- **Type:** Categorical identifier
- **Values:** 9 unique commodities (corn, cotton, eggs us, feeder cattle, live cattle, poultry, soybeans, sugar, wheat)
- **No nulls:** Complete data
- **Purpose:** Primary dimension for filtering and grouping commodity performance
- **Note:** Uses lowercase naming convention; "eggs us" includes country specification

### **time_period** (STRING)
- **Type:** Categorical time frame identifier
- **Values:** 4 distinct periods (12_weeks, 1_year, 5_years, 6_months)
- **Format:** Underscore-separated with time unit
- **No nulls:** Complete data
- **Purpose:** Key dimension for time-based analysis and comparison

### **commodity_unit** (STRING)
- **Type:** Measurement unit specification
- **Values:** 5 unique units (BRL/Kgs, USD/Dozen, USd/BU, USd/Bu, USd/Lbs)
- **No nulls:** Complete data
- **Note:** Mixed case conventions (USd vs USD); BU/Bu both represent bushels; BRL indicates Brazilian Real for sugar
- **Purpose:** Essential for understanding price magnitude and currency context

### **period_start_date** (DATE)
- **Type:** Date
- **Values:** 4 unique dates (2020-12-18, 2024-12-18, 2025-06-18, 2025-09-25)
- **Range:** December 2020 to September 2025
- **No nulls:** Complete data
- **Purpose:** Defines beginning of analysis period; useful for temporal filtering

### **period_end_date** (DATE)
- **Type:** Date
- **Values:** 4 unique dates (2024-12-17, 2025-06-17, 2025-09-24, 2025-12-16)
- **Range:** December 2024 to December 2025
- **No nulls:** Complete data
- **Purpose:** Defines end of analysis period; completes time range definition

### **positive_days** (INT64)
- **Type:** Integer count
- **Range:** 16 to 533 days
- **Unique Values:** 28
- **No nulls:** Complete data
- **Purpose:** Counts days with positive price movement; contributes to win rate calculation

### **negative_days** (INT64)
- **Type:** Integer count
- **Range:** 15 to 519 days
- **Unique Values:** 30
- **No nulls:** Complete data
- **Purpose:** Counts days with negative price movement; contributes to loss rate calculation

### **trading_days** (INT64)
- **Type:** Integer count
- **Range:** 56 to 1,039 days
- **Unique Values:** 23
- **No nulls:** Complete data
- **Purpose:** Total business days in period; sum of positive, negative, and neutral days
- **Note:** Varies by time period length; approximately 58 days for 12_weeks, 1000+ for 5_years

### **neutral_days** (INT64)
- **Type:** Integer count
- **Range:** 0 to 858 days
- **Common Values:** Mostly low (0, 1, 3, 5, 6), but can reach 858
- **No nulls:** Complete data
- **Purpose:** Days with no price change; relatively rare in most periods

### **total_return_pct** (FLOAT64)
- **Type:** Percentage (as float)
- **Range:** -40.88% to 539.44%
- **All Unique Values:** 36 unique values
- **No nulls:** Complete data
- **Purpose:** Overall percentage return for the period; key performance metric
- **Notable:** Extremely wide range indicates high volatility across commodities and periods

### **avg_daily_return_pct** (FLOAT64)
- **Type:** Percentage (as float)
- **Range:** -0.7379% to 0.3445%
- **All Unique Values:** 36 unique values
- **No nulls:** Complete data
- **Purpose:** Average daily percentage return; normalized performance metric
- **Note:** Can be used to compare performance across different time periods

### **volatility_pct** (FLOAT64)
- **Type:** Percentage (as float)
- **Range:** 5.9% to 93.4%
- **All Unique Values:** 36 unique values
- **No nulls:** Complete data
- **Purpose:** Measure of price fluctuation/risk; standard deviation of returns
- **Note:** Higher values indicate more volatile/risky commodities

### **total_price_change** (NUMERIC)
- **Type:** Numeric (absolute price change)
- **Range:** -1.1 to 116.38
- **All Unique Values:** 36 unique values
- **No nulls:** Complete data
- **Purpose:** Absolute price difference between period start and end
- **Note:** Units vary by commodity (see commodity_unit); not directly comparable across commodities

### **win_rate_pct** (FLOAT64)
- **Type:** Percentage (as float)
- **Range:** 9.6% to 69.1%
- **Unique Values:** 33
- **No nulls:** Complete data
- **Purpose:** Percentage of trading days with positive returns
- **Note:** Calculated as (positive_days / trading_days * 100)

### **worst_day_change** (NUMERIC)
- **Type:** Numeric (negative values)
- **Range:** -34.5 to -0.22
- **Unique Values:** 34
- **No nulls:** Complete data
- **Purpose:** Largest single-day price decline; downside risk metric
- **Note:** All values are negative; magnitude varies by commodity unit

### **avg_daily_price_change** (FLOAT64)
- **Type:** Float (can be positive or negative)
- **Range:** -0.9286 to 0.911
- **All Unique Values:** 36 unique values
- **No nulls:** Complete data
- **Purpose:** Average absolute daily price change
- **Note:** Complements avg_daily_return_pct with absolute price movement

### **best_day_change** (NUMERIC)
- **Type:** Numeric (positive values)
- **Range:** 0.25 to 8.57
- **Unique Values:** 34
- **No nulls:** Complete data
- **Purpose:** Largest single-day price gain; upside potential metric
- **Note:** All values are positive; magnitude varies by commodity unit

### **period_start_price** (NUMERIC)
- **Type:** Numeric (positive values)
- **Range:** Varies by commodity (e.g., 5.71 to 1074.75)
- **All Unique Values:** 36 unique values
- **No nulls:** Complete data
- **Purpose:** Commodity price at beginning of period; baseline for performance calculation

### **period_end_price** (NUMERIC)
- **Type:** Numeric (positive values)
- **Range:** Varies by commodity (e.g., 8.3 to 343.18)
- **All Unique Values:** 36 unique values
- **No nulls:** Complete data
- **Purpose:** Commodity price at end of period; used to calculate total returns

## Potential Query Considerations

### **Best Columns for Filtering:**
- **commodity_name:** Filter by specific commodities or commodity groups
- **time_period:** Analyze specific time horizons (short vs long term)
- **period_start_date / period_end_date:** Filter by specific date ranges
- **total_return_pct:** Find best/worst performing periods (WHERE total_return_pct > threshold)
- **volatility_pct:** Identify high-risk or stable commodities

### **Best Columns for Grouping/Aggregation:**
- **commodity_name:** Compare performance across commodities
- **time_period:** Compare short-term vs long-term performance
- **commodity_unit:** Group by currency/measurement type
- Can calculate averages of return metrics across groups

### **Potential Join Keys:**
- **commodity_name + time_period:** Unique combination for joining with other commodity datasets
- **period_start_date / period_end_date:** Join with external economic indicators or market data
- No explicit primary key, but commodity_name + time_period appears to form a composite key

### **Data Quality Considerations:**
- **Unit Consistency:** Be aware that commodity_unit varies (BRL vs USD, different weight measures)
- **Price Comparability:** Direct price comparisons require same units; use percentage returns instead
- **Time Period Lengths:** trading_days varies significantly; normalize by using daily metrics
- **Case Sensitivity:** "USd/BU" vs "USd/Bu" may need standardization
- **Date Ranges:** Some dates are in the future (2025); verify if projections or historical data
- **Extreme Values:** 539% return suggests outliers; consider filtering for typical analysis

### **Useful Calculations:**
- Sharpe ratio approximation: avg_daily_return_pct / volatility_pct
- Risk-adjusted returns across commodities
- Correlation between volatility and returns
- Win/loss ratio: positive_days / negative_days
- Verify: win_rate_pct ≈ (positive_days / trading_days) * 100

## Keywords

agriculture, commodities, futures, trading, performance metrics, corn, wheat, soybeans, cotton, cattle, livestock, sugar, eggs, poultry, price analysis, returns, volatility, risk metrics, win rate, daily returns, time series, financial analysis, market data, commodity prices, trading days, price changes, best day, worst day, agricultural economics, commodity trading, investment performance

## Table and Column Documentation

**Table Comment:** Not provided

**Column Comments:** Not provided