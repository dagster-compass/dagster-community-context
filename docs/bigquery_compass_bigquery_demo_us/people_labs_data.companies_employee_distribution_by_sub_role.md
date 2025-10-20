---
columns:
- company_id (STRING)
- employee_count (INT64)
- sub_role (STRING)
schema_hash: c6987d74945b29e0ce9bfcf62f9e4d90258cb4b9064c7d6a108bb0bbbcffca93

---
# Table Analysis Summary: people_labs_data.companies_employee_distribution_by_sub_role

## Overall Dataset Characteristics

- **Total Rows**: 24,315,326 records
- **Data Quality**: Excellent - 0% null values across all columns
- **Dataset Purpose**: This table tracks employee count distribution across different sub-roles within companies
- **Scale**: Covers over 10 million unique companies with 106 distinct sub-role categories
- **Distribution Pattern**: The data shows a wide range of company sizes, from single employees to large corporations with over 300k employees in specific roles

## Column Details

### sub_role (STRING)
- **Data Type**: String/Text
- **Completeness**: 100% (0% null values)
- **Cardinality**: 106 unique values
- **Value Pattern**: Standardized role categories using lowercase with underscores
- **Common Categories**: Includes diverse roles from `academic`, `account_executive`, `administrative` to specialized roles like `wellness`, `product_management`, `artist`
- **Purpose**: Categorical classification of employee roles within organizations

### employee_count (INT64)
- **Data Type**: 64-bit Integer
- **Completeness**: 100% (0% null values)
- **Range**: 1 to 302,516 employees
- **Cardinality**: 5,390 unique values
- **Distribution**: Likely right-skewed with most companies having smaller employee counts in specific roles
- **Purpose**: Quantifies the number of employees in each sub-role per company

### company_id (STRING)
- **Data Type**: String identifier
- **Completeness**: 100% (0% null values)
- **Cardinality**: 10,078,178 unique values
- **Format**: Alphanumeric strings (appears to be encoded/hashed identifiers)
- **Purpose**: Unique identifier for each company in the dataset

## Query Considerations

### Filtering Opportunities
- **sub_role**: Excellent for filtering by specific job functions or role categories
- **employee_count**: Good for size-based filtering (small, medium, large teams in specific roles)
- **company_id**: Suitable for company-specific analysis

### Grouping/Aggregation Potential
- **sub_role**: Primary dimension for role-based analysis and comparisons
- **employee_count ranges**: Can be binned for company size analysis by role
- **company_id**: Useful for company-level aggregations

### Join Relationships
- **company_id**: Likely foreign key that can join with other company-related tables
- Potential relationships with company metadata, industry classifications, or geographic data

### Data Quality Considerations
- **High Quality**: No missing data concerns
- **Consistency**: Standardized role naming convention
- **Scalability**: Large dataset requiring efficient indexing on frequently queried columns
- **Aggregation Performance**: Consider pre-computing common aggregations due to dataset size

## Keywords

employee distribution, company roles, workforce analytics, sub roles, organizational structure, employee count, company analysis, job functions, role categorization, workforce composition, people analytics, HR data, employment statistics, company sizing, role-based metrics

## Table and Column Documentation

**Table Comment**: Not provided

**Column Comments**: 
- sub_role: No comment provided
- employee_count: No comment provided  
- company_id: No comment provided