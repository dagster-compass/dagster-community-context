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
# Table Summary: Financial Conditions Index

## Overall Dataset Characteristics

**Total Rows:** 87

**General Description:** This table contains monthly financial conditions index (FCI) data spanning from 2016 to 2024. The FCI is a composite metric derived from multiple economic indicators including the Federal Funds Rate (FFR), equity markets, housing markets, and 10-year Treasury yields. The data represents a time series analysis of financial conditions with normalized scores for each component.

**Data Quality Observations:**
- The dataset has consistent nulls (~12.64%) in all score columns (ffr_score, equity_score, housing_score, _10yr_score) for the same records
- These nulls likely represent an initial baseline period or records where scores couldn't be calculated
- All other fields have complete data except equity (13.79% nulls)
- The `created_at` and `index_name` fields are constant across all records, suggesting batch processing

**Notable Patterns:**
- Monthly time series data with 87 unique dates
- The FCI ranges from -0.55 to 0.19, indicating both contractionary and expansionary financial conditions
- All component scores are normalized around zero, suggesting standardization was applied
- The housing component shows the widest range (5.48 units)

## Column Details

### date (DATE)
- **Type:** Date field, monthly granularity
- **Completeness:** 100% (0% nulls)
- **Uniqueness:** All 87 values are unique (one record per month)
- **Pattern:** Monthly economic data points from 2016-03 to 2024-04
- **Query Use:** Primary time dimension for filtering and ordering

### ffr (FLOAT64)
- **Description:** Federal Funds Rate (monthly average or change)
- **Completeness:** 100% (0% nulls)
- **Range:** -0.052 to 0.066
- **Distribution:** 65 unique values, suggesting rate changes and periods of stability
- **Pattern:** Values cluster around zero with both positive and negative values
- **Query Use:** Economic indicator for monetary policy analysis

### equity (FLOAT64)
- **Description:** Equity market indicator/index
- **Completeness:** 86.21% (13.79% nulls)
- **Range:** -4.37 to 3.77
- **Distribution:** 75 unique values with wide dispersion
- **Pattern:** Large range suggests significant market volatility captured
- **Note:** Higher null percentage than other components
- **Query Use:** Stock market conditions filter

### housing (FLOAT64)
- **Description:** Housing market indicator
- **Completeness:** 100% (0% nulls)
- **Range:** -1.01 to 5.48
- **Distribution:** 87 unique values (all unique), highest range among components
- **Pattern:** Predominantly positive values, showing housing market strength
- **Query Use:** Real estate market conditions analysis

### _10yr (FLOAT64)
- **Description:** 10-year Treasury yield metric (likely change or spread)
- **Completeness:** 100% (0% nulls)
- **Range:** -0.038 to 0.038
- **Distribution:** 86 unique values, tightly bounded around zero
- **Pattern:** Small magnitude changes indicating yield movements
- **Query Use:** Fixed income/interest rate analysis

### housing_score (FLOAT64)
- **Description:** Normalized/weighted score for housing component
- **Completeness:** 87.36% (12.64% nulls)
- **Range:** -0.516 to 0.230
- **Distribution:** 76 unique values
- **Pattern:** Standardized contribution to final FCI
- **Query Use:** Component contribution analysis

### _10yr_score (FLOAT64)
- **Description:** Normalized/weighted score for 10-year Treasury component
- **Completeness:** 87.36% (12.64% nulls)
- **Range:** -0.0044 to 0.0044
- **Distribution:** 76 unique values, smallest magnitude scores
- **Pattern:** Minimal contribution to overall FCI
- **Query Use:** Interest rate impact analysis

### equity_score (FLOAT64)
- **Description:** Normalized/weighted score for equity component
- **Completeness:** 87.36% (12.64% nulls)
- **Range:** -0.157 to 0.092
- **Distribution:** 76 unique values
- **Pattern:** Asymmetric range (more negative potential)
- **Query Use:** Equity market contribution analysis

### ffr_score (FLOAT64)
- **Description:** Normalized/weighted score for Federal Funds Rate
- **Completeness:** 87.36% (12.64% nulls)
- **Range:** -0.0085 to 0.0093
- **Distribution:** 76 unique values
- **Pattern:** Small contribution magnitudes
- **Query Use:** Monetary policy impact analysis

### fci (FLOAT64)
- **Description:** **Financial Conditions Index** - composite metric combining all components
- **Completeness:** 100% (0% nulls)
- **Range:** -0.546 to 0.188
- **Distribution:** 77 unique values
- **Pattern:** Negative values = tight conditions, positive = loose conditions
- **Key Metric:** This is the primary output/target variable
- **Query Use:** Primary metric for filtering and trending financial conditions

### index_name (STRING)
- **Description:** Constant identifier for the index type
- **Completeness:** 100% (0% nulls)
- **Unique Value:** "Financial Conditions Index" (all records)
- **Query Use:** Metadata field, likely for multi-index tables

### created_at (TIMESTAMP)
- **Description:** Data load/creation timestamp
- **Completeness:** 100% (0% nulls)
- **Unique Value:** 2025-11-24 18:50:32.747108+00:00 (all records)
- **Pattern:** Batch processing timestamp
- **Query Use:** Data lineage tracking

## Potential Query Considerations

### Good Columns for Filtering:
- **date**: Primary time-based filtering (WHERE date >= '2020-01-01')
- **fci**: Threshold filtering for tight/loose conditions (WHERE fci < 0)
- **equity, housing, ffr, _10yr**: Component-specific analysis

### Good Columns for Grouping/Aggregation:
- **date**: Time series aggregations (monthly, quarterly, yearly)
- Extract components: EXTRACT(YEAR FROM date), EXTRACT(MONTH FROM date)
- **index_name**: If combined with other index tables

### Potential Join Keys:
- **date**: Can join to other economic time series on month/date
- Could join to company financial data, market indices, or other economic indicators by date

### Data Quality Considerations:

1. **Null Handling:**
   - 11 records (~12.64%) have null score values but non-null raw values
   - These appear to be earlier records (e.g., 2016-03-01 sample)
   - Queries should use COALESCE or WHERE score IS NOT NULL when analyzing scores
   - The fci value is 0.0 for these records, suggesting a baseline period

2. **Time Series Gaps:**
   - Verify monthly continuity with date-based queries
   - 87 rows suggests ~7 years of monthly data

3. **Score Calculations:**
   - Score columns appear to be standardized components that sum to FCI
   - Null scores align across all four score columns
   - When querying scores, filter out nulls or treat separately

4. **Outlier Awareness:**
   - Housing component has extreme values (5.48 max)
   - Equity component has wide range (-4.37 to 3.77)
   - May need outlier handling for statistical analysis

### Recommended Query Patterns:

```sql
-- Time series analysis
WHERE date BETWEEN '2020-01-01' AND '2023-12-31'

-- Complete records only
WHERE housing_score IS NOT NULL

-- Financial conditions classification
WHERE fci > 0  -- Loose conditions
WHERE fci < -0.2  -- Tight conditions

-- Component contribution analysis
WHERE ABS(equity_score) > 0.1  -- Significant equity impact
```

## Keywords

Financial Conditions Index, FCI, Federal Funds Rate, FFR, equity markets, housing market, 10-year Treasury, interest rates, monetary policy, economic indicators, financial markets, time series, monthly data, market conditions, Treasury yields, composite index, economic analysis, financial stability, market sentiment, macroeconomic data

## Table and Column Docs

**Table Comment:** Not provided

**Column Comments:** Not provided