---
columns:
- company_id (STRING)
- employee_count (INT64)
- month_date (STRING)
- role (STRING)
schema_hash: daa30e882102489651ee9c4f9b7f58e49ff75a6d55d403eddea5c32d7c360bc4

---
# Table Summary: people_labs_data.companies_employee_timeseries_by_role

## Overall Dataset Characteristics

- **Total Rows**: 42,969,808,368 (approximately 43 billion records)
- **Data Quality**: Excellent - 0% null values across all columns
- **Time Span**: Covers 188 months from 2010-01 onwards (approximately 15+ years of data)
- **Structure**: Time series data tracking employee counts by role across companies over time
- **Scale**: Massive dataset with over 16 million unique companies tracked

## Column Details

### month_date (STRING)
- **Data Type**: String in YYYY-MM format
- **Completeness**: 100% (no nulls)
- **Time Range**: 188 unique months starting from 2010-01
- **Pattern**: Consistent monthly snapshots over approximately 15+ years
- **Usage**: Primary time dimension for temporal analysis

### role (STRING)  
- **Data Type**: Categorical string
- **Completeness**: 100% (no nulls)
- **Categories**: 24 distinct job roles including:
  - Technical: engineering, analyst
  - Business: finance, marketing, legal
  - Operations: fulfillment, hospitality
  - Support: human_resources, education, health
  - Other: advisory, creative
- **Usage**: Primary grouping dimension for role-based analysis

### employee_count (INT64)
- **Data Type**: Integer
- **Completeness**: 100% (no nulls) 
- **Range**: 0 to 304,921 employees
- **Distribution**: Heavy concentration at 0 (many company-role-month combinations have no employees)
- **Precision**: Exact employee counts with high granularity (39,377 unique values)
- **Usage**: Primary metric for aggregation and analysis

### company_id (STRING)
- **Data Type**: String identifier (appears to be encoded/hashed)
- **Completeness**: 100% (no nulls)
- **Uniqueness**: 16,020,211 unique companies
- **Format**: Alphanumeric strings (likely anonymized identifiers)
- **Usage**: Primary entity identifier for company-level analysis

## Query Considerations

### Filtering Columns
- **month_date**: Excellent for time-based filtering (date ranges, specific months/years)
- **role**: Perfect for role-specific analysis (engineering teams, sales teams, etc.)
- **company_id**: Essential for single company deep dives
- **employee_count**: Useful for size-based filtering (startups vs enterprises)

### Grouping/Aggregation Opportunities
- **Temporal Analysis**: Group by month_date for time series trends
- **Role Analysis**: Group by role to compare department sizes across companies
- **Company Segmentation**: Group by employee_count ranges for size-based analysis
- **Multi-dimensional**: Combine role + month_date for role growth trends over time

### Potential Join Keys
- **company_id**: Primary key for joining with other company-related tables
- **month_date**: Can join with other time-series datasets on temporal dimension
- **role**: Could join with role/job function reference tables

### Data Quality Considerations
- **Zero Values**: Many employee_count = 0 records indicate companies may not have employees in every role every month
- **Scale**: Extremely large dataset requires careful query optimization and potentially sampling for exploratory analysis
- **Time Series Gaps**: May need to handle missing months for continuous time series analysis
- **Role Consistency**: Role names appear standardized but should verify completeness of role taxonomy

## Keywords
time series, employee tracking, workforce analytics, company sizing, organizational structure, job roles, monthly snapshots, people analytics, headcount data, employment trends, company growth, workforce planning, HR analytics, organizational charts, employee segmentation

## Table and Column Docs
No table comment or column comments were provided in the analysis report.