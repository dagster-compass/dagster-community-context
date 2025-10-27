---
columns:
- company_id (STRING)
- employee_count (INT64)
- level (STRING)
- month_date (STRING)
schema_hash: a4a68bd81a642b890c2263843fc594c3f207689ec7e49ebbdc4834e6f89e20d9

---
# Table Analysis Summary: people_labs_data.companies_employee_timeseries_by_level

## Overall Dataset Characteristics

- **Total Rows**: 10,466,558,360 (over 10 billion records)
- **Data Quality**: Excellent - no null values across all columns
- **Time Range**: Monthly data spanning from 2010-01 to approximately 2025+ (188 unique months, ~15+ years)
- **Structure**: Time series data tracking employee counts by organizational level for companies
- **Scale**: Massive dataset covering over 16 million unique companies

## Column Details

### month_date (STRING)
- **Type**: String in YYYY-MM format
- **Null Values**: 0% (perfect data quality)
- **Temporal Coverage**: 188 unique months spanning 2010-2025+
- **Format**: Consistent YYYY-MM date format
- **Usage**: Primary time dimension for time series analysis

### employee_count (INT64)
- **Type**: Integer
- **Null Values**: 0% (perfect data quality)
- **Range**: 0 to 120,165 employees
- **Distribution**: Heavy concentration at lower values (many 0s), with maximum suggesting large enterprise companies
- **Usage**: Primary metric for workforce analysis and trends

### level (STRING)
- **Type**: Categorical string
- **Null Values**: 0% (perfect data quality)
- **Categories**: 10 distinct organizational levels:
  - `cxo` (C-suite executives)
  - `director`
  - `entry` (entry-level)
  - `manager`
  - `owner`
  - `partner`
  - `senior`
  - `training`
  - `unpaid`
  - `vp` (vice president)
- **Usage**: Key dimension for organizational structure analysis

### company_id (STRING)
- **Type**: Unique string identifier
- **Null Values**: 0% (perfect data quality)
- **Uniqueness**: 16,020,211 unique companies
- **Format**: Alphanumeric hash-like identifiers (consistent length)
- **Usage**: Primary key for company identification and joins

## Potential Query Considerations

### Excellent for Filtering:
- **month_date**: Time-based filtering (date ranges, specific months/years)
- **level**: Organizational level analysis (executives vs. employees)
- **company_id**: Company-specific analysis
- **employee_count**: Size-based filtering (small vs. large companies)

### Excellent for Grouping/Aggregation:
- **month_date**: Time series aggregations, trend analysis
- **level**: Organizational structure analysis, workforce composition
- **company_id**: Company-level summaries
- **employee_count**: Size-based segmentation and statistics

### Join Considerations:
- **company_id**: Primary join key for company master data, industry classifications, geographic data
- **Time series nature**: Suitable for window functions and temporal joins

### Data Quality Considerations:
- **Exceptional data quality**: No null values across 10+ billion records
- **Time series completeness**: Consider gaps in company reporting across months
- **Zero employee counts**: Many records show 0 employees, which may indicate:
  - Company dormancy periods
  - Data collection gaps
  - Companies with no employees at specific levels
- **Scale considerations**: Queries should use appropriate partitioning and filtering due to massive size

## Keywords

time series, employee data, organizational levels, workforce analytics, company data, headcount tracking, C-suite, management levels, employment trends, corporate structure, people analytics, human resources data, organizational hierarchy, employee count, monthly data, company timeseries

## Table and Column Documentation

No table comment or column comments were provided in the analysis.