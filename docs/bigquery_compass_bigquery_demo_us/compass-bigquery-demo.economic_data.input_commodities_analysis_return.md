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
# Table Summary: input_commodities_analysis_return

## Overall Dataset Characteristics

This table contains **2,967 rows** of commodity pricing data with forward-looking percentage change metrics. The dataset spans from **2012 to 2025** (14 years) and covers **20 different commodities** including metals (aluminum, copper, gold, silver, zinc, lead), specialty metals (gallium, germanium, lithium, titanium), industrial materials (iron ore, lumber, bitumen), and petrochemicals (polypropylene).

**Data Quality:**
- Generally high-quality data with no nulls in core columns
- Forward-looking percentage change columns have minimal null values (0.74% to 2.97%), likely representing end-of-time-series data points
- 167 unique months of data, suggesting approximately 14 years of monthly observations
- Consistent temporal structure with quarterly aggregations

**Notable Patterns:**
- Each commodity is tracked with monthly average prices and quarterly aggregated prices
- Forward-looking percentage changes calculated for 1-4 quarters ahead
- Prices vary dramatically by commodity type and unit (ranging from $2 to $586,773)
- Multiple currency/unit standards (USD and CNY, various weight measurements)

## Column Details

### **commodity_name** (STRING)
- **Type:** Categorical identifier
- **Nulls:** 0%
- **Cardinality:** 20 unique commodities
- **Purpose:** Primary grouping dimension for commodity type
- **Values Include:** aluminum, bitumen, copper, gallium, germanium, gold, iron ore, lead, lithium, lumber, polypropylene, silver, titanium, zinc
- **Query Use:** Primary filtering and grouping column

### **month_date** (DATE)
- **Type:** Temporal identifier (first day of month)
- **Nulls:** 0%
- **Range:** 167 unique months spanning 2012-2025
- **Format:** YYYY-MM-01 (first of month)
- **Query Use:** Time-series filtering, chronological ordering, date-based joins

### **commodity_unit** (STRING)
- **Type:** Measurement unit descriptor
- **Nulls:** 0%
- **Cardinality:** 10 unique units
- **Values:** CNY/KG, CNY/Kg, CNY/T, CNY/mtu, USD Cents/Kg, USD/1000 board feet, USD/KG, USD/Lbs, USD/T, USD/t.oz
- **Note:** Case sensitivity in units (CNY/KG vs CNY/Kg)
- **Query Use:** Important for price interpretation and unit normalization

### **year_month** (STRING)
- **Type:** Temporal identifier (formatted string)
- **Nulls:** 0%
- **Format:** YYYY-MM
- **Cardinality:** 167 unique values
- **Query Use:** Alternative time filtering, human-readable grouping

### **year_quarter** (STRING)
- **Type:** Quarterly period identifier
- **Nulls:** 0%
- **Format:** YYYY-QN (e.g., 2012-Q1)
- **Cardinality:** 56 unique quarters
- **Query Use:** Quarterly aggregation and filtering

### **quarter_num** (INT64)
- **Type:** Quarter indicator
- **Nulls:** 0%
- **Range:** 1-4
- **Purpose:** Isolates quarter number from year
- **Query Use:** Seasonal pattern analysis, quarter-specific filtering

### **monthly_avg_price** (FLOAT64)
- **Type:** Continuous numeric (price measurement)
- **Nulls:** 0%
- **Range:** 2.0046 to 586,772.73
- **Cardinality:** 2,907 unique values (highly granular)
- **Purpose:** Core price metric at monthly granularity
- **Query Use:** Primary measure for calculations, aggregations, and trend analysis

### **year_val** (INT64)
- **Type:** Temporal identifier (year)
- **Nulls:** 0%
- **Range:** 2012-2025
- **Cardinality:** 14 unique years
- **Query Use:** Year-level filtering and grouping

### **quarterly_avg_price** (FLOAT64)
- **Type:** Continuous numeric (aggregated price)
- **Nulls:** 0%
- **Range:** 2.1029 to 561,958.33
- **Cardinality:** 1,001 unique values
- **Purpose:** Quarterly averaged price metric
- **Query Use:** Quarterly comparisons, smoothed trend analysis

### **pct_change_q1_forward** (FLOAT64)
- **Type:** Continuous numeric (percentage)
- **Nulls:** 0.74% (22 rows)
- **Range:** -98.22% to 5,154.46%
- **Purpose:** Price change 1 quarter forward from current period
- **Query Use:** Short-term trend analysis, forecasting validation

### **pct_change_q2_forward** (FLOAT64)
- **Type:** Continuous numeric (percentage)
- **Nulls:** 1.48% (44 rows)
- **Range:** -98.22% to 5,154.46%
- **Purpose:** Price change 2 quarters forward
- **Query Use:** Medium-term trend analysis

### **pct_change_q3_forward** (FLOAT64)
- **Type:** Continuous numeric (percentage)
- **Nulls:** 2.22% (66 rows)
- **Range:** -98.22% to 5,154.46%
- **Purpose:** Price change 3 quarters forward
- **Query Use:** Longer-term trend analysis

### **pct_change_q4_forward** (FLOAT64)
- **Type:** Continuous numeric (percentage)
- **Nulls:** 2.97% (88 rows)
- **Range:** -98.22% to 5,602.09%
- **Cardinality:** 1,564 unique values (most diverse)
- **Purpose:** Price change 4 quarters (1 year) forward
- **Query Use:** Annual trend analysis, year-over-year comparisons

## Potential Query Considerations

### **Good Filtering Columns:**
- `commodity_name` - Filter by specific commodities or groups
- `year_val` - Filter by specific years
- `year_quarter` - Filter by specific quarters
- `month_date` - Date range filtering for time series
- `quarter_num` - Seasonal pattern filtering

### **Good Grouping/Aggregation Columns:**
- `commodity_name` - Compare across commodities
- `year_val` - Annual trends
- `year_quarter` - Quarterly patterns
- `quarter_num` - Seasonal analysis
- `commodity_unit` - Group by currency/measurement type

### **Potential Join Keys:**
- `month_date` - Join to other time-series data
- `commodity_name` + `month_date` - Unique row identifier
- `year_quarter` - Join to quarterly economic indicators

### **Data Quality Considerations:**
1. **Unit Consistency:** Queries comparing prices must account for different units (USD vs CNY) and measurement scales (T, KG, Lbs, etc.)
2. **Null Handling:** Forward-looking percentage changes have increasing nulls toward recent periods (expected for forward-looking metrics)
3. **Price Range Variation:** Massive price range differences across commodities require careful statistical analysis
4. **Case Sensitivity:** Unit names have case variations (CNY/KG vs CNY/Kg)
5. **Temporal Gaps:** Verify continuous monthly data for specific commodities before time-series analysis
6. **Extreme Values:** Some percentage changes exceed 5,000%, indicating potential data quality issues or legitimate extreme volatility

### **Analytical Use Cases:**
- Time-series forecasting of commodity prices
- Commodity correlation analysis
- Seasonal pattern identification
- Price volatility assessment
- Forward-looking return predictions
- Currency comparison (USD vs CNY commodities)
- Quarterly vs monthly price dynamics

## Keywords

commodities, commodity prices, economic data, time series, forward returns, percentage change, metals pricing, quarterly analysis, monthly pricing, aluminum, copper, gold, silver, zinc, lead, lithium, titanium, gallium, germanium, iron ore, lumber, bitumen, polypropylene, price forecasting, price trends, quarterly returns, financial analysis, materials pricing, USD pricing, CNY pricing, commodity units, price volatility, forward-looking metrics, Q1 forward, Q2 forward, Q3 forward, Q4 forward, year-over-year, seasonal patterns, economic indicators

## Table and Column Documentation

**Table Comment:** Not provided

**Column Comments:** Not provided