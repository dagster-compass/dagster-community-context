---
columns:
- company_id (STRING)
- country (STRING)
- employee_count (INT64)
schema_hash: 84b585c7c99900f31105ce68bb168b946b200165fe6977c111e050edd4528030

---
# Table Summary: people_labs_data.companies_employee_distribution_by_country

## Overall Dataset Characteristics

- **Total Rows**: 15,495,627 records
- **Data Quality**: Excellent - 0% null values across all columns
- **Purpose**: This table provides a geographic breakdown of employee distribution across companies, showing how many employees each company has in different countries
- **Granularity**: One row per company-country combination
- **Coverage**: Global dataset spanning 250 countries/territories
- **Company Coverage**: 10,075,624 unique companies represented

### Notable Patterns
- High cardinality in company IDs (10M+ unique companies)
- Moderate cardinality in countries (250 locations)
- Wide range in employee counts (1 to 248,710 employees per company-country)
- Most companies likely have small employee counts based on sample data showing many single-employee entries
- Company IDs use an alphanumeric hash format (consistent 28-character strings)

## Column Details

### country (STRING)
- **Data Type**: STRING (lowercase format)
- **Null Values**: 0% - Complete coverage
- **Unique Values**: 250 distinct countries/territories
- **Format**: Lowercase, full country names (e.g., "united states", "south africa", "united kingdom")
- **Examples**: afghanistan, albania, algeria, american samoa, andorra, angola, argentina, canada
- **Common Values**: united states, canada, united kingdom, algeria, south africa (based on samples)
- **Notes**: Includes territories like "american samoa" and "anguilla"; standardized naming convention

### employee_count (INT64)
- **Data Type**: Integer
- **Null Values**: 0% - Complete coverage
- **Unique Values**: 5,964 distinct counts
- **Range**: 1 to 248,710 employees
- **Distribution**: Heavily right-skewed (many small companies, few very large ones)
- **Common Values**: 1 employee appears frequently in samples, suggesting many single-person offices or small presences
- **Notable**: Maximum of 248,710 suggests presence of very large multinational corporations

### company_id (STRING)
- **Data Type**: STRING (alphanumeric identifier)
- **Null Values**: 0% - Complete coverage
- **Unique Values**: 10,075,624 distinct companies
- **Format**: 28-character alphanumeric hash (e.g., "cwtgOp76OCxLBVhLssA5dwTQOAVC")
- **Purpose**: Unique identifier for each company; likely serves as primary key in a related companies table
- **Notes**: No apparent pattern in the ID structure; appears to be a randomly generated unique identifier

## Table and Column Docs

*No table comment or column comments were provided in the source data.*

## Potential Query Considerations

### Good for Filtering
- **country**: Excellent for geographic filtering (e.g., WHERE country = 'united states')
- **employee_count**: Useful for size-based filtering (e.g., WHERE employee_count > 100)
- **company_id**: Essential for company-specific lookups

### Good for Grouping/Aggregation
- **country**: Ideal for geographic aggregations (total employees by country, company count by country)
- **employee_count**: Can be bucketed for size distribution analysis (small/medium/large companies)
- Combined grouping possible for multi-dimensional analysis

### Potential Join Keys
- **company_id**: Primary join key to connect with other company-related tables (company details, financials, etc.)
- This table likely represents a child/detail table in a company data model

### Data Quality Considerations
1. **Multiple Rows Per Company**: A single company can appear multiple times (once per country where they have employees)
2. **Aggregation Needs**: To get total company headcount, must SUM employee_count GROUP BY company_id
3. **Country Standardization**: Countries are in lowercase with full names; queries should match this format
4. **No Nulls**: All joins and filters can assume complete data
5. **Large Dataset**: 15M+ rows - queries should use appropriate indexes and filtering strategies
6. **Employee Count Accuracy**: Numbers represent employees per country, not total company size

### Recommended Query Patterns
- Geographic analysis: GROUP BY country
- Company size segmentation: CASE statements on employee_count ranges
- Multi-national companies: Companies with COUNT(DISTINCT country) > 1
- Employee concentration: SUM(employee_count) by various dimensions
- Top employers by region: ORDER BY employee_count DESC with country filter

## Keywords

`companies`, `employees`, `employee count`, `geographic distribution`, `country`, `international presence`, `workforce`, `headcount`, `company size`, `multinational`, `employee distribution`, `people analytics`, `company analytics`, `workforce analytics`, `global workforce`, `company footprint`, `office locations`, `regional presence`, `people labs`, `company data`, `employee data`, `business intelligence`, `workforce planning`