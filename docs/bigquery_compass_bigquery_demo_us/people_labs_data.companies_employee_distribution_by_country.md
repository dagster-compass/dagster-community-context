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
- **Dataset Purpose**: This table tracks the distribution of employees by country for companies, representing a many-to-many relationship between companies and countries
- **Scale**: Large enterprise dataset with over 10 million unique companies across 250 countries
- **Distribution Pattern**: Each row represents a company's employee presence in a specific country, allowing companies to have multiple entries (one per country where they have employees)

## Column Details

### company_id (STRING)
- **Data Type**: String identifier
- **Completeness**: 100% populated (0% nulls)
- **Cardinality**: 10,075,624 unique companies
- **Format**: Alphanumeric hash-like identifiers (e.g., "ifPO1TY9q97ZKkBGf1LCOgcQ48bj")
- **Pattern**: Consistent 28-character string format
- **Usage**: Primary identifier for companies, serves as foreign key for joins

### country (STRING)
- **Data Type**: String
- **Completeness**: 100% populated (0% nulls)
- **Cardinality**: 250 unique countries
- **Format**: Lowercase country names with spaces and special characters
- **Common Patterns**: Includes full country names, territories, and dependencies
- **Notable Values**: "united states", "united kingdom", "netherlands", "germany", "france"
- **Geographic Coverage**: Global coverage including small territories and dependencies

### employee_count (INT64)
- **Data Type**: Integer
- **Completeness**: 100% populated (0% nulls)
- **Range**: 1 to 248,710 employees
- **Distribution**: Heavily skewed toward smaller counts (many companies with 1-10 employees per country)
- **Maximum**: 248,710 suggests very large multinational corporations
- **Pattern**: Positive integers only, no zero values

## Potential Query Considerations

### Filtering Opportunities
- **Country-based filtering**: Excellent for geographic analysis and regional queries
- **Employee count ranges**: Good for segmenting companies by size (small, medium, large)
- **Company-specific lookups**: Direct filtering by company_id for specific company analysis

### Grouping/Aggregation Potential
- **By country**: Aggregate employee counts, company counts per country
- **By company**: Sum total global employees, count countries of operation
- **By employee size bands**: Group companies into size categories
- **Geographic regions**: Can be enhanced by mapping countries to regions/continents

### Join Key Relationships
- **company_id**: Primary join key to other company-related tables
- **country**: Can join to country reference tables for additional geographic data
- **Potential relationships**: Company details, industry classifications, financial data

### Data Quality Considerations
- **Excellent data completeness**: No missing values to handle in queries
- **Case sensitivity**: Country names are lowercase, ensure consistent casing in joins
- **Aggregation accuracy**: Multiple rows per company require SUM() for total employee counts
- **Time dimension**: No date fields present - this appears to be point-in-time data

## Keywords

employee distribution, company employees, international presence, geographic distribution, multinational companies, workforce analytics, company size, country analysis, global companies, employee count, business intelligence, company demographics, international business, workforce segmentation

## Table and Column Documentation

**Table Comment**: Not provided

**Column Comments**: Not provided