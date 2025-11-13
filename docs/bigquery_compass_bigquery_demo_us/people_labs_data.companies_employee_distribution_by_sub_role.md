---
columns:
- company_id (STRING)
- employee_count (INT64)
- sub_role (STRING)
schema_hash: c6987d74945b29e0ce9bfcf62f9e4d90258cb4b9064c7d6a108bb0bbbcffca93

---
# Table Summary: people_labs_data.companies_employee_distribution_by_sub_role

## Overall Dataset Characteristics

This table contains **24,315,326 rows** representing the distribution of employees across different sub-roles within companies. The dataset appears to be a denormalized fact table that breaks down employee counts by company and functional sub-role, likely used for workforce analytics and organizational structure analysis.

**Data Quality Observations:**
- **Excellent completeness**: All columns have 0% null values
- **High granularity**: Over 10 million unique companies represented
- **Standardized categorization**: 106 distinct sub-role categories
- **Wide value range**: Employee counts range from 1 to 302,516, suggesting the dataset includes companies of all sizes from startups to large enterprises

**Notable Patterns:**
- The presence of "other_uncategorized" as a sub_role suggests a catch-all category for roles that don't fit standard classifications
- Employee counts follow a long-tail distribution typical of organizational hierarchies
- The table structure suggests a many-to-many relationship between companies and sub-roles (one company can have multiple sub-roles, each with different employee counts)

## Column Details

### company_id (STRING)
- **Type**: Alphanumeric identifier (appears to be a hash or encoded ID)
- **Cardinality**: 10,078,178 unique companies
- **Format**: Fixed-length alphanumeric strings (e.g., "V13qLfzYBVIZAvzO5sktHAJhCiBJ")
- **Null Values**: None (0%)
- **Purpose**: Primary key component for identifying distinct companies
- **Pattern**: Each company_id appears multiple times (average ~2.4 rows per company), indicating companies typically have employees distributed across multiple sub-roles

### sub_role (STRING)
- **Type**: Categorical text field
- **Cardinality**: 106 distinct sub-roles
- **Null Values**: None (0%)
- **Common Categories Include**:
  - Business functions: account_executive, account_management, accounting, administrative
  - Technical roles: architecture, project_management
  - Leadership: executive, advisor
  - Specialized: academic, agriculture, aides, accounting_services
  - Miscellaneous: other_uncategorized, growth
- **Format**: Lowercase with underscores separating words
- **Purpose**: Classifies the functional role or department of employees within organizations

### employee_count (INT64)
- **Type**: Integer
- **Range**: 1 to 302,516 employees
- **Cardinality**: 5,390 unique values
- **Null Values**: None (0%)
- **Distribution**: 
  - Small counts (1-10) are most common based on samples
  - Maximum of 302,516 suggests representation of very large organizations
  - The wide range indicates companies of all sizes from small businesses to Fortune 500 enterprises
- **Purpose**: Quantifies the number of employees in each sub_role for each company

## Potential Query Considerations

### Filtering Opportunities
- **sub_role**: Excellent for filtering by functional area (e.g., WHERE sub_role = 'executive' for C-suite analysis)
- **employee_count**: Useful for segmenting companies by size or role concentration (e.g., WHERE employee_count > 100 for large departments)
- **company_id**: Essential for company-specific analysis or joining to company dimension tables

### Grouping/Aggregation Patterns
- **Aggregate by sub_role**: Calculate total employees per role type across all companies (e.g., `SUM(employee_count) GROUP BY sub_role`)
- **Company-level aggregation**: Total employees per company by summing across all sub_roles
- **Distribution analysis**: Count of companies per sub_role, average employees per role, percentile analysis
- **Size segmentation**: Group companies by total employee count ranges

### Join Considerations
- **company_id** is the natural join key to link with:
  - Company master/dimension tables (for company name, industry, location, etc.)
  - Financial data tables
  - Company metadata or profile tables
- Likely part of a star schema where this is a fact table

### Data Quality Considerations for Queries
1. **Multiple rows per company**: Queries calculating total company headcount must SUM across all sub_roles for each company_id
2. **"other_uncategorized" handling**: May need special treatment or exclusion depending on analysis goals
3. **Large result sets**: Queries without proper filtering may return millions of rows
4. **Distribution skew**: The maximum employee_count (302K+) suggests potential outliers that could affect aggregate calculations
5. **Role standardization**: The 106 sub_roles may need grouping into higher-level categories for some analyses

## Keywords

workforce analytics, employee distribution, organizational structure, headcount by role, company staffing, functional roles, job categories, personnel breakdown, talent composition, organizational hierarchy, company size, department distribution, role taxonomy, employment data, people analytics, sub-role classification, staffing levels, workforce segmentation

## Table and Column Documentation

**Table Comment**: Not provided

**Column Comments**: Not provided