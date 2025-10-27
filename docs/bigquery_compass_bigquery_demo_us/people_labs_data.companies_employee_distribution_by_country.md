---
columns:
- company_id (STRING)
- country (STRING)
- employee_count (INT64)
schema_hash: 84b585c7c99900f31105ce68bb168b946b200165fe6977c111e050edd4528030

---
# Table Analysis Summary: people_labs_data.companies_employee_distribution_by_country

## Overall Dataset Characteristics

- **Total Rows**: 15,495,627 records
- **Data Quality**: Excellent - no null values in any column (0.00% null rate across all fields)
- **Dataset Purpose**: This table tracks employee distribution across different countries for companies, showing how many employees each company has in each specific country
- **Notable Patterns**: 
  - Wide geographic coverage with 250 different countries represented
  - Company employee counts range from very small (1 employee) to very large organizations (248,710 employees)
  - Over 10 million unique companies in the dataset
  - The data appears to be at a granular level, with one row per company-country combination

## Column Details

### country (STRING)
- **Data Type**: String/text field
- **Null Values**: None (0.00%)
- **Distribution**: 250 unique countries represented
- **Format**: Lowercase country names (e.g., "germany", "united kingdom", "peru")
- **Coverage**: Global dataset including major countries and territories like "american samoa", "anguilla"
- **Data Quality**: Standardized naming convention with consistent lowercase formatting

### employee_count (INT64)
- **Data Type**: Integer
- **Null Values**: None (0.00%)
- **Range**: 1 to 248,710 employees
- **Distribution**: 5,964 unique employee count values
- **Pattern**: Heavily skewed toward smaller companies (many with 1-10 employees based on sample)
- **Business Context**: Represents the number of employees a company has in a specific country

### company_id (STRING)
- **Data Type**: String identifier
- **Null Values**: None (0.00%)
- **Uniqueness**: 10,075,624 unique company identifiers
- **Format**: Alphanumeric hash-like identifiers (e.g., "9uJL4ANcj65Z3mIv4HvvDQ7KFjet")
- **Purpose**: Primary key for identifying companies across the dataset

## Potential Query Considerations

### Good for Filtering:
- **country**: Excellent for geographic analysis and regional filtering
- **employee_count**: Useful for company size segmentation (small, medium, large enterprises)
- **company_id**: Essential for company-specific analysis

### Good for Grouping/Aggregation:
- **country**: Perfect for geographic summaries and country-level analytics
- **employee_count ranges**: Can be binned for company size analysis
- **company_id**: For per-company aggregations across countries

### Potential Join Keys:
- **company_id**: Primary key for joining with other company-related tables
- **country**: Could join with geographic/demographic data tables

### Data Quality Considerations:
- **No missing data**: All queries can assume complete data coverage
- **Country standardization**: Country names are consistently lowercase and standardized
- **Scale considerations**: Large dataset (15M+ rows) may require optimization for performance
- **One-to-many relationship**: Companies can appear multiple times (once per country where they have employees)

## Keywords

employee distribution, company demographics, geographic analysis, workforce analytics, international companies, country-level data, employee counts, business intelligence, corporate presence, global workforce, company size analysis, geographic footprint

## Table and Column Documentation

No table comment or column comments were provided in the source data.