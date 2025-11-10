---
columns:
- company_id (STRING)
- country (STRING)
- employee_count (INT64)
schema_hash: 84b585c7c99900f31105ce68bb168b946b200165fe6977c111e050edd4528030

---
# Table Summary: people_labs_data.companies_employee_distribution_by_country

## Overall Dataset Characteristics

### Scale and Structure
- **Total Rows**: 15,495,627 (approximately 15.5 million records)
- **Data Quality**: Excellent - 0% null values across all columns
- **Granularity**: Each row represents the employee count for a specific company in a specific country
- **Coverage**: Global dataset with 250 countries represented and over 10 million unique companies

### Notable Patterns
- The dataset appears to track employee distribution across different geographic locations for companies
- Many companies appear multiple times (10M unique companies across 15.5M rows), suggesting multinational operations
- Employee counts range dramatically from 1 to 248,710 employees per country per company
- High concentration in major economies (United States and Germany appear frequently in samples)

## Column Details

### country (STRING)
- **Data Type**: String, lowercase format
- **Completeness**: 100% populated (0% null)
- **Cardinality**: 250 unique countries
- **Format Pattern**: Lowercase, full country names (e.g., "united states", "germany", "tunisia")
- **Common Values**: Based on samples: "united states", "germany", "mexico", "tunisia"
- **Geographic Coverage**: Comprehensive global coverage including territories (e.g., "american samoa", "anguilla")
- **Query Consideration**: Primary dimension for geographic analysis and filtering

### employee_count (INT64)
- **Data Type**: Integer (64-bit)
- **Completeness**: 100% populated (0% null)
- **Cardinality**: 5,964 unique values
- **Range**: 1 to 248,710 employees
- **Distribution**: Likely right-skewed (many small counts, few very large ones)
- **Granularity**: Precise employee counts per company-country combination
- **Query Consideration**: Key metric for aggregation (SUM, AVG, MAX) and filtering by company size

### company_id (STRING)
- **Data Type**: String (appears to be alphanumeric hash/identifier)
- **Completeness**: 100% populated (0% null)
- **Cardinality**: 10,075,624 unique companies
- **Format Pattern**: 28-character alphanumeric strings (e.g., "JuiDJFFFE5QxGUKxxyKthQJNcBN7")
- **Uniqueness**: Non-unique in this table (companies appear multiple times for different countries)
- **Query Consideration**: Primary key for joining to company master tables; grouping key for company-level aggregations

## Potential Query Considerations

### Filtering Strategies
- **Geographic filtering**: Use `country` column for regional analysis (exact match required due to lowercase format)
- **Size-based filtering**: Use `employee_count` with numeric operators (>, <, BETWEEN) to segment by company size
- **Company-specific queries**: Filter by `company_id` for individual company analysis

### Aggregation Opportunities
- **Total employees by country**: `SUM(employee_count) GROUP BY country`
- **Total employees per company globally**: `SUM(employee_count) GROUP BY company_id`
- **Average company size by country**: `AVG(employee_count) GROUP BY country`
- **Company presence (country count)**: `COUNT(DISTINCT country) GROUP BY company_id`
- **Market concentration**: Count of companies by country

### Join Key Potential
- **company_id**: Primary join key to connect with other company-related tables (company profiles, financials, industries, etc.)
- **country**: Potential join to country reference tables (GDP, population, regional groupings)

### Data Quality Considerations
- **No null handling required**: All columns are fully populated
- **Case sensitivity**: Country names are lowercase; queries should use lowercase or LOWER() function
- **Duplicate awareness**: Companies appear multiple times (one row per country presence); use appropriate GROUP BY for company-level metrics
- **Scale considerations**: 15.5M rows requires indexing on frequently filtered columns for performance
- **Employee count accuracy**: Represents snapshot in time; may need date context from related tables

## Keywords

multinational companies, employee distribution, geographic presence, company size, workforce by country, global employment, company locations, international business, employee headcount, country-level data, company footprint, labor distribution, organizational structure, company expansion, market presence, workforce analytics, global operations, company geography, employee counts by region, international workforce

## Table and Column Documentation

**Note**: No table comment or column comments were provided in the source analysis report.