---
columns:
- company_id (STRING)
- employee_additions_count (INT64)
- employee_departures_count (INT64)
- month_date (STRING)
- total_employee_count (INT64)
schema_hash: 79523b2b19040120bf40e40186db1d6f50f4e640a6d1ba170a495487fadaaafb

---
# Table Summary: people_labs_data.companies_employee_timeseries

## Overall Dataset Characteristics

This is a **massive time-series dataset** tracking employee counts and movements across companies over time, containing **1.79 billion rows**. The data spans approximately **188 months** (roughly 15+ years from 2010 onwards based on sample values) and covers **16+ million unique companies**.

### Key Observations:
- **Time Period**: Data ranges from at least 2010-01 through 2021-08 (and likely beyond)
- **Scale**: Monthly snapshots of employee metrics for millions of companies
- **Data Quality**: Mixed quality with significant null values in movement metrics (additions: 17.46%, departures: 41.61%)
- **Granularity**: Monthly aggregations with company-level metrics

## Column Details

### month_date (STRING)
- **Format**: YYYY-MM date string
- **Coverage**: 188 unique months spanning ~15 years
- **Completeness**: 100% populated (no nulls)
- **Pattern**: Monthly time series data starting from 2010
- **Query Use**: Primary time dimension for filtering and grouping; temporal analysis

### total_employee_count (INT64)
- **Range**: 0 to 542,509 employees
- **Distribution**: 57,786 unique values; heavily skewed toward smaller companies
- **Completeness**: 100% populated
- **Characteristics**: 
  - Many companies with 0 employees (possibly defunct or pre-launch)
  - Maximum suggests very large enterprise companies included
  - Low single-digit values are common (startups/small businesses)
- **Query Use**: Primary metric for company size analysis, filtering, aggregation

### employee_additions_count (INT64)
- **Range**: 0 to 30,333 new hires per month
- **Null Rate**: 17.46% (significant missing data)
- **Distribution**: 4,376 unique values; most companies have low hiring rates
- **Characteristics**:
  - Represents monthly new hires/additions
  - Nulls likely indicate no data available vs. zero additions
  - Maximum of 30K suggests major hiring events or large companies
- **Query Use**: Growth analysis, hiring trend identification (handle nulls carefully)

### employee_departures_count (INT64)
- **Range**: 0 to 16,422 departures per month
- **Null Rate**: 41.61% (high missing data - worse than additions)
- **Distribution**: 3,540 unique values
- **Characteristics**:
  - Represents monthly attrition/departures
  - Higher null rate suggests departure data is harder to track
  - Maximum lower than additions (16K vs 30K)
- **Query Use**: Attrition analysis, turnover calculations (requires null handling)

### company_id (STRING)
- **Cardinality**: 16,020,211 unique companies
- **Format**: Alphanumeric hash strings (consistent length ~32 characters)
- **Completeness**: 100% populated
- **Pattern**: Appears to be a UUID or hash-based identifier
- **Query Use**: Primary key for company identification, join key for company dimension tables

## Potential Query Considerations

### Filtering Best Practices:
1. **Time-based filtering**: Use `month_date` for temporal queries
   - Consider date range filters (e.g., `month_date >= '2020-01'`)
   - Monthly aggregations are already built-in
   
2. **Company size filtering**: Use `total_employee_count` to segment by company size
   - Small: 1-50, Medium: 51-500, Large: 500+
   - Filter out zero-employee records if analyzing active companies

3. **Data quality filtering**: 
   - Consider `WHERE employee_additions_count IS NOT NULL` for hiring analysis
   - Be aware of 41.61% null rate in departures data

### Grouping/Aggregation Opportunities:
1. **Time-series analysis**: Group by `month_date` for trend analysis
2. **Company-level aggregations**: Group by `company_id` for company lifecycle analysis
3. **Cohort analysis**: Combine time and size dimensions
4. **Growth metrics**: Calculate net employee change (additions - departures)

### Join Considerations:
- **Primary join key**: `company_id` - likely joins to company dimension tables
- **Composite key**: (`company_id`, `month_date`) for precise point-in-time joins
- **Expected related tables**: Company profiles, industry classifications, geographic data

### Data Quality Considerations:
1. **Null handling**: Critical for movement metrics
   - Don't assume NULL = 0 for additions/departures
   - Consider separate analysis for records with complete vs. incomplete data
   
2. **Zero employee companies**: Decide whether to include/exclude based on analysis goal
   
3. **Outliers**: Very large employee counts or movements may need validation
   
4. **Time coverage**: Not all companies have data for all months (gaps expected)

5. **Calculation accuracy**: 
   - Net change: `total_employee_count` current month - previous month
   - May not always equal `additions - departures` due to data collection methods

## Keywords

time-series, employee-count, workforce-analytics, headcount-tracking, hiring-trends, attrition-analysis, company-growth, monthly-snapshots, workforce-movement, employee-additions, employee-departures, company-timeseries, headcount-history, employment-data, organizational-growth, turnover-metrics, people-analytics, staffing-trends, workforce-changes, company-metrics

## Table and Column Documentation

**Table Comment**: Not provided

**Column Comments**: Not provided