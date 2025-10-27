---
columns:
- company_id (STRING)
- employee_count (INT64)
- role (STRING)
schema_hash: 51368c4f020428e9d698aaf80c8cd3744fb72c34ed4d1d8ed34fc89cbe090029

---
# Table Summary: people_labs_data.companies_employee_distribution_by_role

## Overall Dataset Characteristics

- **Total Rows**: 22,588,172 records
- **Data Quality**: Excellent - no null values detected in any column
- **Dataset Nature**: This appears to be a comprehensive employee distribution dataset showing how employees are distributed across different roles within companies
- **Coverage**: Contains data for over 10 million unique companies with 24 distinct role categories
- **Distribution Pattern**: The data shows a wide range of company sizes, from single-employee companies to large enterprises with over 300,000 employees

## Column Details

### role (STRING)
- **Data Type**: String, categorical data
- **Completeness**: 100% (0% null values)
- **Cardinality**: 24 unique role categories
- **Value Distribution**: Includes standard business functions such as:
  - Core business roles: engineering, finance, marketing, sales
  - Support functions: human_resources, legal, operations
  - Specialized roles: creative, education, health, hospitality
  - Service roles: fulfillment, public_service, partnerships
  - Catch-all: other_uncategorized
- **Data Quality**: Well-structured categorical data with consistent naming conventions

### employee_count (INT64)
- **Data Type**: Integer, numeric count data
- **Completeness**: 100% (0% null values)
- **Range**: 1 to 303,046 employees per role per company
- **Cardinality**: 5,454 unique values
- **Distribution**: Heavily skewed toward smaller counts (many companies have 1-10 employees per role)
- **Business Context**: Represents the number of employees in each specific role within each company

### company_id (STRING)
- **Data Type**: String, appears to be encoded identifier
- **Completeness**: 100% (0% null values)
- **Cardinality**: 10,078,178 unique companies
- **Format**: Alphanumeric strings (e.g., "ZnMFKUZ3DjdxUJt8RtYZ6we2965q")
- **Primary Key Candidate**: Serves as the company identifier for joining with other company-related tables

## Potential Query Considerations

### Filtering Opportunities
- **role**: Excellent for filtering by specific job functions or business areas
- **employee_count**: Good for filtering by company size ranges or role-specific headcount thresholds
- **company_id**: Essential for company-specific analysis

### Grouping/Aggregation Potential
- **role**: Primary grouping dimension for analyzing workforce composition across industries
- **company_id**: For company-level aggregations and analysis
- **employee_count**: Can be binned for size-based analysis (small/medium/large companies)

### Join Considerations
- **company_id**: Primary join key for connecting with other company-related tables
- High cardinality suggests this is likely a fact table that would join with company dimension tables

### Data Quality Considerations
- **Completeness**: Excellent data quality with no missing values
- **Consistency**: Role categories appear standardized and consistent
- **Scale**: Large dataset may require performance considerations for complex queries
- **Granularity**: Data is at company-role level, allowing for detailed workforce analysis

## Keywords

employee distribution, workforce composition, company roles, organizational structure, headcount analysis, business functions, company staffing, role-based analysis, enterprise data, people analytics, HR analytics, company size analysis, workforce planning

## Table and Column Documentation

No table comments or column comments were provided in the analysis report.