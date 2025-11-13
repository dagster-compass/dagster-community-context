---
columns:
- company_id (STRING)
- employee_additions_count (INT64)
- employee_departures_count (INT64)
- month_date (STRING)
- total_employee_count (INT64)
schema_hash: 79523b2b19040120bf40e40186db1d6f50f4e640a6d1ba170a495487fadaaafb

---
# Companies Employee Timeseries - Comprehensive Data Summary

## Overall Dataset Characteristics

**Dataset Size:** 1,790,408,682 rows (approximately 1.79 billion records)

**Data Quality Observations:**
- This is a very large-scale employee tracking dataset covering company workforce changes over time
- Moderate data quality with some null values in employee movement columns
- Time series data spanning from 2010 to approximately 2023 (188 unique months)
- Data appears to be point-in-time snapshots of employee counts for companies on a monthly basis

**Notable Patterns:**
- Significant null percentages in employee additions (17.46%) and departures (41.61%), suggesting these metrics may not be available for all company-month combinations
- Many companies show zero employee counts, indicating either defunct companies, data collection gaps, or companies without detectable employees
- The dataset tracks over 16 million unique companies, indicating comprehensive business coverage

**Distribution Insights:**
- Employee counts range from 0 to over 542,000 (likely major corporations)
- Most companies appear to be small (employee counts showing 0-9 as common values)
- Employee additions and departures are generally small numbers (most under 10), with rare large spikes

## Column Details

### month_date (STRING)
- **Type:** Date string in YYYY-MM format
- **Null Pattern:** No null values (0.00%)
- **Coverage:** 188 unique months spanning 2010-01 through approximately 2023-04
- **Format:** Consistent YYYY-MM pattern
- **Purpose:** Temporal dimension for time series analysis
- **Sample Dates:** 2010-01 through 2010-10, 2017-03, 2019-12, 2023-04

### total_employee_count (INT64)
- **Type:** Integer
- **Null Pattern:** No null values (0.00%)
- **Range:** 0 to 542,509
- **Distribution:** 57,786 unique values; heavily skewed toward lower counts (0-9 are common)
- **Interpretation:** Snapshot of total workforce size at month end
- **Zero Values:** Common, indicating companies with no tracked employees

### employee_additions_count (INT64)
- **Type:** Integer
- **Null Pattern:** 17.46% null values (312.6 million records)
- **Range:** 0 to 30,333
- **Distribution:** 4,376 unique values; most values are 0-8
- **Interpretation:** Number of new hires/additions during the month
- **Null Meaning:** Likely indicates no data available for that month or company

### employee_departures_count (INT64)
- **Type:** Integer
- **Null Pattern:** 41.61% null values (745.1 million records)
- **Range:** 0 to 16,422
- **Distribution:** 3,540 unique values; most values are 0-8
- **Interpretation:** Number of employees who left during the month
- **Null Meaning:** Likely indicates no data available; higher null rate than additions suggests departures are harder to track

### company_id (STRING)
- **Type:** String identifier
- **Null Pattern:** No null values (0.00%)
- **Unique Values:** 16,020,211 companies
- **Format:** 28-character alphanumeric hash (e.g., "HiU2m9VfuhbcatbliB17TwwuSfBI")
- **Purpose:** Primary identifier for joining with other company dimension tables
- **Cardinality:** Very high - each company tracked across multiple months

## Potential Query Considerations

### Filtering Columns
- **month_date:** Excellent for time-based filtering and windowing
  - Use for trend analysis, year-over-year comparisons, or specific time periods
  - Consider filtering recent dates for current workforce analysis
- **total_employee_count:** Filter by company size segments (startups, SMBs, enterprises)
- **company_id:** Direct lookup for specific company analysis
- **Zero/Null patterns:** Filter out zero-employee companies for active company analysis

### Grouping/Aggregation Columns
- **month_date:** Primary grouping for time series aggregations
  - Calculate monthly hiring/departure rates
  - Seasonal trend analysis
  - Growth rate calculations
- **company_id:** Group to get company-level statistics over time
- **Size bands:** Create calculated fields from total_employee_count for cohort analysis

### Join Keys
- **company_id:** Primary key for joining with:
  - Company dimension tables (name, industry, location, founding date)
  - Funding/financial tables
  - Company metadata or classification tables
- Consider creating composite keys with month_date for specific point-in-time joins

### Data Quality Considerations

**Null Handling:**
- **Critical:** Always account for nulls in employee_additions_count (17.46%) and employee_departures_count (41.61%)
- Use COALESCE or IFNULL for calculations, or explicitly filter WHERE IS NOT NULL
- Consider separate analyses for records with complete vs. incomplete data

**Zero Values:**
- Many companies show 0 employees - determine if these should be excluded
- Zero additions/departures may be legitimate or data quality issues

**Temporal Gaps:**
- Not all companies may have continuous monthly records
- Use window functions carefully; gaps may affect LAG/LEAD calculations

**Data Freshness:**
- Most recent data appears to be 2023-04; verify currency for current analysis
- Historical data starts 2010-01; pre-2010 trends unavailable

**Volume Considerations:**
- 1.79 billion rows requires query optimization
- Use WHERE clauses to filter early in query execution
- Consider partitioning strategies by month_date
- Aggregations should be performed thoughtfully to manage processing time

**Calculation Recommendations:**
- Growth rates: Use LAG/LEAD with PARTITION BY company_id ORDER BY month_date
- Retention calculations: May be imperfect due to null departure data
- Net change validation: total_employee_count changes should approximate (additions - departures)

## Keywords

timeseries, employees, workforce, headcount, hiring, attrition, departures, additions, company growth, employment trends, monthly data, workforce analytics, HR metrics, company size, organizational growth, employee churn, recruitment metrics, time series analysis, business intelligence, people analytics, staffing levels, workforce planning

## Table and Column Documentation

**Table Comment:** Not provided

**Column Comments:** Not provided