---
columns:
- company_id (STRING)
- employee_count (INT64)
- job_class (STRING)
schema_hash: 4ec24a365c9a3456a129cb767dfa91c019b0ce2f0616e25f58b04bc0bf5e7f13

---
# Data Summary: people_labs_data.companies_employee_distribution_by_class

## Overall Dataset Characteristics

- **Total Rows**: 17,813,054
- **Data Quality**: Excellent - no null values detected across all columns
- **Dataset Purpose**: This table captures employee distribution across different job classifications for companies
- **Key Pattern**: Each row represents a specific company's employee count within a particular job class category
- **Scale**: Covers over 10 million unique companies with employee counts ranging from small (1 employee) to very large organizations (306,179 employees)

## Column Details

### job_class (STRING)
- **Data Type**: String/categorical
- **Null Values**: 0.00% (perfect data quality)
- **Categories**: 5 distinct job classifications
  - `general_and_administrative`
  - `other_uncategorized` 
  - `research_and_development`
  - `sales_and_marketing`
  - `services`
- **Usage**: Primary dimension for analyzing workforce composition by functional area

### employee_count (INT64)
- **Data Type**: Integer
- **Null Values**: 0.00% (perfect data quality)
- **Range**: 1 to 306,179 employees
- **Distribution**: 5,880 unique values indicating wide variety in company sizes
- **Pattern**: Likely right-skewed distribution with many small companies (1-10 employees) and fewer large enterprises
- **Usage**: Quantitative measure for aggregations and size-based analysis

### company_id (STRING)
- **Data Type**: String identifier
- **Null Values**: 0.00% (perfect data quality)
- **Uniqueness**: 10,078,178 unique companies
- **Format**: Alphanumeric strings (appears to be base64-like encoding)
- **Usage**: Primary key for company identification and potential joins

## Potential Query Considerations

### Filtering Opportunities
- **job_class**: Excellent for filtering by specific workforce categories
- **employee_count**: Good for size-based filtering (small/medium/large companies)
- **company_id**: For specific company lookups

### Grouping/Aggregation Potential
- **Primary Grouping**: `job_class` for workforce composition analysis
- **Secondary Grouping**: Employee count ranges (e.g., 1-10, 11-50, 51-200, 200+)
- **Aggregations**: SUM(employee_count) for total workforce, COUNT(*) for company counts, AVG(employee_count) for size metrics

### Join Considerations
- **company_id**: Likely foreign key for joining with other company-related tables
- **Potential Relationships**: Company details, industry classifications, geographic data, financial metrics

### Data Quality Considerations
- **Strengths**: No missing data, consistent formatting
- **Query Reliability**: High - all aggregations and calculations will be accurate
- **Performance**: Large dataset (17M+ rows) may require indexed queries for optimal performance

## Keywords

company workforce, employee distribution, job classification, organizational structure, company size analysis, workforce composition, employee count, business functions, company analytics, HR data, organizational analysis, company demographics

## Table and Column Documentation

**Table Comment**: Not provided

**Column Comments**: Not provided