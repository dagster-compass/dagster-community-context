---
columns:
- company_id (STRING)
- employee_additions_count (INT64)
- employee_departures_count (INT64)
- month_date (STRING)
- total_employee_count (INT64)
schema_hash: 79523b2b19040120bf40e40186db1d6f50f4e640a6d1ba170a495487fadaaafb

---
# Comprehensive Data Summary: companies_employee_timeseries

## Overall Dataset Characteristics

### Dataset Scale and Scope
- **Total Rows**: 1,790,408,682 (approximately 1.79 billion records)
- **Data Type**: Time-series employee tracking data at company-month granularity
- **Temporal Coverage**: 188 unique months spanning from 2010-01 to at least 2024-10 (approximately 15 years)
- **Company Coverage**: 16,020,211 unique companies tracked

### General Data Quality Observations
- **Core Data Completeness**: Company ID, month_date, and total_employee_count are 100% populated
- **Partial Data Availability**: 
  - Employee additions data is missing for 17.46% of records
  - Employee departures data is missing for 41.61% of records (significantly higher missing rate)
- **Data Quality Pattern**: The higher null percentage in departures suggests this metric may be harder to track or is collected less consistently than additions
- **Time Series Integrity**: Monthly granularity is consistent with YYYY-MM format

### Notable Patterns and Distributions
- **Company Size Distribution**: Employee counts range from 0 (possibly inactive/pre-launch) to 542,509 (large enterprise), with heavy representation of small companies (0-9 employees are common values)
- **Employee Movement**: Additions range 0-30,333 and departures 0-16,422, suggesting some companies experience significant workforce changes
- **Sparse Data**: The massive number of companies (16M+) relative to total records suggests many companies have limited time-series history

## Column Details

### month_date (STRING)
- **Format**: YYYY-MM (e.g., "2024-07", "2021-01")
- **Completeness**: 100% populated (0.00% null)
- **Temporal Range**: 188 unique months from 2010-01 through at least 2024-10
- **Pattern**: Consistent monthly time-series format
- **Use Case**: Primary temporal dimension for time-series analysis
- **Note**: STRING type may require conversion for date operations

### total_employee_count (INT64)
- **Completeness**: 100% populated (0.00% null)
- **Range**: 0 to 542,509 employees
- **Distribution**: 57,786 unique values suggest wide variety of company sizes
- **Common Values**: 0, 1, 2, 3... indicating heavy representation of small companies and startups
- **Pattern**: Sample shows values like 0, 1, 9, 18, 56 - spanning micro to large companies
- **Use Case**: Primary metric for company size analysis and growth tracking

### employee_additions_count (INT64)
- **Completeness**: 82.54% populated (17.46% null)
- **Range**: 0 to 30,333 new employees
- **Distribution**: 4,376 unique values
- **Common Values**: 0 is highly prevalent in samples, suggesting many months with no hiring
- **Pattern**: Most companies show 0 additions in typical months; large values indicate aggressive growth periods
- **Data Quality**: Nulls likely represent periods where addition data wasn't tracked or available

### employee_departures_count (INT64)
- **Completeness**: 58.39% populated (41.61% null - highest null rate)
- **Range**: 0 to 16,422 departures
- **Distribution**: 3,540 unique values (fewer than additions)
- **Common Values**: 0 when populated; NULL very common in samples
- **Pattern**: Maximum departures (16,422) is about half of maximum additions (30,333)
- **Data Quality**: High null percentage suggests departure tracking is less consistent than hiring tracking

### company_id (STRING)
- **Completeness**: 100% populated (0.00% null)
- **Cardinality**: 16,020,211 unique companies
- **Format**: Alphanumeric hash-like identifiers (e.g., "kBFtBhB0bmiCmR1aPga9BgfDbDJp")
- **Length**: Appears to be fixed-length 32-character strings
- **Pattern**: Mix of uppercase, lowercase letters and numbers
- **Use Case**: Primary key for company identification; join key to other company dimension tables

## Potential Query Considerations

### Filtering Recommendations
- **Time-based filtering**: Use `month_date` with string comparison or PARSE_DATE function
  - Consider recent data (e.g., `month_date >= '2020-01'`) for better data completeness
  - Filter by date ranges for period-over-period analysis
- **Company size filtering**: Use `total_employee_count` to focus on specific company segments
  - Small: 1-50, Medium: 51-500, Large: 500+
- **Activity filtering**: Consider filtering WHERE `employee_additions_count` IS NOT NULL for hiring analysis
- **Data quality filtering**: Be explicit about NULL handling for additions/departures

### Grouping/Aggregation Opportunities
- **Temporal aggregations**: Group by `month_date` for trend analysis
  - Can extract year, quarter from month_date string
- **Company-level aggregations**: Group by `company_id` for company-specific metrics
  - Calculate growth rates, average tenure patterns
- **Cohort analysis**: Group companies by first appearance month
- **Size-based segmentation**: Bucket by `total_employee_count` ranges
- **Combined metrics**: Calculate net employee change (additions - departures) when both are available

### Join Keys and Relationships
- **Primary Key**: Composite key of (`company_id`, `month_date`)
- **Foreign Key**: `company_id` likely joins to:
  - Company master table with name, industry, location, founding date
  - Company metadata or profile tables
- **Relationship Pattern**: Many-to-one from timeseries to company dimension

### Data Quality Considerations for Queries

1. **NULL Handling Strategy**:
   - Always check if departures data is needed; if so, expect 42% data loss
   - Use COALESCE for additions (0 as default) with caution
   - Consider filtering to periods with complete data

2. **Time Series Gaps**:
   - Not all companies have continuous monthly records
   - Check for gaps when calculating month-over-month changes
   - Use LAG/LEAD functions carefully with PARTITION BY company_id

3. **Recent Data Bias**:
   - Later years (2020+) likely have better data completeness
   - Consider data vintage when comparing historical trends

4. **Scale Considerations**:
   - 1.79B rows require efficient filtering before aggregation
   - Always filter on indexed columns first (likely company_id and month_date)
   - Use partitioning by month_date if available

5. **Calculated Metrics**:
   - Net change = additions - departures (handle NULLs appropriately)
   - Growth rate = (current - previous) / previous (watch for division by zero)
   - Turnover rate requires handling both NULLs and zero employee counts

6. **Edge Cases**:
   - Companies with 0 employees (possibly pre-launch or defunct)
   - Large spikes in additions/departures may indicate M&A activity
   - Single-month records may be data quality issues vs. short-lived companies

## Keywords

time-series, employee data, workforce analytics, company growth, headcount tracking, hiring trends, employee turnover, attrition, monthly data, employment statistics, company size, talent analytics, workforce planning, HR analytics, personnel changes, organizational growth, staffing levels, employee movement, longitudinal data, panel data, company analytics, business intelligence, people analytics, workforce metrics, employment trends, company timeseries, monthly snapshots, employee counts, hiring patterns, departure tracking

## Table and Column Documentation

**Note**: No table comment or column comments were provided in the source data analysis report. The table appears to be named `people_labs_data.companies_employee_timeseries` which suggests it is part of a People Labs dataset focused on company employee time-series tracking.