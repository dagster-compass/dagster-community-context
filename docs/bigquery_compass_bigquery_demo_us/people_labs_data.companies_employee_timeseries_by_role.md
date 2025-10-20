---
columns:
- company_id (STRING)
- employee_count (INT64)
- month_date (STRING)
- role (STRING)
schema_hash: daa30e882102489651ee9c4f9b7f58e49ff75a6d55d403eddea5c32d7c360bc4

---
# Dataset Summary: people_labs_data.companies_employee_timeseries_by_role

## Overall Dataset Characteristics

- **Total Rows**: 42,969,808,368 (approximately 43 billion records)
- **Data Quality**: Excellent - 0% null values across all columns
- **Time Span**: Data spans from 2010-01 to 2024-05 (188 months, ~14.4 years)
- **Scale**: Massive timeseries dataset tracking employee counts by role across ~16 million companies
- **Notable Patterns**: 
  - Many records show 0 employee counts, suggesting comprehensive tracking even for roles not present at companies
  - Wide range of employee counts (0 to 304,921) indicating coverage from startups to large enterprises
  - Consistent monthly granularity for temporal analysis

## Column Details

### role (STRING)
- **Data Type**: Categorical string
- **Completeness**: 100% (no nulls)
- **Cardinality**: 24 distinct roles
- **Coverage**: Spans major business functions including engineering, sales, marketing, finance, HR, etc.
- **Sample Roles**: advisory, analyst, creative, education, engineering, finance, fulfillment, health, hospitality, human_resources, manufacturing, marketing, partnerships, sales_engineering, support
- **Query Considerations**: Excellent for grouping and filtering by business function

### month_date (STRING)
- **Data Type**: String in YYYY-MM format
- **Completeness**: 100% (no nulls)
- **Temporal Range**: 2010-01 to 2024-05 (188 unique months)
- **Format**: Consistent YYYY-MM pattern
- **Query Considerations**: 
  - Primary dimension for time-series analysis
  - Can be converted to DATE type for temporal operations
  - Suitable for trend analysis and time-based filtering

### employee_count (INT64)
- **Data Type**: Integer
- **Completeness**: 100% (no nulls)
- **Range**: 0 to 304,921 employees
- **Distribution**: 39,377 unique values, with many zero values indicating roles not present at companies
- **Query Considerations**: 
  - Primary metric for aggregation (SUM, AVG, MAX, MIN)
  - Zero values may need special handling depending on analysis needs
  - Wide range suggests need for appropriate aggregation strategies

### company_id (STRING)
- **Data Type**: Alphanumeric identifier string
- **Completeness**: 100% (no nulls)
- **Cardinality**: 16,020,211 unique companies
- **Format**: Consistent alphanumeric string format (~32 characters)
- **Query Considerations**: 
  - Primary key for company-level analysis
  - Essential for joins with other company datasets
  - High cardinality requires efficient indexing strategies

## Potential Query Considerations

### Filtering Columns
- **month_date**: Excellent for time-based filtering (e.g., recent years, specific quarters)
- **role**: Perfect for analyzing specific business functions
- **company_id**: For company-specific analysis
- **employee_count**: For filtering by company size thresholds

### Grouping/Aggregation Opportunities
- **Time-series analysis**: GROUP BY month_date for trend analysis
- **Role analysis**: GROUP BY role for workforce composition insights
- **Company segmentation**: Aggregate by company_id for company-level metrics
- **Combined dimensions**: Multi-dimensional analysis (role + time, company size categories)

### Potential Join Keys
- **company_id**: Primary key for joining with other company datasets (financials, industry, location, etc.)
- **month_date**: Can join with economic indicators, market data, or other time-series datasets

### Data Quality Considerations
- **Zero Values**: Many employee_count = 0 records may need filtering depending on analysis goals
- **Scale**: 43B+ rows require careful query optimization and potentially sampling for exploratory analysis
- **Time Consistency**: Monthly granularity is consistent, enabling reliable time-series analysis
- **Company Coverage**: Massive company coverage suggests comprehensive market representation

## Keywords
employee timeseries, workforce analytics, company staffing, role-based employment, monthly employee data, business function staffing, company growth tracking, headcount analysis, organizational structure, people analytics, employment trends, company size metrics, staff composition, workforce planning data

## Table and Column Documentation
*No table comment or column comments provided in the source data.*