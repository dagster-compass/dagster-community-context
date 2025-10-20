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
- **Data Quality**: Excellent - 0% null values across all columns
- **Dataset Purpose**: This appears to be a comprehensive mapping of companies to countries with their respective employee counts, likely representing the distribution of company workforces across different geographical locations
- **Scale**: Large-scale dataset with over 10 million unique companies across 250 countries
- **Data Completeness**: 100% complete with no missing values

## Column Details

### country (STRING)
- **Data Type**: String, standardized lowercase format
- **Null Values**: 0% (complete data)
- **Distribution**: 250 unique countries represented
- **Format Pattern**: Lowercase, full country names (e.g., "united states", "united kingdom")
- **Notable Values**: Includes major economies like India, Netherlands, United States, as well as smaller territories like American Samoa, Anguilla
- **Geographic Coverage**: Global dataset including countries, territories, and dependencies

### employee_count (INT64)
- **Data Type**: Integer
- **Null Values**: 0% (complete data)
- **Range**: 1 to 248,710 employees
- **Distribution**: 5,964 unique employee count values
- **Patterns**: 
  - Heavily skewed toward smaller companies (many companies with 1 employee)
  - Large range suggests presence of both small startups and major corporations
  - Maximum of 248,710 suggests very large multinational companies

### company_id (STRING)
- **Data Type**: String identifier
- **Null Values**: 0% (complete data)
- **Uniqueness**: 10,075,624 unique company IDs
- **Format**: Alphanumeric strings (appears to be encoded/hashed identifiers)
- **Pattern**: Consistent length format, likely system-generated
- **Key Characteristic**: Primary identifier for companies in the dataset

## Potential Query Considerations

### Filtering Opportunities
- **country**: Excellent for geographical analysis and filtering by specific regions or countries
- **employee_count**: Good for size-based company segmentation (small/medium/large enterprises)
- **company_id**: Perfect for individual company lookups

### Grouping/Aggregation Potential
- **country**: Primary grouping dimension for geographical analysis
- **employee_count ranges**: Can be binned for company size analysis
- **Aggregate functions**: SUM(employee_count) by country, COUNT(*) for company counts per country

### Join Key Potential
- **company_id**: Primary key for joining with other company-related tables
- **country**: Can be joined with geographical/economic data tables

### Data Quality Considerations
- **No null handling required**: All columns are complete
- **Case sensitivity**: Country names are in lowercase, may need standardization when joining with other datasets
- **Employee count validation**: Consider filtering out unrealistic values if needed (though range appears reasonable)
- **Country name standardization**: May need mapping if joining with datasets using different country naming conventions

## Query Performance Considerations
- **Large dataset**: 15M+ rows require efficient indexing strategies
- **Country filtering**: Likely benefits from indexing on country column
- **Company lookups**: company_id should be indexed for individual company queries
- **Aggregation queries**: Consider partitioning by country for large analytical queries

## Keywords
employee distribution, company workforce, geographical analysis, business intelligence, company size, international business, workforce analytics, company demographics, global companies, employee count by country, business presence, multinational corporations, startup analysis, SME analysis, geographic distribution

## Table and Column Documentation
*No table comment or column comments were provided in the source data.*