---
columns:
- company_id (STRING)
- profile (STRING)
schema_hash: 857d0bb74f09d1acc161b931b7d48780f1ae26ac59c0cb15d6f4c2e87c996412

---
# Table Analysis Summary: affiliated_profile

## Overall Dataset Characteristics

- **Total Rows**: 103,856 records
- **Data Quality**: Excellent - no null values detected in any column
- **Structure**: Simple two-column mapping table establishing relationships between profiles and companies
- **Distribution Pattern**: Many-to-many relationship structure with some profiles potentially affiliated with multiple companies
- **Data Format**: All values appear to be encoded identifiers using alphanumeric strings

## Column Details

### company_id (STRING)
- **Data Type**: String identifier
- **Null Values**: 0.00% (perfect data quality)
- **Unique Values**: 71,488 distinct companies
- **Format Pattern**: 28-character alphanumeric identifiers (e.g., "MH0TFBsZ07mmAOv6nqcdDQdc0eD7")
- **Distribution**: Multiple profiles can be associated with the same company (103,856 total rows vs 71,488 unique companies)

### profile (STRING)
- **Data Type**: String identifier  
- **Null Values**: 0.00% (perfect data quality)
- **Unique Values**: 78,684 distinct profiles
- **Format Pattern**: 28-character alphanumeric identifiers (e.g., "kUcwVqquZbq5yalqeVsBggLl2xja")
- **Distribution**: Some profiles may be affiliated with multiple companies (103,856 total rows vs 78,684 unique profiles)

## Potential Query Considerations

### Filtering Capabilities
- Both `company_id` and `profile` are excellent for exact match filtering
- No partial matching recommended due to encoded identifier format
- All records have complete data, so no null handling required

### Grouping and Aggregation Opportunities
- **By company_id**: Count affiliated profiles per company, identify companies with most/least profiles
- **By profile**: Count company affiliations per profile, identify multi-company profiles
- Cross-analysis to understand affiliation patterns and distributions

### Relationship Analysis
- **Primary use case**: Join table connecting company and profile entities
- **Many-to-many relationship**: Profiles can have multiple company affiliations and companies can have multiple affiliated profiles
- **Join key candidates**: Both columns serve as foreign keys to their respective dimension tables

### Data Quality Considerations
- **High reliability**: Zero null values ensure consistent join operations
- **Identifier format**: Consistent 28-character alphanumeric format suggests systematic ID generation
- **Completeness**: Full population of both columns eliminates need for null-safe operations

## Keywords

affiliation, company, profile, relationship, mapping, junction table, many-to-many, identifiers, people labs, compass bigquery, employee company relationship

## Table and Column Documentation

**Table Comment**: Not provided

**Column Comments**: Not provided