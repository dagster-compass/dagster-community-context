---
columns:
- company_id (STRING)
- employee_count (INT64)
- sub_role (STRING)
schema_hash: c6987d74945b29e0ce9bfcf62f9e4d90258cb4b9064c7d6a108bb0bbbcffca93

---
# Table Summary: people_labs_data.companies_employee_distribution_by_sub_role

## Overall Dataset Characteristics

This table contains **24,315,326 rows** representing the distribution of employees across different sub-roles (job functions) within companies. 

**Key Observations:**
- **Excellent data quality**: 0% null values across all columns
- **Granular company-level data**: Over 10 million unique companies
- **Comprehensive role taxonomy**: 106 distinct sub-role categories
- **Wide distribution of company sizes**: Employee counts range from 1 to 302,516 per sub-role per company
- **Many-to-many relationship**: Each company can have multiple sub-roles, and each sub-role appears across multiple companies
- **Table comment**: Not provided

## Column Details

### company_id (STRING)
- **Purpose**: Primary identifier for companies
- **Data Type**: String (hash-based identifier)
- **Completeness**: 100% populated (0% null)
- **Cardinality**: 10,078,178 unique companies
- **Format**: Alphanumeric hash strings (e.g., "xTtBnzbFoBFiU3Ki8aV3jAgtq8LR")
- **Pattern**: Appears to be a consistent-length encoded identifier
- **Column comment**: Not provided

### sub_role (STRING)
- **Purpose**: Categorizes job functions/roles within organizations
- **Data Type**: String (categorical)
- **Completeness**: 100% populated (0% null)
- **Cardinality**: 106 unique sub-roles
- **Common Categories Include**:
  - Executive functions: executive, advisor
  - Technical roles: product_management, product_design, architecture
  - Sales/Business: account_executive, account_management, business_development
  - Operations: accounting, accounting_services, administrative
  - Customer-facing: customer_success
  - Industry-specific: agriculture, academic, aides
  - Education: primary_and_secondary
  - Catch-all: other_uncategorized
- **Format**: Lowercase with underscores (snake_case)
- **Column comment**: Not provided

### employee_count (INT64)
- **Purpose**: Number of employees in a specific sub-role at a given company
- **Data Type**: Integer
- **Completeness**: 100% populated (0% null)
- **Range**: 1 to 302,516 employees
- **Distribution**: 
  - 5,390 unique values
  - Lower counts (1-10) appear most frequently in samples
  - Maximum of 302,516 suggests very large organizations in dataset
- **Pattern**: Positive integers only, no zeros (companies only represented if they have employees in that role)
- **Column comment**: Not provided

## Potential Query Considerations

### Optimal for Filtering:
- **sub_role**: Excellent for filtering by specific job functions (e.g., `WHERE sub_role = 'executive'`)
- **company_id**: Essential for company-specific queries
- **employee_count**: Good for filtering by company size in specific roles (e.g., `WHERE employee_count > 100`)

### Optimal for Grouping/Aggregation:
- **sub_role**: Primary dimension for workforce analysis (e.g., distribution of roles across industries)
- **company_id**: For calculating total employees per company, role diversity per company
- **employee_count**: For aggregations like SUM, AVG, MAX to understand workforce composition

### Potential Join Keys:
- **company_id**: Primary join key to other company-related tables (firmographics, financials, locations, etc.)
- Could join to employee detail tables, company profile tables, or industry classification tables

### Recommended Query Patterns:

1. **Company workforce composition**: 
   ```sql
   GROUP BY company_id, sub_role
   ```

2. **Role distribution analysis**:
   ```sql
   GROUP BY sub_role 
   AGGREGATE SUM(employee_count)
   ```

3. **Company size by role**:
   ```sql
   WHERE sub_role IN ('executive', 'sales', 'engineering')
   GROUP BY company_id
   ```

4. **Large department identification**:
   ```sql
   WHERE employee_count > threshold
   ```

### Data Quality Considerations:

- **No null handling required**: All columns are fully populated
- **Grain understanding**: One row = one sub-role within one company (not individual employees)
- **Completeness**: Companies without employees in a sub-role will have no row (not a zero count)
- **Size outliers**: The maximum of 302,516 suggests potential for very large companies; consider percentile-based filtering for typical analyses
- **Role taxonomy**: The 106 sub-roles provide granular detail but may need grouping for high-level analysis
- **Snapshot nature**: Appears to be point-in-time data (no temporal dimension visible)

## Keywords

employee distribution, workforce composition, job roles, sub-roles, company workforce, organizational structure, headcount by role, employee count, job functions, people analytics, workforce analytics, talent distribution, company staffing, role taxonomy, organizational roles, business functions, departmental headcount, company_id, people data, labor distribution, staffing levels, workforce segmentation

## Table and Column Docs

**Table Comment**: Not provided

**Column Comments**: 
- company_id: Not provided
- sub_role: Not provided  
- employee_count: Not provided