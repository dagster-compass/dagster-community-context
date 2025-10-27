---
columns:
- company_id (STRING)
- employee_count (INT64)
- month_date (STRING)
- role (STRING)
schema_hash: daa30e882102489651ee9c4f9b7f58e49ff75a6d55d403eddea5c32d7c360bc4

---
# Table Analysis Summary: people_labs_data.companies_employee_timeseries_by_role

## Overall Dataset Characteristics

- **Total Rows**: 42,969,808,368 (approximately 43 billion rows)
- **Data Quality**: Excellent - 0% null values across all columns
- **Time Range**: Spans from 2010-01 to at least 2025-03 (188 unique months, ~15+ years)
- **Scale**: Massive enterprise-level dataset tracking employee counts by role across millions of companies
- **Structure**: Time series data with monthly granularity for company workforce composition

## Column Details

### company_id (STRING)
- **Type**: String identifier (likely UUID format)
- **Nulls**: 0.00%
- **Unique Values**: 16,020,211 companies
- **Format**: Alphanumeric identifiers (e.g., "bGfbFRHHOObpJQMuPSCM3wQHbWjb")
- **Usage**: Primary entity identifier for joining with company master data

### month_date (STRING) 
- **Type**: String in YYYY-MM format
- **Nulls**: 0.00%
- **Unique Values**: 188 months
- **Range**: 2010-01 through 2025-03 (includes future dates)
- **Pattern**: Consistent monthly time series data
- **Usage**: Time dimension for trend analysis and filtering

### role (STRING)
- **Type**: Categorical string
- **Nulls**: 0.00%
- **Unique Values**: 24 distinct roles
- **Categories**: advisory, analyst, creative, education, engineering, finance, fulfillment, health, hospitality, human_resources, legal, public_service, other_uncategorized, etc.
- **Usage**: Primary dimension for workforce composition analysis

### employee_count (INT64)
- **Type**: Integer
- **Nulls**: 0.00%
- **Range**: 0 to 304,921 employees
- **Unique Values**: 39,377 distinct counts
- **Distribution**: Heavy concentration at 0 (many company-role-month combinations have no employees)
- **Usage**: Primary metric for aggregations and analysis

## Potential Query Considerations

### Excellent for Filtering:
- **month_date**: Time-based filtering (quarters, years, date ranges)
- **role**: Specific job function analysis
- **company_id**: Company-specific workforce tracking
- **employee_count**: Size-based filtering (>0 for active roles, specific thresholds)

### Excellent for Grouping/Aggregation:
- **role**: Workforce composition analysis across industries
- **month_date**: Time series aggregations, trend analysis
- **company_id**: Company-level summaries
- Combined grouping for multi-dimensional analysis

### Join Considerations:
- **company_id**: Primary key for joining with company metadata (industry, location, size)
- May relate to other employee or company dimension tables

### Data Quality Considerations:
- **Zero Values**: Many records show 0 employees - these may represent:
  - Companies without that specific role
  - Seasonal variations
  - Data collection periods before/after company activity
- **Future Dates**: Data includes 2025 dates, suggesting projections or data pipeline testing
- **Scale**: Query performance considerations due to 43B+ row volume
- **Partitioning**: Likely partitioned by month_date for optimal query performance

## Keywords

time series, employee tracking, workforce analytics, company staffing, role-based employment, monthly data, people analytics, human resources data, company growth tracking, organizational structure, job functions, employment trends, workforce composition, staff count, headcount analysis

## Table and Column Documentation

No table comment or column comments were provided in the source data.