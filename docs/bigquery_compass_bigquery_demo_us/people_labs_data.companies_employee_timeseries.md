---
columns:
- company_id (STRING)
- employee_additions_count (INT64)
- employee_departures_count (INT64)
- month_date (STRING)
- total_employee_count (INT64)
schema_hash: 79523b2b19040120bf40e40186db1d6f50f4e640a6d1ba170a495487fadaaafb

---
# Table Analysis Summary: people_labs_data.companies_employee_timeseries

## Overall Dataset Characteristics

This is a large-scale employee time series dataset containing **1.79 billion rows** tracking monthly employee counts and changes for approximately 16 million companies. The data spans from 2010 to at least 2025 (188 unique months), providing a comprehensive view of workforce dynamics across organizations.

**Data Quality Observations:**
- High data completeness for core metrics (month_date and total_employee_count have 0% nulls)
- Significant missing data for employee movement metrics (17.46% nulls for additions, 41.61% nulls for departures)
- The high null percentage in departures suggests this metric may be harder to track or calculate
- Future dates (e.g., 2025-05) indicate this may include projected or estimated data

**Notable Patterns:**
- Wide range in company sizes (0 to 542,509 employees)
- Most companies appear to be small (sample data shows many single-employee companies)
- Employee changes range from 0 to over 30,000 in a single month for additions

## Column Details

### month_date (STRING)
- **Format:** YYYY-MM format representing monthly periods
- **Coverage:** 188 unique months spanning approximately 15+ years (2010-2025+)
- **Data Quality:** Complete (0% nulls)
- **Usage:** Primary time dimension for temporal analysis and filtering

### company_id (STRING)
- **Format:** Alphanumeric identifier (32-character hash-like strings)
- **Uniqueness:** 16,020,211 unique companies
- **Data Quality:** Complete (0% nulls)
- **Usage:** Primary entity identifier for grouping and company-specific analysis

### total_employee_count (INT64)
- **Range:** 0 to 542,509 employees
- **Distribution:** 57,786 unique values, heavily skewed toward smaller companies
- **Data Quality:** Complete (0% nulls)
- **Usage:** Key metric for company size analysis, growth tracking, and segmentation

### employee_additions_count (INT64)
- **Range:** 0 to 30,333 new hires per month
- **Missing Data:** 17.46% null values
- **Distribution:** 4,376 unique values
- **Usage:** Hiring activity analysis, growth momentum tracking

### employee_departures_count (INT64)
- **Range:** 0 to 16,422 departures per month
- **Missing Data:** 41.61% null values (highest among all columns)
- **Distribution:** 3,540 unique values
- **Usage:** Turnover analysis, retention studies (when available)

## Query Considerations

### Filtering Opportunities
- **Time-based filtering:** `month_date` for specific periods or date ranges
- **Company size filtering:** `total_employee_count` for company size segments
- **Activity filtering:** Non-null `employee_additions_count` or `employee_departures_count` for companies with recorded changes

### Grouping/Aggregation Potential
- **Temporal aggregation:** By month, quarter, or year using `month_date`
- **Company segmentation:** By employee count ranges (small/medium/large companies)
- **Growth analysis:** Companies with consistent addition/departure data

### Join Considerations
- **Primary key:** Likely `company_id` + `month_date` combination
- **Foreign key potential:** `company_id` could join with company master data tables
- **Time series integrity:** Each company should have monthly records for analysis

### Data Quality Considerations
- **Handle nulls carefully:** Especially for employee movement metrics
- **Consider data completeness:** Filter for companies with sufficient historical data
- **Validate date ranges:** Be aware of future dates that may be projections
- **Size validation:** Very large employee counts (>100k) may need verification
- **Movement logic:** Additions + Previous Total - Departures should equal Current Total (when all data available)

## Keywords
employee timeseries, workforce analytics, company growth, hiring trends, employee turnover, monthly employment data, company size analysis, people analytics, HR metrics, organizational growth, headcount tracking, talent acquisition, retention analysis, business intelligence

## Table and Column Documentation
*No table comment or column comments were provided in the source analysis.*