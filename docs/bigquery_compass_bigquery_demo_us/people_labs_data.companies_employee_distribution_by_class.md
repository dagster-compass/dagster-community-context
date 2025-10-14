---
columns:
- company_id (STRING)
- employee_count (INT64)
- job_class (STRING)
schema_hash: 4ec24a365c9a3456a129cb767dfa91c019b0ce2f0616e25f58b04bc0bf5e7f13

---
# Dataset Summary: people_labs_data.companies_employee_distribution_by_class

## Overall Dataset Characteristics

- **Total Rows**: 17,813,054
- **Data Quality**: Excellent - no null values in any column
- **Structure**: Employee distribution data by job classification across companies
- **Scale**: Large dataset covering over 10 million unique companies
- **Pattern**: Each row represents a company-job_class combination with employee count

## Column Details

### company_id (STRING)
- **Data Type**: String identifier
- **Completeness**: 100% populated (0% null)
- **Uniqueness**: 10,078,178 unique values (~57% of total rows)
- **Format**: Alphanumeric hash-like identifiers (28 characters)
- **Pattern**: Each company can appear multiple times with different job classes
- **Sample**: `hFlP2MxUpC5BcAWEdH3uzwfOMyz3`

### job_class (STRING)
- **Data Type**: Categorical string
- **Completeness**: 100% populated (0% null)
- **Categories**: 5 distinct job classifications
  - `general_and_administrative`
  - `other_uncategorized` 
  - `research_and_development`
  - `sales_and_marketing`
  - `services`
- **Usage**: Primary grouping dimension for employee distribution analysis

### employee_count (INT64)
- **Data Type**: Integer
- **Completeness**: 100% populated (0% null)
- **Range**: 1 to 306,179 employees
- **Distribution**: 5,880 unique values, heavily skewed toward lower counts
- **Pattern**: Represents number of employees in each job class per company

## Potential Query Considerations

### Filtering Opportunities
- **company_id**: Excellent for company-specific analysis
- **job_class**: Perfect for functional area analysis (5 clear categories)
- **employee_count**: Good for size-based filtering (small/medium/large companies)

### Grouping/Aggregation Potential
- **Primary grouping**: job_class for functional distribution analysis
- **Secondary grouping**: company_id for per-company summaries
- **Aggregation metrics**: SUM(employee_count) for total workforce, AVG(employee_count) for typical department sizes

### Relationship Considerations
- **Fact table structure**: This appears to be a fact table with company_id as potential foreign key
- **One-to-many**: Each company_id can have multiple job_class entries
- **Complete representation**: Not all companies necessarily have all 5 job classes

### Data Quality Considerations
- **No missing data**: All columns are fully populated
- **Referential integrity**: company_id values should be validated against master company table
- **Business logic**: Employee counts should be positive integers (current data shows minimum of 1)
- **Aggregation accuracy**: Total company workforce = SUM of all job_class employee_counts per company

## Keywords

employee distribution, workforce analysis, job classification, company staffing, organizational structure, headcount, functional roles, business intelligence, HR analytics, company size analysis, departmental distribution

## Table and Column Documentation

**Table Comment**: Not provided

**Column Comments**: Not provided