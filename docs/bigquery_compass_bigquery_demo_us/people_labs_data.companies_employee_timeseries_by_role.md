---
columns:
- company_id (STRING)
- employee_count (INT64)
- month_date (STRING)
- role (STRING)
schema_hash: daa30e882102489651ee9c4f9b7f58e49ff75a6d55d403eddea5c32d7c360bc4

---
# Table Analysis Summary: companies_employee_timeseries_by_role

## Overall Dataset Characteristics

- **Total Rows**: 42,969,808,368 (~43 billion records)
- **Data Quality**: Excellent - 0% null values across all columns
- **Dataset Type**: Time-series data tracking employee counts by role across companies
- **Time Range**: January 2010 to April 2025 (188 months of data)
- **Coverage**: 16+ million unique companies tracked across 24 different role categories
- **Notable Pattern**: High frequency of zero employee counts in samples, suggesting sparse data or companies without employees in specific roles during certain periods

## Column Details

### company_id (STRING)
- **Purpose**: Unique identifier for each company
- **Cardinality**: 16,020,211 unique companies
- **Format**: 28-character alphanumeric strings (e.g., "TAWln52dmuqBb5h3lxjBsQKFoNI2")
- **Data Quality**: No nulls, highly unique identifiers
- **Use Case**: Primary key for joining with other company tables, filtering by specific companies

### month_date (STRING)
- **Purpose**: Time dimension for tracking employee counts
- **Format**: YYYY-MM (e.g., "2023-04", "2016-12")
- **Range**: 2010-01 to 2025-04 (188 unique months, ~15.7 years)
- **Data Quality**: No nulls, consistent format
- **Notable**: Includes future dates (2025), suggesting forecasting or data collection through current date
- **Use Case**: Time-series filtering, trending analysis, year-over-year comparisons

### role (STRING)
- **Purpose**: Categorizes employees by their functional role
- **Cardinality**: 24 unique role types
- **Known Values**: 
  - advisory, analyst, creative, education, engineering
  - finance, fulfillment, health, hospitality, human_resources
  - legal, other_uncategorized, operations (from samples)
- **Data Quality**: No nulls, standardized categorical values
- **Use Case**: Role-based analysis, filtering by department, aggregating workforce composition

### employee_count (INT64)
- **Purpose**: Number of employees in a specific role at a company during a given month
- **Range**: 0 to 304,921 employees
- **Cardinality**: 39,377 unique values
- **Distribution**: Many zero values observed in samples, maximum suggests large enterprise data included
- **Data Quality**: No nulls, non-negative integers
- **Use Case**: Aggregation, trending, growth analysis, company size classification

## Potential Query Considerations

### Excellent for Filtering:
- **company_id**: Direct company lookups, multi-company comparisons
- **month_date**: Time-range queries, specific period analysis (use string comparison or PARSE_DATE)
- **role**: Department-specific analysis, filtering for technical vs. non-technical roles
- **employee_count**: Finding companies above/below size thresholds (e.g., WHERE employee_count > 100)

### Excellent for Grouping/Aggregation:
- **role**: Aggregate workforce distribution across companies
- **month_date**: Time-series aggregations, monthly/quarterly/yearly rollups
- **company_id**: Per-company statistics, company-level summaries
- **Combinations**: Company growth by role over time, industry trends by month

### Join Key Candidates:
- **company_id**: Primary join key to other company dimension tables (company profiles, industry, location, etc.)
- **month_date**: Could join to economic indicators, market data, or other time-series datasets
- **role**: Could map to role hierarchies or classification tables

### Data Quality Considerations for Queries:

1. **Sparse Data**: Many zero employee counts suggest not all companies have employees in all roles during all periods. Consider:
   - Filtering out zeros if analyzing active roles
   - Using SUM vs COUNT carefully in aggregations
   - Handling missing role-month combinations

2. **Scale**: With 43 billion rows, queries require careful optimization:
   - Always filter on indexed columns (likely company_id, month_date)
   - Use partitioning by month_date for time-range queries
   - Consider sampling for exploratory analysis
   - Aggregate before JOINs when possible

3. **String Date Format**: month_date as STRING requires:
   - PARSE_DATE function for date operations
   - String comparison works for filtering (e.g., WHERE month_date >= '2020-01')
   - Extract year/quarter using string functions or date parsing

4. **Temporal Considerations**:
   - Future dates present (2025-04) - may need filtering for historical analysis
   - Check for data completeness across all months
   - Consider lag time in data availability for recent months

5. **Role Analysis**:
   - "other_uncategorized" category may need special handling
   - 24 roles provide granular analysis but may need grouping for high-level insights
   - Consider creating role hierarchies (technical, business, support, etc.)

## Keywords

timeseries, time series, employee count, headcount, workforce, employment, company size, role, department, function, job function, growth, hiring, staffing, organizational structure, personnel, human resources, workforce analytics, employee trends, company growth, temporal data, monthly data, role distribution, department size, company metrics, people analytics, talent analytics

## Table and Column Documentation

**Table Comment**: Not provided

**Column Comments**: 
- company_id: Not provided
- month_date: Not provided
- role: Not provided
- employee_count: Not provided