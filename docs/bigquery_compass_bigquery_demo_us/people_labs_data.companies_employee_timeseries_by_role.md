---
columns:
- company_id (STRING)
- employee_count (INT64)
- month_date (STRING)
- role (STRING)
schema_hash: daa30e882102489651ee9c4f9b7f58e49ff75a6d55d403eddea5c32d7c360bc4

---
# Table Summary: companies_employee_timeseries_by_role

## Overall Dataset Characteristics

**Total Rows:** 42,969,808,368 (~43 billion records)

**General Description:** This is a massive time-series dataset tracking employee counts by role across companies over time. The data spans from 2010 to 2025 (188 unique months) and covers over 16 million unique companies with 24 distinct role categories.

**Data Quality:** Excellent - all columns show 0% null values, indicating complete data coverage across all dimensions.

**Notable Patterns:**
- The dataset is heavily sparse with many zero-count entries (as evidenced by sample data)
- Employee counts range from 0 to 304,921, suggesting coverage of companies from startups to large enterprises
- The presence of zeros suggests the dataset tracks historical snapshots even when no employees existed in certain roles
- Monthly granularity provides fine-grained temporal analysis capability

---

## Column Details

### **company_id** (STRING)
- **Purpose:** Unique identifier for each company in the dataset
- **Cardinality:** 16,020,211 unique companies
- **Format:** 32-character alphanumeric strings (e.g., "G7B3FHvnz46gSdlhET2ptQ5yZKd6")
- **Data Quality:** Complete (0% nulls), highly unique
- **Query Usage:** Primary dimension for filtering, grouping, and joining to company master tables

### **month_date** (STRING)
- **Purpose:** Time dimension representing the month of the employee count snapshot
- **Cardinality:** 188 unique months
- **Format:** YYYY-MM format (e.g., "2015-10", "2023-09")
- **Time Range:** January 2010 to June 2025 (includes future projections/forecasts)
- **Data Quality:** Complete (0% nulls)
- **Query Usage:** Time-based filtering, trend analysis, time-series aggregations
- **Note:** Stored as STRING rather than DATE type; queries may need PARSE_DATE() conversions

### **role** (STRING)
- **Purpose:** Categorical dimension for employee job function/department
- **Cardinality:** 24 unique role types
- **Known Values Include:**
  - Business functions: sales, sales_engineering, finance, human_resources, legal
  - Technical: engineering, analyst, research
  - Operational: fulfillment, support, hospitality
  - Other: advisory, creative, education, health, other_uncategorized
- **Data Quality:** Complete (0% nulls)
- **Query Usage:** Primary grouping dimension for role-based analysis, filtering by department

### **employee_count** (INT64)
- **Purpose:** Metric representing the number of employees in a specific role at a company for a given month
- **Cardinality:** 39,377 unique values
- **Range:** 0 to 304,921
- **Distribution:** Heavily skewed toward lower values (many zeros in sample data)
- **Data Quality:** Complete (0% nulls), includes zero counts
- **Query Usage:** Primary metric for aggregation (SUM, AVG, MAX), trend calculations, growth analysis

---

## Potential Query Considerations

### **Filtering Strategies:**
1. **company_id:** Essential for company-specific analysis; exact match filtering
2. **month_date:** Use range filters for time periods (e.g., `>= '2020-01' AND <= '2023-12'`); consider parsing to DATE for date functions
3. **role:** Use IN clauses for multiple roles; good for categorical filtering
4. **employee_count:** Filter out zeros if analyzing only populated roles (`WHERE employee_count > 0`)

### **Grouping/Aggregation Opportunities:**
- **Time-series analysis:** Group by month_date for trends
- **Role analysis:** Group by role to compare departments
- **Company benchmarking:** Group by company_id for company-level metrics
- **Multi-dimensional:** Combine dimensions (e.g., role trends by month)
- **Aggregation metrics:** SUM(employee_count), AVG(employee_count), MAX(employee_count), COUNT(DISTINCT company_id)

### **Join Considerations:**
- **company_id** is likely a foreign key to a companies master table
- Could join to company metadata (industry, size, location, founding date)
- Self-joins possible for period-over-period comparisons
- Role dimension might join to a role taxonomy/hierarchy table

### **Data Quality Considerations:**
1. **Zero counts:** Determine whether to include/exclude in analysis (sparse data)
2. **Future dates:** Data includes 2025 months - verify if projections or actual data
3. **Date format:** STRING type requires parsing for date arithmetic
4. **Scale:** 43B rows requires careful query optimization:
   - Use WHERE clauses to filter early
   - Consider date range partitioning
   - Avoid SELECT * queries
   - Use LIMIT for exploratory queries
5. **Missing role combinations:** Not all companies will have all 24 roles in all months

### **Performance Optimization Tips:**
- Filter on company_id and month_date early to reduce scan size
- Consider clustering on company_id or month_date if table supports it
- Use approximate aggregation functions (APPROX_COUNT_DISTINCT) for large-scale queries
- Partition filters on month_date will be critical for performance

---

## Keywords

`employee timeseries`, `workforce data`, `headcount tracking`, `role-based employment`, `company employment history`, `department staffing`, `employee count by role`, `monthly snapshots`, `organizational structure`, `workforce analytics`, `staffing levels`, `human capital data`, `employment trends`, `departmental headcount`, `time-series workforce data`, `company staffing history`, `role distribution`, `employee metrics`, `workforce composition`, `people analytics`

---

## Table and Column Documentation

**Table Comment:** Not provided

**Column Comments:** 
- company_id: Not provided
- month_date: Not provided
- role: Not provided
- employee_count: Not provided