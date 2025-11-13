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

**General Description:** This table contains employee distribution data across different roles for companies. It represents a many-to-many relationship where each company can have multiple role entries, with each entry showing the count of employees in that specific role.

**Data Quality:** Excellent - no null values detected in any column (0.00% null percentage across all fields).

**Key Patterns:**
- The dataset covers over 10 million unique companies
- Employee counts range from 1 to 303,046 per role per company, suggesting coverage from small startups to large enterprises
- 24 distinct role categories are tracked
- Most entries appear to have small employee counts (1-10), with 303,046 being an outlier maximum

## Column Details

### 1. company_id (STRING)
- **Type:** String identifier
- **Nulls:** None (0.00%)
- **Cardinality:** 10,078,178 unique companies
- **Format:** Alphanumeric hash-like identifiers (e.g., "nBb7d4SMLIS95ywqvDKirQFaHdEv")
- **Purpose:** Primary identifier for companies; serves as the linking key to other company-related tables
- **Distribution:** High cardinality indicates this is a granular company-level dataset

### 2. role (STRING)
- **Type:** Categorical string
- **Nulls:** None (0.00%)
- **Cardinality:** 24 unique values
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
  - operations
  - product
  - professional_service
  - research
  - other_uncategorized
- **Pattern:** Snake_case naming convention for multi-word roles
- **Purpose:** Categorizes employee functions within companies

### 3. employee_count (INT64)
- **Type:** Integer
- **Nulls:** None (0.00%)
- **Range:** 1 to 303,046
- **Cardinality:** 5,454 unique values
- **Distribution:** Heavily skewed toward lower values (sample shows mostly 1-3), with maximum of 303,046 indicating large enterprise presence
- **Purpose:** Quantifies the number of employees in each role per company

## Potential Query Considerations

### Filtering Recommendations:
- **role:** Excellent for filtering by job function categories (24 distinct values make it efficient)
- **employee_count:** Good for filtering by company size thresholds (e.g., `WHERE employee_count > 100`)
- **company_id:** Essential for company-specific analysis

### Grouping/Aggregation Opportunities:
- **By role:** Calculate total employees across roles, identify most common roles
- **By company_id:** Get total employee distribution per company across all roles
- **By employee_count ranges:** Segment companies by size (small, medium, large)
- **Combined groupings:** Role distribution analysis by company size segments

### Join Considerations:
- **company_id** is the natural join key to other company tables
- This table likely joins with:
  - Company master/profile tables
  - Company metadata (industry, location, funding, etc.)
  - Other employee-related tables

### Data Quality Considerations:
- No missing data handling required (0% nulls)
- Consider that a company may appear multiple times (once per role)
- The "other_uncategorized" role may need special handling in analysis
- Maximum employee_count (303,046) suggests possible data aggregation at enterprise level
- Sum of employee_counts per company_id would give total company size

### Performance Tips:
- company_id and role combination likely represents the grain of the table
- Queries filtering on specific roles will be efficient
- Aggregations by role will be performant due to low cardinality (24 values)
- Consider indexing on company_id for join performance

## Keywords

company employees, employee distribution, workforce composition, organizational structure, role analysis, job functions, company staffing, headcount by role, employee segmentation, workforce analytics, company size, human resources data, organizational roles, employee counts, staff allocation, company workforce, employment data, role categories, people analytics, company intelligence

## Table and Column Documentation

**Table Comment:** Not provided in the analysis report.

**Column Comments:** 
- company_id: Not provided
- role: Not provided  
- employee_count: Not provided