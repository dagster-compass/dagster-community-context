---
columns:
- company_id (STRING)
- employee_additions_count (INT64)
- employee_departures_count (INT64)
- month_date (STRING)
- total_employee_count (INT64)
schema_hash: 79523b2b19040120bf40e40186db1d6f50f4e640a6d1ba170a495487fadaaafb

---
# People Labs Companies Employee Timeseries Dataset Summary

## Overall Dataset Characteristics

- **Total Rows**: 1,790,408,682 (nearly 1.8 billion records)
- **Time Range**: 188 months spanning from 2010-01 to approximately 2024-06 (approximately 14.5 years)
- **Companies Tracked**: Over 16 million unique companies (16,020,211)
- **Data Quality**: Mixed quality with significant null values in movement columns but complete data for core metrics
- **Scale**: This is a massive enterprise-scale dataset tracking employee counts and movements across millions of companies over time

## Column Details

### month_date (STRING)
- **Data Type**: String in YYYY-MM format
- **Completeness**: 100% complete (no nulls)
- **Time Range**: 188 unique months from 2010-01 to 2024-06
- **Format**: Consistent YYYY-MM date format
- **Usage**: Primary time dimension for temporal analysis

### company_id (STRING)
- **Data Type**: String identifier (appears to be base64-encoded)
- **Completeness**: 100% complete (no nulls)
- **Uniqueness**: 16,020,211 unique companies
- **Format**: Alphanumeric strings (e.g., "C0Yli4Nb9klCZgiy2CB7oQ04ZHQN")
- **Usage**: Primary company identifier for joins and grouping

### total_employee_count (INT64)
- **Data Type**: Integer
- **Completeness**: 100% complete (no nulls)
- **Range**: 0 to 542,509 employees
- **Distribution**: 57,786 unique values, heavily skewed toward smaller companies
- **Common Values**: Many companies with 0-10 employees
- **Usage**: Primary metric for company size analysis

### employee_additions_count (INT64)
- **Data Type**: Integer
- **Completeness**: 82.54% complete (17.46% null)
- **Range**: 0 to 30,333 additions per month
- **Distribution**: 4,376 unique values, most companies have 0-8 additions
- **Null Pattern**: Significant null percentage suggests data availability issues
- **Usage**: Metric for hiring activity analysis

### employee_departures_count (INT64)
- **Data Type**: Integer
- **Completeness**: 58.39% complete (41.61% null)
- **Range**: 0 to 16,422 departures per month
- **Distribution**: 3,540 unique values, most companies have 0-8 departures
- **Null Pattern**: High null percentage (41.61%) indicates limited departure tracking
- **Usage**: Metric for attrition analysis

## Potential Query Considerations

### Excellent for Filtering
- **month_date**: Perfect for time-based filtering and trend analysis
- **company_id**: Essential for company-specific analysis
- **total_employee_count**: Good for company size segmentation (small, medium, large companies)

### Good for Grouping/Aggregation
- **month_date**: Time-series aggregations, trend analysis, seasonal patterns
- **company_id**: Company-level summaries and comparisons
- **total_employee_count ranges**: Company size cohort analysis

### Join Considerations
- **company_id**: Primary key for joining with other company tables
- **month_date + company_id**: Composite key for time-series company data

### Data Quality Considerations
- **Null Handling**: Queries involving employee_additions_count and employee_departures_count must handle significant null percentages
- **Zero Values**: Many companies show 0 employees, which may indicate inactive/closed companies
- **Time Gaps**: Not all companies have data for all months
- **Performance**: With 1.8B rows, queries should use appropriate filtering and indexing strategies
- **Movement Data Reliability**: High null percentages in movement columns suggest incomplete tracking

### Recommended Query Patterns
- Always filter by time ranges to improve performance
- Consider excluding companies with 0 employees for active company analysis
- Use COALESCE or IS NOT NULL filters for movement columns
- Implement company size buckets for meaningful aggregations
- Use window functions for growth rate calculations

## Keywords
employee timeseries, company workforce, hiring trends, employee count, workforce analytics, company growth, employee additions, employee departures, monthly data, company size, headcount tracking, HR analytics, workforce intelligence, people data, employment trends

## Table and Column Documentation
*No table comment or column comments were provided in the source data.*