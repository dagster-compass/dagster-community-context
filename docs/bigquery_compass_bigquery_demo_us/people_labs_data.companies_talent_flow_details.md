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
- **Data Quality**: Generally good with no null values in key identifier columns
- **Core Purpose**: Tracks talent movement between companies, capturing both hiring and departure events
- **Time Period**: Limited to 5 months in 2025 (May through August, plus November)
- **Notable Patterns**: 
  - High diversity in job titles (78,750 unique values)
  - Significant null values in job classification fields (21-87% depending on column)
  - Approximately 60% of records have "other company" information populated

## Column Details

### Identifier Columns
- **person_id** (STRING): Unique person identifier with 179,589 unique values across 211,892 records, indicating some people have multiple job events. No null values. Format appears to be hash-based.
- **company_id** (STRING): Company identifier with 113,007 unique companies represented. No null values. Hash-based format similar to person_id.

### Event Information
- **event_date** (STRING): Month-level granularity in YYYY-MM format. Only 5 possible values: 2025-05, 2025-06, 2025-07, 2025-08, 2025-11. No null values.
- **record_type** (STRING): Binary classification of talent movement - "departure" or "hire". No null values. Critical for understanding direction of talent flow.

### Current Company Job Information
- **job_title** (STRING): Highly diverse with 78,750 unique values. No null values. Ranges from simple titles like "vice president" to complex descriptions.
- **job_title_role** (STRING): Categorized role type with 23 possible values (21.86% null). Includes categories like engineering, finance, operations, etc.
- **job_title_sub_role** (STRING): More granular role classification with 103 values (40.13% null). Examples include executive, product_management, software.
- **job_title_class** (STRING): High-level business function with only 4 values (21.86% null): general_and_administrative, research_and_development, sales_and_marketing, services.

### Previous/Other Company Information
- **other_company_id** (STRING): Previous or destination company ID (39.86% null). 75,125 unique values when populated.
- **other_company_job_title** (STRING): Job title at other company (39.86% null). 69,232 unique values.
- **other_company_job_title_role** (STRING): Role classification at other company (53.80% null). Same 23 categories as main job_title_role.
- **other_company_job_title_sub_role** (STRING): Sub-role at other company (64.73% null). 105 unique values.
- **other_company_job_title_class** (STRING): Business function at other company (87.16% null). Same 4 categories as main classification.

## Potential Query Considerations

### Good for Filtering
- **event_date**: Limited values make it excellent for time-based filtering
- **record_type**: Perfect for separating hires vs departures
- **job_title_role** and **job_title_class**: Good for role-based analysis when not null
- **company_id**: For company-specific analysis

### Good for Grouping/Aggregation
- **event_date**: Time-based trend analysis
- **job_title_role/sub_role/class**: Role distribution analysis
- **company_id**: Company-level metrics
- **record_type**: Hire vs departure metrics

### Potential Join Keys
- **person_id**: Could join with other person-related tables
- **company_id** and **other_company_id**: Could join with company information tables
- Consider that **other_company_id** could match **company_id** in other records to trace talent flows

### Data Quality Considerations
- High null percentages in job classification fields may require careful handling in aggregations
- **other_company_*** fields are only populated for ~60% of records - queries involving these should account for nulls
- Job title fields are highly varied and may need text processing for meaningful analysis
- Event dates are limited to 2025 months - this appears to be recent/projected data

## Keywords
talent flow, employee movement, hiring, departures, job titles, company transitions, workforce analytics, people data, career progression, talent acquisition, employee turnover, job roles, business functions, organizational changes

## Table and Column Docs
*No table comments or column comments were provided in the source analysis.*