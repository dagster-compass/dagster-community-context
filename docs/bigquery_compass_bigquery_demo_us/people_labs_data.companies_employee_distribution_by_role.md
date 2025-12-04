---
columns:
- company_id (STRING)
- employee_count (INT64)
- role (STRING)
schema_hash: 51368c4f020428e9d698aaf80c8cd3744fb72c34ed4d1d8ed34fc89cbe090029

---
# Table Summary: people_labs_data.companies_employee_distribution_by_role

## Overall Dataset Characteristics

**Total Rows:** 22,588,172

**Dataset Purpose:** This table contains employee distribution data across different functional roles within companies. It represents a denormalized view where each row captures the count of employees in a specific role for a given company.

**Data Quality:** 
- Excellent completeness - no null values detected across any columns (0.00% null rate)
- High cardinality in company_id (10M+ unique values) relative to total rows, suggesting most companies have multiple role entries
- The data appears to be comprehensive and well-structured

**Notable Patterns:**
- Employee counts are heavily skewed toward smaller numbers (ranges 1-303,046, but likely concentrated in lower values)
- Average of ~2.2 role entries per company (22.6M rows / 10M companies)
- 24 distinct role categories provide standardized classification across all companies

## Column Details

### company_id (STRING)
- **Purpose:** Unique identifier for each company in the dataset
- **Cardinality:** 10,078,178 unique companies
- **Format:** Alphanumeric hash-like strings (e.g., "BYfSpBtrRReJwODKcaYlMQjbbuVF")
- **Null Values:** None (0.00%)
- **Usage:** Primary key component (in combination with role); essential for company-level aggregations and filtering
- **Data Quality:** Consistent format, no nulls, high quality identifier

### role (STRING)
- **Purpose:** Categorizes employees by their functional role/department
- **Cardinality:** 24 unique role categories
- **Null Values:** None (0.00%)
- **Known Values Include:**
  - advisory
  - analyst
  - creative
  - education
  - engineering
  - finance
  - fulfillment
  - health
  - hospitality
  - human_resources
  - other_uncategorized
  - partnerships
  - professional_service
  - support
- **Data Quality:** Standardized categorical values, consistent naming convention using snake_case
- **Distribution:** Sample suggests "other_uncategorized" and "support" are common categories

### employee_count (INT64)
- **Purpose:** Number of employees in the specified role for the company
- **Range:** 1 to 303,046 employees
- **Cardinality:** 5,454 unique values
- **Null Values:** None (0.00%)
- **Distribution Characteristics:**
  - Minimum: 1 employee
  - Maximum: 303,046 employees (likely a major corporation)
  - Sample values show heavy concentration at low counts (1, 2, 4)
  - Likely follows a power law distribution (many small values, few large values)
- **Data Quality:** Integer values, no nulls, realistic range

## Potential Query Considerations

### Filtering Opportunities
- **By Company:** `company_id` for company-specific analysis
- **By Role:** `role` to analyze specific functional areas (e.g., "engineering", "finance")
- **By Company Size:** `employee_count` thresholds to segment small/medium/large teams
- **Combined Filters:** Companies with specific role compositions

### Grouping/Aggregation Scenarios
- **Company-level aggregations:** 
  - Total employees per company: `SUM(employee_count) GROUP BY company_id`
  - Number of roles per company: `COUNT(DISTINCT role) GROUP BY company_id`
  - Role diversity metrics
  
- **Role-level aggregations:**
  - Total employees in each role across all companies: `SUM(employee_count) GROUP BY role`
  - Average team size by role: `AVG(employee_count) GROUP BY role`
  - Companies per role: `COUNT(DISTINCT company_id) GROUP BY role`

- **Distribution analysis:**
  - Employee count percentiles by role
  - Company size categories based on total employee count

### Join Considerations
- **company_id** is the natural join key to other company-related tables (e.g., company details, revenue, industry)
- Composite key (company_id + role) uniquely identifies each row
- Suitable for joining with employee-level data, company metadata, or industry benchmarks

### Data Quality Considerations
- No missing data concerns (0% null rate across all columns)
- **Completeness Question:** Does absence of a role for a company mean zero employees in that role, or missing data? Queries may need LEFT JOINs or COALESCE for complete role coverage
- **Large Value Handling:** The maximum employee_count (303K+) suggests presence of very large enterprises; percentile-based analysis recommended over simple averages
- **Role Standardization:** All roles use consistent snake_case naming; no special character handling needed
- **Temporal Considerations:** No timestamp column visible; this appears to be point-in-time data

### Performance Optimization Tips
- Index on `company_id` for company-specific queries
- Index on `role` for role-based filtering
- Consider partitioning by role for large-scale analytics
- For total employee calculations, SUM aggregations will be frequent

## Keywords
employee distribution, company roles, workforce composition, organizational structure, headcount by function, role analysis, employee count, company staffing, functional departments, team size, workforce analytics, HR metrics, company_id, engineering headcount, support staff, employee roles, company demographics, organizational breakdown, People Labs, workforce data, role categories, staff allocation, department size, employee segmentation

## Table and Column Documentation

**Table Comment:** Not provided in the analysis report

**Column Comments:**
- company_id: Not provided
- role: Not provided  
- employee_count: Not provided