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

- **Total Rows**: 42,969,808,368 (~43 billion records)
- **Dataset Type**: Large-scale time-series data tracking employee counts by role across companies
- **Time Range**: January 2010 to November 2024 (188 months/~15.7 years)
- **Granularity**: Monthly snapshots of employee counts per company per role
- **Data Quality**: Excellent - all columns show 0.00% null values
- **Scale**: Covers 16+ million unique companies across 24 different role categories

### Notable Patterns
- High prevalence of zero employee counts in samples, suggesting sparse data (companies may not have employees in all roles for all months)
- Extensive historical tracking enabling longitudinal workforce analysis
- Fine-grained role segmentation providing detailed workforce composition insights

## Column Details

### 1. **company_id** (STRING)
- **Purpose**: Primary entity identifier for companies
- **Cardinality**: 16,020,211 unique companies
- **Format**: 32-character alphanumeric hash (e.g., "r2SlCB6fqCDO441WAJENHgsZQrld")
- **Null Pattern**: No nulls (0.00%)
- **Data Quality**: Consistent format, appears to be a proprietary ID system
- **Use Case**: Essential for filtering by company, joining with other company tables

### 2. **month_date** (STRING)
- **Purpose**: Temporal dimension for time-series analysis
- **Cardinality**: 188 unique months
- **Format**: YYYY-MM (e.g., "2016-03", "2020-05", "2024-11")
- **Range**: 2010-01 through 2024-11
- **Null Pattern**: No nulls (0.00%)
- **Data Quality**: Standardized format, consistent monthly intervals
- **Use Case**: Time-series filtering, trend analysis, period-over-period comparisons
- **Note**: Stored as STRING rather than DATE/TIMESTAMP - may need casting for date operations

### 3. **role** (STRING)
- **Purpose**: Categorical dimension for employee functional roles
- **Cardinality**: 24 unique role types
- **Categories Include**:
  - Technical: engineering, research
  - Business: sales_engineering, partnerships, finance
  - Operations: operations, fulfillment, hospitality
  - Support: human_resources, education, creative
  - Analytics: analyst
  - Other: advisory, health, other_uncategorized
- **Null Pattern**: No nulls (0.00%)
- **Data Quality**: Well-structured categorical data
- **Use Case**: Role-based filtering, workforce composition analysis, role trend tracking

### 4. **employee_count** (INT64)
- **Purpose**: Measure of employee headcount
- **Cardinality**: 39,377 unique values
- **Range**: 0 to 304,921 employees
- **Distribution**: Heavy concentration at lower values (many 0s in samples)
- **Null Pattern**: No nulls (0.00%)
- **Data Quality**: Clean integer values, logical range
- **Use Case**: Aggregations (SUM, AVG), growth calculations, size segmentation
- **Note**: Zero values are legitimate (company has no employees in that role that month)

## Query Considerations

### Recommended Filtering Columns
1. **company_id**: For company-specific analysis or joining with other tables
2. **month_date**: For time-range filtering (requires string comparison or PARSE_DATE)
3. **role**: For role-specific workforce analysis
4. **employee_count**: For size-based filtering (e.g., WHERE employee_count > 0)

### Recommended Grouping/Aggregation Patterns
1. **Time-series aggregations**: GROUP BY month_date for trends
2. **Role analysis**: GROUP BY role for workforce composition
3. **Company-level summaries**: GROUP BY company_id for total headcount
4. **Multi-dimensional**: GROUP BY month_date, role for detailed trends
5. **Aggregation functions**: SUM(employee_count), AVG(employee_count), MAX(employee_count)

### Potential Join Keys
- **company_id**: Primary key for joining with company profile/metadata tables
- **Composite key**: (company_id, month_date, role) forms unique identifier for each record

### Data Quality Considerations

1. **Sparse Data**: Many zero values suggest not all companies have all roles filled; consider filtering WHERE employee_count > 0 for active role analysis
2. **Date Format**: month_date is STRING - use PARSE_DATE(month_date, '%Y-%m') or string comparisons
3. **Scale**: 43B rows requires careful query optimization:
   - Always filter by company_id or date ranges when possible
   - Use LIMIT for exploratory queries
   - Consider partitioning strategies if available
4. **Latest Data**: Most recent month is 2024-11; data appears current
5. **Historical Completeness**: 188 consecutive months suggests comprehensive historical tracking

### Performance Optimization Tips
- Pre-filter by date ranges to reduce scan size
- Use company_id IN (...) for multi-company analysis
- Consider role IN (...) for focused role analysis
- Aggregate before joining when possible
- Use approximate aggregation functions (e.g., APPROX_COUNT_DISTINCT) for very large queries

## Keywords

time-series, employee headcount, workforce analytics, company growth, organizational structure, role distribution, employment trends, longitudinal data, people analytics, HR metrics, staffing levels, headcount tracking, monthly snapshots, role categories, company size, employee segmentation, workforce composition, talent analytics, organizational growth, employment history, functional roles, departmental headcount, company workforce, employee timeseries

## Table and Column Documentation

**Table Comment**: Not provided

**Column Comments**: 
- company_id: Not provided
- month_date: Not provided  
- role: Not provided
- employee_count: Not provided