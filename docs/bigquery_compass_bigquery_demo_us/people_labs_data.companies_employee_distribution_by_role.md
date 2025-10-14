---
columns:
- company_id (STRING)
- employee_count (INT64)
- role (STRING)
schema_hash: 51368c4f020428e9d698aaf80c8cd3744fb72c34ed4d1d8ed34fc89cbe090029

---
# Dataset Summary: people_labs_data.companies_employee_distribution_by_role

## Overall Dataset Characteristics

- **Total Rows**: 22,588,172 records
- **Data Quality**: Excellent - no null values in any column (0.00% null rate across all fields)
- **Dataset Purpose**: Tracks employee distribution across different roles within companies
- **Data Completeness**: 100% complete with no missing data
- **Scale**: Large enterprise dataset covering over 10 million unique companies

## Column Analysis

### company_id (STRING)
- **Data Type**: String identifier
- **Null Values**: None (0.00%)
- **Uniqueness**: 10,078,178 unique companies
- **Format**: Alphanumeric hash-like identifiers (e.g., "TnfOs8XlySUV16C5R3jPqgb3x75P")
- **Pattern**: Consistent 28-character strings with mixed case letters and numbers
- **Purpose**: Primary identifier for companies in the dataset

### role (STRING)
- **Data Type**: Categorical string
- **Null Values**: None (0.00%)
- **Unique Values**: 24 distinct roles
- **Categories Include**: advisory, analyst, creative, education, engineering, finance, fulfillment, health, hospitality, human_resources, operations, partnerships, sales, other_uncategorized
- **Distribution**: Covers major business functions and departments
- **Data Quality**: Standardized role categories with consistent naming

### employee_count (INT64)
- **Data Type**: Integer
- **Null Values**: None (0.00%)
- **Range**: 1 to 303,046 employees per role
- **Unique Values**: 5,454 distinct counts
- **Distribution**: Heavily skewed toward smaller counts (many companies have 1-10 employees per role)
- **Scale**: Accommodates everything from small businesses to large enterprises

## Potential Query Considerations

### Excellent for Filtering:
- **role**: Perfect for filtering by specific job functions or departments
- **company_id**: Ideal for company-specific analysis
- **employee_count**: Good for size-based filtering (e.g., companies with >100 employees in engineering)

### Excellent for Grouping/Aggregation:
- **role**: Primary grouping dimension for role-based analysis
- **company_id**: For company-level aggregations
- **employee_count**: For statistical analysis (SUM, AVG, MAX, MIN)

### Join Considerations:
- **company_id**: Primary key for joining with other company-related tables
- High cardinality (10M+ unique companies) suggests this is a comprehensive company dataset

### Query Performance Considerations:
- Large dataset (22M+ rows) may require careful indexing strategies
- Role-based queries will be efficient due to low cardinality (24 values)
- Company-specific queries should perform well with proper indexing on company_id

## Common Analysis Patterns:
1. **Role Distribution Analysis**: Aggregate employee counts by role across all companies
2. **Company Size Analysis**: Analyze total employees per company across all roles
3. **Role Concentration**: Identify companies with heavy concentration in specific roles
4. **Comparative Analysis**: Compare role distributions between different company segments

## Keywords
company employees, workforce distribution, organizational structure, job roles, employee count, business functions, company analysis, workforce analytics, role distribution, organizational data, employee segmentation, company demographics, workforce composition

## Table and Column Documentation
*No table comment or column comments were provided in the source data.*