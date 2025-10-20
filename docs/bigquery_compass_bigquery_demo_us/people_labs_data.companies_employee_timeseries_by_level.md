---
columns:
- company_id (STRING)
- employee_count (INT64)
- level (STRING)
- month_date (STRING)
schema_hash: a4a68bd81a642b890c2263843fc594c3f207689ec7e49ebbdc4834e6f89e20d9

---
# Table Analysis Summary: companies_employee_timeseries_by_level

## Overall Dataset Characteristics

- **Total Rows**: 10,466,558,360 (over 10 billion records)
- **Data Quality**: Excellent - 0% null values across all columns
- **Time Range**: Monthly data from 2010-01 to approximately 2021+ (188 unique months, ~15.7 years)
- **Data Pattern**: Time series data tracking employee counts by organizational level for companies
- **Scale**: Massive dataset covering over 16 million unique companies with hierarchical employee tracking

## Column Details

### company_id (STRING)
- **Data Type**: String identifier
- **Completeness**: 100% (no nulls)
- **Cardinality**: 16,020,211 unique companies
- **Format**: Alphanumeric hash-like identifiers (32 characters)
- **Pattern**: Appears to be encoded/hashed company identifiers
- **Usage**: Primary entity identifier for companies

### month_date (STRING)
- **Data Type**: String in YYYY-MM format
- **Completeness**: 100% (no nulls)
- **Cardinality**: 188 unique months
- **Range**: 2010-01 through 2021+ (spans ~15.7 years)
- **Format**: Consistent YYYY-MM date format
- **Usage**: Temporal dimension for time series analysis

### level (STRING)
- **Data Type**: Categorical string
- **Completeness**: 100% (no nulls)
- **Cardinality**: 10 distinct organizational levels
- **Values**: 
  - `cxo` (C-level executives)
  - `director` (Director level)
  - `entry` (Entry level)
  - `manager` (Manager level)
  - `owner` (Business owners)
  - `partner` (Partners)
  - `senior` (Senior level)
  - `training` (Trainees/interns)
  - `unpaid` (Unpaid positions)
  - `vp` (Vice Presidents)
- **Usage**: Organizational hierarchy dimension

### employee_count (INT64)
- **Data Type**: Integer
- **Completeness**: 100% (no nulls)
- **Range**: 0 to 120,165 employees
- **Cardinality**: 26,016 unique values
- **Distribution**: Heavy concentration at lower values (many 0s), indicating sparse data
- **Usage**: Measure/metric for analysis

## Potential Query Considerations

### Filtering Columns
- **month_date**: Excellent for time-based filtering (quarters, years, date ranges)
- **level**: Perfect for organizational hierarchy analysis
- **company_id**: For company-specific analysis
- **employee_count**: For size-based filtering (>0 for active positions, ranges for company sizes)

### Grouping/Aggregation Opportunities
- **Time-based aggregation**: By year, quarter, or month using `month_date`
- **Hierarchical analysis**: Grouping by `level` for organizational structure insights
- **Company segmentation**: Grouping by `company_id` for company-level metrics
- **Combined dimensions**: Multi-dimensional analysis (company + time + level)

### Potential Join Keys
- **company_id**: Primary key for joining with other company-related tables
- **month_date**: Can join with other time series data
- **level**: Could join with organizational hierarchy reference tables

### Data Quality Considerations
- **Zero values**: High frequency of 0 employee_counts suggests sparse data structure
- **Scale**: Extremely large dataset requires careful query optimization
- **Time series completeness**: Consider gaps in time series for specific companies/levels
- **Partitioning**: Likely partitioned by month_date for query performance

### Query Performance Tips
- Use date range filters early in WHERE clauses
- Consider aggregating before detailed analysis due to data volume
- Partition-aware queries using month_date will be most efficient
- Index on company_id likely exists for fast company lookups

## Keywords
time series, employee data, organizational hierarchy, company analytics, workforce tracking, C-level executives, management levels, employment trends, corporate structure, people analytics, headcount data, organizational analysis, business intelligence, HR metrics

## Table and Column Documentation
*No table comment or column comments were provided in the analysis report.*