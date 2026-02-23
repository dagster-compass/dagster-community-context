---
columns:
- _10yr (FLOAT64)
- _10yr_score (FLOAT64)
- created_at (TIMESTAMP)
- date (DATE)
- equity (FLOAT64)
- equity_score (FLOAT64)
- fci (FLOAT64)
- ffr (FLOAT64)
- ffr_score (FLOAT64)
- housing (FLOAT64)
- housing_score (FLOAT64)
- index_name (STRING)
schema_hash: 7ce6771a8189046e3ab12b9d6df2bb072c7cc17522c5955fddfad895d2cb3943

---
# Financial Conditions Index Dataset Summary

## Overall Dataset Characteristics

**Total Rows:** 87

**General Description:** This dataset contains time-series data tracking financial market conditions through various economic indicators. The data spans from 2016 to 2025, with monthly observations. All records were created on the same timestamp (2025-11-24), suggesting a batch import or historical data compilation.

**Data Quality Observations:**
- Generally high quality with minimal nulls in most columns
- Notable exception: `equity` column has 13.79% null values, and all score columns have 12.64% null values
- Consistent temporal coverage with one record per month
- All records share the same `index_name` value, indicating this is a single index dataset

**Notable Patterns:**
- The Financial Conditions Index (FCI) ranges from -0.55 to 0.19, suggesting standardized/normalized values
- All component metrics (ffr, equity, housing, _10yr) appear to be normalized or percentage-based
- Score columns appear to be weighted or adjusted versions of their base metrics

## Column Details

### Temporal Column

**`date` (DATE)**
- **Format:** Monthly frequency (first day of each month)
- **Nulls:** None (0.00%)
- **Coverage:** 87 unique months from 2016 to 2025
- **Usage:** Primary time dimension for temporal analysis and trending

### Raw Financial Metrics

**`ffr` (FLOAT64) - Federal Funds Rate**
- **Range:** -0.052 to 0.066
- **Nulls:** None (0.00%)
- **Distribution:** 65 unique values across 87 records
- **Interpretation:** Likely represents month-over-month changes or normalized FFR values
- **Pattern:** Includes negative values, suggesting rate decreases or normalized deviations

**`equity` (FLOAT64) - Equity Market Indicator**
- **Range:** -4.37 to 3.77
- **Nulls:** 13.79% (12 missing values)
- **Distribution:** 75 unique values
- **Pattern:** Widest range among metrics, indicating higher volatility
- **Data Quality Note:** Missing values may impact certain time periods

**`housing` (FLOAT64) - Housing Market Indicator**
- **Range:** -1.01 to 5.48
- **Nulls:** None (0.00%)
- **Distribution:** All 87 values are unique
- **Pattern:** Positive skew with maximum at 5.48, suggesting strong housing market periods

**`_10yr` (FLOAT64) - 10-Year Treasury Indicator**
- **Range:** -0.038 to 0.038
- **Nulls:** None (0.00%)
- **Distribution:** 86 unique values (nearly all unique)
- **Pattern:** Symmetric distribution around zero, likely yield changes

### Weighted Score Columns

**`equity_score` (FLOAT64)**
- **Range:** -0.157 to 0.092
- **Nulls:** 12.64% (11 missing values)
- **Distribution:** 76 unique values
- **Purpose:** Weighted contribution of equity to FCI

**`housing_score` (FLOAT64)**
- **Range:** -0.516 to 0.230
- **Nulls:** 12.64%
- **Distribution:** 76 unique values
- **Pattern:** Largest range among score columns, suggesting housing has highest weight in FCI

**`_10yr_score` (FLOAT64)**
- **Range:** -0.0044 to 0.0044
- **Nulls:** 12.64%
- **Distribution:** 76 unique values
- **Pattern:** Smallest magnitude, suggesting lower weight in FCI calculation

**`ffr_score` (FLOAT64)**
- **Range:** -0.0085 to 0.0093
- **Nulls:** 12.64%
- **Distribution:** 76 unique values
- **Pattern:** Small magnitude similar to _10yr_score

### Composite Index

**`fci` (FLOAT64) - Financial Conditions Index**
- **Range:** -0.546 to 0.188
- **Nulls:** None (0.00%)
- **Distribution:** 77 unique values
- **Interpretation:** Aggregate measure of financial conditions; negative = tighter, positive = looser conditions
- **Usage:** Primary output metric for analysis

### Metadata Columns

**`created_at` (TIMESTAMP)**
- **Value:** Single timestamp: 2025-11-24 18:50:32.747108+00:00
- **Nulls:** None
- **Usage:** Data provenance tracking

**`index_name` (STRING)**
- **Value:** Single value: "Financial Conditions Index"
- **Nulls:** None
- **Usage:** Dataset identifier (constant across all rows)

## Query Considerations

### Filtering Recommendations
- **Primary filter:** `date` column for time-based queries
- **Value filters:** `fci` for identifying tight/loose financial conditions
- **Null handling:** Always account for nulls in `equity` and score columns

### Grouping/Aggregation Opportunities
- **Temporal aggregations:** By year, quarter, or custom date ranges
- **Threshold-based grouping:** Categorize periods by FCI levels (e.g., tight/neutral/loose)
- **Metric correlations:** Compare raw metrics vs. their scores

### Join Considerations
- **Primary key:** `date` column (unique per row)
- **Potential joins:** Other economic time-series data on date
- **Index name:** Could join to metadata tables describing index methodology

### Data Quality Considerations
1. **Missing equity data:** 12 records (13.79%) lack equity values; queries using equity should handle nulls
2. **Missing scores:** 11 records (12.64%) missing all score columns; likely corresponds to early/late periods
3. **Score calculation:** FCI appears to be sum of score columns; verify this relationship in queries
4. **Temporal completeness:** Check for any missing months if doing sequential analysis
5. **Static metadata:** `created_at` and `index_name` are constant; don't use for filtering

### Analytical Use Cases
- **Trend analysis:** Track FCI evolution over time
- **Component contribution:** Analyze which metrics drive FCI changes
- **Threshold analysis:** Identify periods of extreme financial conditions
- **Leading indicators:** Compare raw metrics to scores to understand weighting
- **Volatility analysis:** Equity shows highest variance; housing most complete

## Keywords

Financial conditions, economic indicators, federal funds rate, FFR, equity markets, housing market, treasury yields, 10-year treasury, interest rates, monetary policy, financial markets, time series, economic data, market conditions, financial stress, credit conditions, liquidity, economic index, normalized indicators, weighted scores, financial stability, macroeconomic data, monthly data, economic indicators aggregation

## Table and Column Documentation

**Table Comment:** Not provided in the analysis report

**Column Comments:** No column-level comments were provided in the analysis report. The column names and data patterns suggest:
- Raw metrics (ffr, equity, housing, _10yr) represent underlying financial indicators
- Score columns appear to be weighted/normalized versions contributing to the composite FCI
- The FCI is the primary output representing overall financial conditions