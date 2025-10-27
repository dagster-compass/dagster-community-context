---
columns:
- company_id (STRING)
- event_date (STRING)
- job_title (STRING)
- job_title_class (STRING)
- job_title_role (STRING)
- job_title_sub_role (STRING)
- other_company_id (STRING)
- other_company_job_title (STRING)
- other_company_job_title_class (STRING)
- other_company_job_title_role (STRING)
- other_company_job_title_sub_role (STRING)
- person_id (STRING)
- record_type (STRING)
schema_hash: b9dbf0184a2fdfd7c008fc452bdb7ceb7d815fce9ed2dc32ca634a0d07e1f9c6

---
# Table Analysis Summary: people_labs_data.companies_talent_flow_details

## Overall Dataset Characteristics

- **Total Rows**: 211,892 records
- **Data Quality**: Good overall quality with no null values in key identifier columns
- **Time Period**: Limited to 5 months in 2025 (May, June, July, August, November)
- **Primary Purpose**: Tracks employee movement (hires and departures) between companies with detailed job role classifications

## Column Details

### Temporal Dimension
- **event_date** (STRING): Monthly granularity with 5 unique values (2025-05 through 2025-11), no nulls
  - Format: YYYY-MM
  - Complete coverage for tracking talent flow events

### Entity Identifiers
- **person_id** (STRING): 179,589 unique individuals, no nulls
  - Format appears to be encoded identifiers ending in "_0000"
- **company_id** (STRING): 113,007 unique companies, no nulls
  - Format: Base64-like encoded strings
- **other_company_id** (STRING): 75,125 unique companies, 39.86% null
  - Represents the destination company for departures or source company for hires

### Event Classification
- **record_type** (STRING): Binary classification, no nulls
  - Values: "departure", "hire"
  - Core dimension for analyzing talent flow direction

### Job Title Information
- **job_title** (STRING): 78,750 unique raw job titles, no nulls
  - Highly granular, unstructured job titles
- **job_title_role** (STRING): 23 standardized roles, 21.86% null
  - Categories include: marketing, engineering, finance, operations, etc.
- **job_title_sub_role** (STRING): 103 sub-categories, 40.13% null
  - More specific role classifications (executive, retail, investment_banking, etc.)
- **job_title_class** (STRING): 4 high-level categories, 21.86% null
  - Values: general_and_administrative, research_and_development, sales_and_marketing, services

### Other Company Job Information
- **other_company_job_title** (STRING): 69,232 unique titles, 39.86% null
- **other_company_job_title_role** (STRING): 23 categories, 53.80% null
- **other_company_job_title_sub_role** (STRING): 105 categories, 64.73% null
- **other_company_job_title_class** (STRING): 4 categories, 87.16% null

## Data Quality Observations

- **High Null Rates**: Other company job information has significant null percentages (40-87%), indicating many records lack destination/source job details
- **Hierarchical Job Classification**: Job roles are organized in a 3-tier hierarchy (class > role > sub_role)
- **Consistent Identifiers**: All core identifiers (person_id, company_id, event_date) are complete

## Query Considerations

### Good for Filtering
- **event_date**: Time-based analysis (monthly trends)
- **record_type**: Separate hire vs. departure analysis
- **job_title_role/class**: Role-based filtering with manageable cardinality
- **company_id**: Company-specific analysis

### Good for Grouping/Aggregation
- **event_date**: Monthly talent flow trends
- **record_type**: Hire/departure ratios
- **job_title_class/role**: Role-based aggregations
- **company_id**: Company-level metrics

### Potential Relationships
- **company_id** ↔ **other_company_id**: Talent flow between companies
- **person_id**: Individual career progression tracking
- Job title hierarchy relationships for role analysis

### Data Quality Considerations
- Handle high null rates in "other_company" fields appropriately
- Consider using COALESCE or IS NOT NULL filters for complete records
- Be aware that job title classifications may not be available for all records
- Time series analysis limited to 5-month window in 2025

## Keywords

talent flow, employee movement, hiring, departures, job roles, company talent analytics, workforce mobility, career transitions, job classifications, people analytics, HR data, recruitment data, employee turnover, talent acquisition, workforce planning

## Table and Column Documentation

No table comment or column comments were provided in the analysis report.