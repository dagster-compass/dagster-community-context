---
columns:
- company_id (STRING)
- employee_additions_count (INT64)
- employee_departures_count (INT64)
- month_date (STRING)
- total_employee_count (INT64)
schema_hash: 79523b2b19040120bf40e40186db1d6f50f4e640a6d1ba170a495487fadaaafb

---
# Company Employee Timeseries Dataset Summary

## Overall Dataset Characteristics

This is a massive employee tracking dataset with **1,790,408,682 rows** containing monthly timeseries data for company employee counts. The dataset spans from 2010 to 2023 (188 unique months) across over 16 million unique companies, making it a comprehensive workforce analytics resource.

**Data Quality Observations:**
- High data completeness for core fields (company_id, month_date, total_employee_count)
- Significant missing data for employee movement metrics (17.46% for additions, 41.61% for departures)
- The dataset appears to prioritize headcount tracking over detailed hiring/departure analytics

**Notable Patterns:**
- Company sizes range from 0 to 542,509 employees, indicating coverage of everything from startups to large enterprises
- Missing departure data is more common than missing addition data, suggesting challenges in tracking employee exits
- The timespan covers both pre-recession, recession, recovery, and pandemic periods (2010-2023)

## Column Details

### month_date (STRING)
- **Format:** YYYY-MM (e.g., "2020-09", "2018-09", "2023-01")
- **Coverage:** 188 months from 2010-01 to 2023 (approximately 15+ years)
- **Completeness:** 100% - no null values
- **Usage:** Primary time dimension for temporal analysis

### company_id (STRING)
- **Format:** Alphanumeric hash identifiers (32 characters)
- **Uniqueness:** 16,020,211 unique companies
- **Completeness:** 100% - no null values  
- **Usage:** Primary company identifier for grouping and filtering

### total_employee_count (INT64)
- **Range:** 0 to 542,509 employees
- **Distribution:** 57,786 unique values, heavily skewed toward smaller companies
- **Completeness:** 100% - no null values
- **Usage:** Core metric for company size analysis and growth tracking

### employee_additions_count (INT64)
- **Range:** 0 to 30,333 new hires per month
- **Missing Data:** 17.46% null values
- **Distribution:** 4,376 unique values, most companies show 0-10 additions
- **Usage:** Hiring velocity and growth analysis (with data quality caveats)

### employee_departures_count (INT64)
- **Range:** 0 to 16,422 departures per month
- **Missing Data:** 41.61% null values - highest missing rate
- **Distribution:** 3,540 unique values
- **Usage:** Attrition analysis and workforce stability metrics (limited by data availability)

## Query Considerations

### Optimal Filtering Columns:
- **month_date**: Excellent for time-based filtering and trend analysis
- **company_id**: Essential for company-specific analysis
- **total_employee_count**: Good for company size segmentation (0-10, 11-100, 101-1000, etc.)

### Grouping/Aggregation Opportunities:
- **Temporal grouping**: By year, quarter, or month for trend analysis
- **Company size buckets**: Small/medium/large enterprise analysis
- **Geographic analysis**: If company location data is available in related tables
- **Industry analysis**: If sector data is available in related tables

### Potential Join Keys:
- **company_id**: Primary key for joining with company profile, industry, or location tables
- **month_date**: Can join with economic indicators, market data, or external events

### Data Quality Considerations:
- **Missing departure data**: Queries involving employee_departures_count should account for 41.61% null values
- **Missing addition data**: 17.46% null rate for employee_additions_count requires careful handling
- **Zero vs. null distinction**: Zero values indicate measured zero activity; nulls indicate missing measurements
- **Time series gaps**: Companies may have missing months in their timeseries
- **Company lifecycle**: Some companies may appear/disappear from dataset over time

### Recommended Query Patterns:
- Use `total_employee_count` for reliable workforce size analysis
- Apply null-safe operations when using additions/departures metrics
- Consider rolling averages for smoothing monthly volatility
- Use window functions for growth rate calculations
- Filter out companies with insufficient data history for trend analysis

## Keywords
employee timeseries, workforce analytics, company headcount, hiring data, employee departures, monthly employment data, company growth tracking, HR analytics, workforce planning, employee additions, company size analysis, employment trends, business intelligence, people analytics

## Table and Column Documentation
*No table comment or column comments were provided in the source data.*