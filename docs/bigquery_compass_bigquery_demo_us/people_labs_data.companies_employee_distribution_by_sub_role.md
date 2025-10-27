---
columns:
- company_id (STRING)
- employee_count (INT64)
- sub_role (STRING)
schema_hash: c6987d74945b29e0ce9bfcf62f9e4d90258cb4b9064c7d6a108bb0bbbcffca93

---
# Table Summary: people_labs_data.companies_employee_distribution_by_sub_role

## Overall Dataset Characteristics

- **Total Rows**: 24,315,326 records
- **Data Quality**: Excellent - no null values detected in any column
- **Structure**: Company-level employee distribution data organized by functional sub-roles
- **Scale**: Covers over 10 million unique companies with detailed role-based workforce breakdowns
- **Distribution Pattern**: Most companies appear to have small employee counts (1-10 range is common), with some large enterprises having hundreds of thousands of employees

## Column Details

### sub_role (STRING)
- **Data Type**: String/categorical
- **Null Values**: 0% - complete data
- **Unique Values**: 106 distinct sub-roles
- **Value Patterns**: Professional function categories including:
  - Business functions: account_executive, account_management, accounting, administrative
  - Technical roles: mechanic, nursing, legal
  - Specialized areas: agriculture, architecture, journalism, product_management, recruiting
- **Usage**: Primary grouping dimension for workforce analysis

### employee_count (INT64)
- **Data Type**: Integer
- **Null Values**: 0% - complete data
- **Range**: 1 to 302,516 employees
- **Unique Values**: 5,390 distinct counts
- **Distribution**: Heavy concentration in lower ranges (1-10), indicating many small companies
- **Usage**: Quantitative measure for aggregations and size-based filtering

### company_id (STRING)
- **Data Type**: String identifier
- **Null Values**: 0% - complete data
- **Unique Values**: 10,078,178 distinct companies
- **Format**: Alphanumeric hash-like identifiers (e.g., "thJcFG2B4pAE5dnLC9fxPgxEeXjA")
- **Usage**: Primary key for company-level operations and joins

## Potential Query Considerations

### Filtering Opportunities
- **sub_role**: Excellent for filtering by specific job functions or role categories
- **employee_count**: Good for size-based filtering (small/medium/large companies)
- **company_id**: Essential for company-specific lookups

### Grouping/Aggregation Potential
- **sub_role**: Primary dimension for workforce composition analysis
- **Employee size bands**: Create size categories from employee_count for market segmentation
- **Cross-tabulation**: Role distribution patterns across company sizes

### Join Capabilities
- **company_id**: Primary join key for linking with other company datasets
- Likely connects to company profile, industry, location, or financial data tables

### Data Quality Considerations
- **Complete Data**: No missing values simplifies query logic
- **Large Scale**: Queries should consider performance implications with 24M+ rows
- **Cardinality**: High company_id cardinality may require indexed access patterns
- **Role Standardization**: Sub-roles appear standardized and consistently formatted

## Keywords

employee distribution, workforce composition, company roles, sub-roles, organizational structure, people analytics, company size, employee count, business functions, job categories, workforce analysis, company demographics, role-based analytics, organizational data, people labs, employee segmentation

## Table and Column Documentation

**Table Comment**: Not provided in the analysis report.

**Column Comments**: No specific column comments were provided in the analysis report.