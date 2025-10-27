---
columns:
- company_id (STRING)
- employee_count (INT64)
- job_class (STRING)
schema_hash: 4ec24a365c9a3456a129cb767dfa91c019b0ce2f0616e25f58b04bc0bf5e7f13

---
# Data Summary: people_labs_data.companies_employee_distribution_by_class

## Overall Dataset Characteristics

- **Total Rows**: 17,813,054 records
- **Data Quality**: Excellent - 0% null values across all columns
- **Dataset Purpose**: Employee distribution data across different job classes for companies
- **Scale**: Large-scale dataset covering over 10 million unique companies
- **Distribution Pattern**: Heavily skewed toward smaller employee counts (sample shows mostly count of 1)

## Column Details

### job_class (STRING)
- **Data Type**: Categorical string
- **Null Values**: None (0.00%)
- **Unique Values**: 5 distinct categories
- **Categories**: 
  - `general_and_administrative`
  - `other_uncategorized` 
  - `research_and_development`
  - `sales_and_marketing`
  - `services`
- **Usage**: Primary classification dimension for employee roles

### employee_count (INT64)
- **Data Type**: Integer
- **Null Values**: None (0.00%)
- **Range**: 1 to 306,179 employees
- **Unique Values**: 5,880 distinct counts
- **Distribution**: Highly right-skewed (sample data shows predominantly small counts)
- **Usage**: Quantitative measure of employees in each job class

### company_id (STRING)
- **Data Type**: Alphanumeric identifier
- **Null Values**: None (0.00%)
- **Unique Values**: 10,078,178 distinct companies
- **Format**: Base64-like encoded strings (28 characters)
- **Usage**: Primary key for company identification

## Potential Query Considerations

### Filtering Opportunities
- **job_class**: Excellent for filtering by specific employee categories
- **employee_count**: Good for size-based filtering (small/medium/large companies)
- **company_id**: Useful for specific company lookups

### Grouping/Aggregation Potential
- **job_class**: Primary dimension for aggregating employee distributions
- **employee_count ranges**: Can create company size categories (1-10, 11-50, 51-200, etc.)
- **company_id**: For company-level aggregations

### Analytical Capabilities
- **Employee distribution analysis**: Sum employee_count by job_class
- **Company size analysis**: Distribution of companies by total employees
- **Job class prevalence**: Count of companies with each job class
- **Cross-tabulation**: Company size vs job class distribution

### Data Quality Considerations
- **No missing data**: All queries can proceed without null handling
- **Large dataset**: Consider using LIMIT for exploratory queries
- **Skewed distribution**: Employee counts heavily weighted toward smaller numbers
- **Multiple records per company**: Companies appear multiple times (once per job class with employees)

## Keywords
employee distribution, job classification, company workforce, organizational structure, employee count, job classes, company size, workforce analytics, human resources data, employment statistics

## Table and Column Docs
No table comment or column comments were provided in the source data.