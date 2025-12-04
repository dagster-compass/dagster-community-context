---
columns:
- company_id (STRING)
- employee_count (INT64)
- sub_role (STRING)
schema_hash: c6987d74945b29e0ce9bfcf62f9e4d90258cb4b9064c7d6a108bb0bbbcffca93

---
# Table Summary: people_labs_data.companies_employee_distribution_by_sub_role

## Overall Dataset Characteristics

This table contains **24,315,326 rows** representing employee distribution data across companies, categorized by specialized sub-roles. The dataset appears to be a dimension table that breaks down workforce composition by functional roles within organizations.

**Data Quality Observations:**
- Excellent data completeness with 0% null values across all columns
- High cardinality in company_id (10+ million unique companies)
- Relatively low cardinality in sub_role (106 distinct role categories)
- Employee counts range from single employees to over 300,000 per role/company combination

**Notable Patterns:**
- The dataset captures granular workforce segmentation across diverse business functions
- Small employee counts (1-10) appear to be very common based on sample values
- Distribution suggests many small companies or niche roles alongside large organizations

## Column Details

### company_id (STRING)
- **Data Type:** STRING identifier
- **Null Pattern:** No null values (0.00%)
- **Cardinality:** 10,078,178 unique companies
- **Format:** Alphanumeric hash-like identifiers (e.g., "tFy6F21QD1ZfyEnK6Eo3RQK5D2DK")
- **Characteristics:** 
  - Appears to be a unique company identifier/foreign key
  - Consistent length and format across entries
  - Case-sensitive alphanumeric strings

### sub_role (STRING)
- **Data Type:** STRING categorical
- **Null Pattern:** No null values (0.00%)
- **Cardinality:** 106 distinct role categories
- **Common Values Include:**
  - Business functions: account_executive, account_management, accounting, consulting, executive
  - Technical roles: devops, architecture
  - Specialized areas: academic, agriculture, fitness, investor
  - General category: other_uncategorized
- **Format:** Lowercase with underscores separating words
- **Characteristics:** Represents functional job categories/departments within companies

### employee_count (INT64)
- **Data Type:** Integer
- **Null Pattern:** No null values (0.00%)
- **Range:** 1 to 302,516 employees
- **Cardinality:** 5,390 distinct values
- **Distribution:** 
  - Small counts (1-10) appear frequently in samples
  - Maximum value (302,516) suggests very large organizations
  - Sample values show wide variance: 1, 4, 384
- **Characteristics:** Represents the number of employees in a specific sub_role at a company

## Potential Query Considerations

### Optimal for Filtering:
- **sub_role**: Excellent for filtering by specific job functions (106 categories provides good selectivity)
- **company_id**: Perfect for company-specific analysis or joining with other company tables
- **employee_count**: Can filter by company size or role prominence (e.g., WHERE employee_count > 100)

### Optimal for Grouping/Aggregation:
- **sub_role**: Ideal for aggregate analysis (e.g., total employees across all companies per role)
- **company_id**: Can group to see total employee distribution within a company
- Combined grouping (company_id + sub_role) represents the grain of this table

### Potential Join Keys:
- **company_id**: Primary join key to connect with other company dimension tables (company details, industry, location, etc.)
- This table likely serves as a fact table in a star schema

### Recommended Query Patterns:
1. **Role Distribution Analysis**: `GROUP BY sub_role` with `SUM(employee_count)`
2. **Company Workforce Composition**: `GROUP BY company_id` to see role diversity
3. **Large Organization Identification**: Filter by high employee_counts
4. **Role Prevalence**: Count distinct companies per sub_role

### Data Quality Considerations:
- **No missing data**: All queries can rely on complete values
- **Multiple rows per company**: Companies appear multiple times (once per sub_role), so aggregation needed for total company size
- **Outliers**: The maximum employee_count (302,516) suggests potential need for outlier handling in statistical analyses
- **Role granularity**: The "other_uncategorized" category may contain heterogeneous roles requiring special handling

### Performance Optimization Tips:
- Partition by sub_role if available for role-based queries
- Index on company_id for join operations
- Consider materialized views for common aggregations (total employees per company, per role)

## Keywords

employee distribution, workforce composition, job roles, sub-roles, company employees, organizational structure, headcount, functional roles, devops, accounting, executives, consulting, company_id, role categories, employee count, people analytics, workforce analytics, HR data, organizational data, company staffing

## Table and Column Documentation

**Table Comment:** Not provided

**Column Comments:** Not provided