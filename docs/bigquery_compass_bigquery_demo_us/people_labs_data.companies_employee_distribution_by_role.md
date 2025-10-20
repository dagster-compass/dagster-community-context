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
- **Data Quality**: Excellent - no null values across all columns (0.00% null rate)
- **Structure**: This appears to be a fact table containing employee distribution data across different roles within companies
- **Scale**: Large dataset with over 10 million unique companies and comprehensive role coverage
- **Distribution Pattern**: The data shows a wide range of employee counts (1 to 303,046), suggesting coverage of companies from small startups to large enterprises

## Column Details

### role (STRING)
- **Data Type**: String/categorical
- **Completeness**: 100% populated (0% nulls)
- **Cardinality**: 24 distinct role categories
- **Key Values**: advisory, analyst, creative, education, engineering, finance, fulfillment, health, hospitality, human_resources, other_uncategorized
- **Usage Pattern**: Categorical dimension for role-based analysis
- **Note**: "other_uncategorized" appears frequently in samples, suggesting this is a catch-all category

### employee_count (INT64)
- **Data Type**: Integer
- **Completeness**: 100% populated (0% nulls)
- **Range**: 1 to 303,046 employees
- **Cardinality**: 5,454 unique values
- **Distribution**: Heavily skewed toward smaller counts (samples show many 1-employee entries)
- **Usage Pattern**: Quantitative measure for aggregations and size-based filtering

### company_id (STRING)
- **Data Type**: String identifier
- **Completeness**: 100% populated (0% nulls)
- **Cardinality**: 10,078,178 unique companies
- **Format**: Alphanumeric hash-like identifiers (e.g., "1tWCcdHnvHnM72CcGBZaAg1LO9zR")
- **Usage Pattern**: Primary key for company identification and joining

## Potential Query Considerations

### Filtering Opportunities
- **role**: Excellent for filtering by specific job functions or role categories
- **employee_count**: Good for size-based filtering (e.g., companies with >100 employees in engineering)
- **company_id**: Useful for company-specific analysis

### Grouping/Aggregation Potential
- **role**: Primary dimension for role-based analytics and comparisons
- **employee_count**: Can be aggregated (SUM, AVG, MAX) to understand company sizes and role distributions
- **company_id**: Can group to get total employees per company across all roles

### Join Considerations
- **company_id**: Primary key for joining with other company-related tables
- This appears to be a normalized fact table that would benefit from dimension tables with company metadata

### Data Quality Considerations
- **Completeness**: Excellent data quality with no missing values
- **Granularity**: One row per company-role combination
- **Potential Duplicates**: Should verify no duplicate company_id + role combinations exist
- **Scale Considerations**: Large dataset may require partitioning strategies for optimal query performance
- **Role Standardization**: The "other_uncategorized" category suggests some roles may not be properly classified

## Keywords

employee distribution, company roles, workforce analytics, organizational structure, role-based analysis, company size, employee count, job functions, human resources data, organizational charts, staff distribution, company demographics, workforce composition, role categories, people analytics

## Table and Column Documentation

**Table Comment**: Not provided

**Column Comments**: 
- role: Not provided
- employee_count: Not provided  
- company_id: Not provided