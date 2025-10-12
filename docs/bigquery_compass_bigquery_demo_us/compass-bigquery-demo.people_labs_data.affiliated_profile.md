---
columns:
- company_id (STRING)
- profile (STRING)
schema_hash: 857d0bb74f09d1acc161b931b7d48780f1ae26ac59c0cb15d6f4c2e87c996412

---
# Table Analysis Summary: compass-bigquery-demo.people_labs_data.affiliated_profile

## Overall Dataset Characteristics

- **Total Rows**: 103,856 records
- **Data Quality**: Excellent - no null values detected in any column
- **Structure**: Simple two-column association table linking profiles to companies
- **Distribution Pattern**: Many-to-many relationship structure with 78,684 unique profiles associated with 71,488 unique companies
- **Notable Observations**: 
  - Some profiles appear to be affiliated with multiple companies (78,684 profiles vs 103,856 total rows)
  - Some companies have multiple affiliated profiles
  - All identifiers follow a consistent alphanumeric format (28 characters)

## Column Details

### profile (STRING)
- **Data Type**: STRING with consistent 28-character alphanumeric format
- **Null Values**: 0.00% (complete coverage)
- **Uniqueness**: 78,684 unique values out of 103,856 rows (~75.8% unique)
- **Pattern**: Consistent alphanumeric identifier format (e.g., "WBjBaEnRbM0CjMsPfgisCgLbP485")
- **Distribution**: Multiple profiles can appear more than once, indicating one profile can be affiliated with multiple companies

### company_id (STRING)
- **Data Type**: STRING with consistent 28-character alphanumeric format
- **Null Values**: 0.00% (complete coverage)
- **Uniqueness**: 71,488 unique values out of 103,856 rows (~68.8% unique)
- **Pattern**: Consistent alphanumeric identifier format (e.g., "FUVVLspTvCjVYiICKgGJiwU75tf6")
- **Distribution**: Multiple company_ids can appear more than once, indicating companies can have multiple affiliated profiles

## Potential Query Considerations

### Filtering Options
- **By Profile**: Direct profile lookups using exact string matching
- **By Company**: Direct company_id lookups using exact string matching
- Both columns are ideal for WHERE clause filtering due to consistent format and no nulls

### Grouping/Aggregation Opportunities
- **Profile-based aggregation**: Count companies per profile to identify multi-company affiliations
- **Company-based aggregation**: Count profiles per company to identify company sizes or network reach
- **Relationship analysis**: Analyze the many-to-many relationship patterns

### Join Key Potential
- **profile**: Likely joins to other profile-related tables in the people_labs_data dataset
- **company_id**: Likely joins to company information tables
- Both columns appear to be foreign keys to other entities in the broader dataset

### Data Quality Considerations
- **High reliability**: No null values make this table very reliable for joins and analysis
- **Consistent formatting**: All identifiers follow the same 28-character alphanumeric pattern
- **Complete relationships**: Every profile has a company affiliation, and every company has at least one profile
- **Duplicate handling**: Queries should account for the many-to-many nature when doing counts or aggregations

## Keywords

affiliation, profile, company, relationship, association, many-to-many, people_labs, compass, bigquery, identifiers, foreign_keys, joins, aggregation, network_analysis

## Table and Column Documentation

**Table Comment**: Not provided

**Column Comments**: 
- profile: Not provided
- company_id: Not provided