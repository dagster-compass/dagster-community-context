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
- **Data Quality**: Excellent - no null values across all columns (0.00% null rate)
- **Dataset Type**: Employee distribution data aggregated by company and sub-role
- **Notable Patterns**: 
  - High granularity with over 10 million unique companies
  - 106 distinct sub-roles representing various job functions
  - Employee counts range from 1 to over 300,000, indicating companies of all sizes
  - Most common employee counts are small (1-10), suggesting many small companies or niche roles

## Column Details

### company_id (STRING)
- **Data Type**: String identifier
- **Null Values**: None (0.00%)
- **Uniqueness**: 10,078,178 unique companies (~41% of total rows)
- **Format**: Alphanumeric hash-like identifiers (e.g., "MZR4TNSB6x8QTBIe5ZfFBQuYhl1C")
- **Usage**: Primary key for joining with other company tables

### sub_role (STRING)
- **Data Type**: Categorical string
- **Null Values**: None (0.00%)
- **Uniqueness**: 106 distinct sub-roles
- **Common Categories**: administrative, logistics, chemical, account_executive, accounting, etc.
- **Pattern**: Represents specific job functions/departments within companies
- **Usage**: Ideal for grouping and filtering by job function

### employee_count (INT64)
- **Data Type**: Integer
- **Null Values**: None (0.00%)
- **Range**: 1 to 302,516 employees
- **Distribution**: 5,390 unique values, heavily skewed toward smaller counts
- **Pattern**: Most sample values show count of 1, indicating many companies have single employees in specific sub-roles
- **Usage**: Perfect for aggregation, filtering, and statistical analysis

## Potential Query Considerations

### Filtering Opportunities
- **sub_role**: Excellent for filtering by job function (e.g., 'administrative', 'logistics', 'accounting')
- **employee_count**: Good for filtering by company size ranges (e.g., WHERE employee_count > 100)
- **company_id**: Useful for filtering specific companies

### Grouping/Aggregation Potential
- **sub_role**: Primary grouping dimension for analyzing workforce distribution across job functions
- **employee_count ranges**: Can create size buckets (small: 1-10, medium: 11-100, large: 100+)
- **Company-level aggregations**: Sum employee_count by company_id for total workforce

### Join Considerations
- **company_id**: Primary join key to connect with other company-related tables
- Consider joining with company metadata tables for industry, location, or company details

### Data Quality Considerations
- **Excellent data completeness**: No missing values to handle
- **Potential duplicates**: Multiple rows per company (one per sub-role) - this is expected structure
- **Scale considerations**: Large dataset (24M+ rows) may require optimization for complex queries
- **Employee count validation**: Verify if counts represent full-time equivalents, headcount, or other metrics

## Keywords

employee distribution, workforce analytics, company staffing, job roles, sub-roles, headcount, organizational structure, employment data, company demographics, people analytics, HR analytics, staffing levels, job functions, company size analysis

## Table and Column Documentation

**Table Comment**: Not provided in the analysis report.

**Column Comments**: No column-specific comments were provided in the analysis report.