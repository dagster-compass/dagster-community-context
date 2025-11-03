---
columns:
- company_id (STRING)
- country (STRING)
- employee_count (INT64)
schema_hash: 84b585c7c99900f31105ce68bb168b946b200165fe6977c111e050edd4528030

---
# Table Summary: people_labs_data.companies_employee_distribution_by_country

## Overall Dataset Characteristics

- **Total Rows**: 15,495,627
- **Data Quality**: Excellent - no null values detected in any column (0.00% null percentage across all fields)
- **Dataset Purpose**: This table tracks the geographic distribution of employees across companies, showing employee counts per company per country
- **Scale**: Contains data for 10+ million unique companies across 250 countries/territories
- **Notable Pattern**: High granularity with many companies having small employee counts (1-10 employees common), but range extends to large organizations with up to 248,710 employees

## Column Details

### country (STRING)
- **Type**: Text/categorical field
- **Data Quality**: Complete (0% nulls)
- **Cardinality**: 250 unique countries/territories
- **Format**: Lowercase, standardized country names (e.g., "united states", "czechia", "malawi")
- **Geographic Coverage**: Global dataset including territories like "american samoa" and "anguilla"
- **Common Values**: Based on samples, includes major economies (United States, Mexico, Bulgaria, Denmark, Czechia, Zimbabwe)
- **Note**: Uses modern naming conventions (e.g., "czechia" rather than "czech republic")

### employee_count (INT64)
- **Type**: Integer/numeric
- **Data Quality**: Complete (0% nulls), all positive values
- **Range**: 1 to 248,710 employees
- **Cardinality**: 5,964 unique values
- **Distribution Pattern**: Likely heavily right-skewed with many small companies (1-10 employees are listed in possible values)
- **Use Case**: Quantifies workforce size per company per country

### company_id (STRING)
- **Type**: Text/identifier field
- **Data Quality**: Complete (0% nulls)
- **Cardinality**: 10,075,624 unique companies
- **Format**: Alphanumeric hash/encoded identifiers (28 characters, mixed case)
- **Examples**: "qL2MlZpEtWgqnZh47trHEQgGX7O9", "5HhC3EnY6N9CNsCVTrySIQeIwaYD"
- **Note**: Acts as primary key for company entities; suggests companies can have multiple rows (one per country where they have employees)

## Potential Query Considerations

### Filtering Opportunities
- **country**: Excellent for geographic filtering (e.g., WHERE country = 'united states')
- **employee_count**: Good for size-based filtering (e.g., WHERE employee_count > 100 for large offices)
- **company_id**: Essential for company-specific lookups or joining to other company tables

### Grouping/Aggregation Use Cases
- **By country**: Aggregate total employees or count companies per country
- **By company_id**: Sum employees across all countries to get total company size
- **By employee_count ranges**: Distribution analysis (small/medium/large office sizes)
- **Combined**: Company count by country and size tier

### Join Considerations
- **company_id**: Primary join key to connect with other company dimension tables (likely company details, industry, founding date, etc.)
- **country**: Could join with geographic reference tables for regional groupings or economic indicators

### Data Quality Considerations for Queries
- **Multiple rows per company**: Companies appear multiple times if they have employees in multiple countries (one row per country)
- **Country name standardization**: Use lowercase country names in WHERE clauses
- **Aggregation requirement**: To get total company employee count, must SUM(employee_count) GROUP BY company_id
- **Large dataset**: 15M+ rows require efficient indexing; use appropriate WHERE clauses to limit result sets
- **No temporal dimension**: This appears to be a snapshot without date/time fields

## Keywords

global workforce, employee distribution, company size, geographic distribution, international presence, headcount by country, multinational companies, office locations, employee count, company employees, workforce geography, country-level data, company footprint, global employees, staffing levels, international workforce, people analytics, human capital, organizational size, geographic footprint

## Table and Column Documentation

**Table Comment**: Not provided

**Column Comments**: Not provided

---

**Analysis Notes**: This is a fact table showing the geographic distribution of employees across companies. The grain is one row per company per country combination. To analyze total company size, queries must aggregate across countries. The absence of temporal fields suggests this is a current snapshot rather than historical tracking.