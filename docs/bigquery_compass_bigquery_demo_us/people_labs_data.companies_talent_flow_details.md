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
# Table Summary: people_labs_data.companies_talent_flow_details

## Overall Dataset Characteristics

**Total Rows:** 211,892

**General Description:** This table tracks employee movement (hires and departures) across companies, capturing detailed information about job roles, titles, and transitions between organizations. The data represents talent flow events occurring in 2025 (months 05-08 and 11).

**Data Quality Observations:**
- Core identifiers (person_id, company_id, event_date, job_title, record_type) have no null values
- Significant null percentages in classification fields: job_title_sub_role (40%), job_title_class (22%), job_title_role (22%)
- "Other company" fields have high null rates (40-87%), which is expected as departures may not always have a destination company, and hires may come from unemployment or non-tracked sources
- The data appears to be forward-looking (all dates are in 2025), suggesting this may be predictive or projected data

**Notable Patterns:**
- 179,589 unique individuals across 211,892 records indicates some people have multiple events
- 113,007 unique companies involved
- 78,750 unique job titles showing high diversity in role descriptions
- Only 5 distinct months of data (May, June, July, August, November 2025)

## Column Details

### Core Identifiers

**person_id** (STRING)
- No null values (100% populated)
- 179,589 unique values out of 211,892 rows
- Format: Alphanumeric strings with underscores (e.g., "0Ohfd005KzO3RGHbWITlJA_0000")
- Purpose: Unique identifier for individuals, some individuals appear multiple times

**company_id** (STRING)
- No null values (100% populated)
- 113,007 unique companies
- Format: Alphanumeric strings (e.g., "E44GC7tpJfGDiJk1jpO9mgjUqeXv")
- Purpose: Identifier for the primary company in the talent flow event

**event_date** (STRING)
- No null values (100% populated)
- Only 5 unique values: 2025-05, 2025-06, 2025-07, 2025-08, 2025-11
- Format: YYYY-MM (year-month)
- Pattern: Concentrated in specific months, with a gap between August and November

**record_type** (STRING)
- No null values (100% populated)
- Only 2 values: "hire" or "departure"
- Purpose: Indicates whether the event is an employee joining or leaving the company

### Primary Job Information

**job_title** (STRING)
- No null values (100% populated)
- 78,750 unique values (high cardinality)
- Examples: "vice president quality assurance", "chief data officer", "controller"
- Very diverse, ranging from C-level executives to specific functional roles

**job_title_role** (STRING)
- 21.86% null values
- 23 unique values
- Categories: sales, engineering, operations, finance, professional_service, creative, analyst, advisory, education, fulfillment, health, hospitality, etc.
- Purpose: High-level role categorization

**job_title_sub_role** (STRING)
- 40.13% null values (significant missing data)
- 103 unique values
- Examples: business_development, strategy, investment_banking, accounting, executive
- Purpose: More granular role categorization within the main role

**job_title_class** (STRING)
- 21.86% null values
- Only 4 unique values: general_and_administrative, research_and_development, sales_and_marketing, services
- Purpose: Broad organizational classification of the role

### Other Company Information (Previous/Next Employment)

**other_company_id** (STRING)
- 39.86% null values
- 75,125 unique companies
- Purpose: Identifier for the company the person is moving from (for hires) or to (for departures)
- High null rate is logical: departures may be to unemployment/retirement, hires may be from non-tracked sources

**other_company_job_title** (STRING)
- 39.86% null values
- 69,232 unique values
- Examples: "vice president", "chief compliance officer", "senior advisor"
- Purpose: Job title at the other company

**other_company_job_title_role** (STRING)
- 53.80% null values
- 23 unique values (same categories as job_title_role)
- Purpose: Role categorization at other company

**other_company_job_title_sub_role** (STRING)
- 64.73% null values (highest null rate among other_company fields)
- 105 unique values
- Purpose: Sub-role categorization at other company

**other_company_job_title_class** (STRING)
- 87.16% null values (extremely sparse)
- Only 4 unique values (same as job_title_class)
- Purpose: Classification of role at other company

## Potential Query Considerations

### Good Filtering Columns:
- **record_type**: Simple binary filter (hire vs departure)
- **event_date**: Time-based filtering (though limited to 5 months)
- **job_title_role**: Categorical filtering with 23 distinct roles
- **job_title_class**: High-level filtering with 4 broad categories
- **company_id**: For company-specific analysis

### Good Grouping/Aggregation Columns:
- **event_date**: Trend analysis over time
- **record_type**: Comparing hires vs departures
- **job_title_role**: Analyzing talent flow by functional area
- **job_title_class**: High-level departmental analysis
- **company_id**: Company-level aggregations

### Potential Join Keys:
- **person_id**: Join to people/employee dimension tables
- **company_id**: Join to company dimension/profile tables
- **other_company_id**: Join to company tables for transition analysis

### Data Quality Considerations:

1. **Null Handling**: Queries should account for high null percentages in:
   - Other company fields (40-87% nulls) - use `IS NULL` checks or `COALESCE`
   - Job classification fields (22-40% nulls) - may need to filter or group "unknown" separately

2. **Date Limitations**: Only 5 months of data available, with a gap between August and November 2025

3. **Duplicate Person Events**: Since 179,589 unique people appear in 211,892 rows, be careful with person-level aggregations to avoid double-counting

4. **Text Analysis**: The job_title fields have very high cardinality (78,750 values), requiring careful handling:
   - Use LIKE or REGEXP for pattern matching
   - Consider the structured classification fields (role, sub_role, class) for more reliable grouping

5. **Directionality**: For talent flow analysis, consider both hire and departure records to understand net movement between companies

## Keywords

talent acquisition, employee turnover, workforce analytics, hiring trends, attrition analysis, job transitions, career mobility, organizational movement, talent flow, people analytics, recruitment data, departure tracking, job roles, employment events, workforce planning, HR analytics, employee retention, company transitions, job titles, career progression, headcount changes, talent management, people movement, organizational churn

## Table and Column Documentation

**Table Comment:** Not provided

**Column Comments:** Not provided