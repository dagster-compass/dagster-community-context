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

This table tracks **talent flow events** (hires and departures) for individuals across companies, containing **211,892 records**. The data represents employee movements during 2025, specifically covering months May through August and November. 

**Key Observations:**
- The dataset captures bidirectional employment transitions, showing both where people are coming from and where they're going
- Data quality is generally good for core fields (person_id, company_id, event_date, job_title) with 0% null values
- Significant null percentages exist for classification fields, particularly for "other company" attributes (39-87% nulls)
- The data contains 179,589 unique individuals and 113,007 unique companies, indicating many people have multiple records (movements)
- Record types are binary: "hire" or "departure" events

## Column Details

### **Core Identifiers**

**person_id** (STRING)
- Unique identifier for individuals (0% nulls)
- 179,589 unique values across 211,892 records
- Format: alphanumeric with underscores (e.g., "18rSne1BHQeIOd9SROvL7w_0000")
- Some individuals appear multiple times, suggesting multiple job movements

**company_id** (STRING)
- Identifier for the primary company in the event (0% nulls)
- 113,007 unique companies represented
- Format: alphanumeric string (e.g., "5azS3gqXKnBpCvktfe1EBgBmrKpU")

**event_date** (STRING)
- Date of the employment event (0% nulls)
- Only 5 unique values: 2025-05, 2025-06, 2025-07, 2025-08, 2025-11
- Format: YYYY-MM (year-month only, no day precision)
- Data appears to have gaps (no Sept/Oct records visible)

### **Primary Position Information**

**job_title** (STRING)
- Current/new job title at the company (0% nulls)
- 78,750 unique job titles showing high diversity
- Examples: "owner", "chief medical officer", "senior vice president"
- Appears to be free-form text with varying formats

**job_title_class** (STRING)
- High-level categorization of the role (21.86% nulls)
- 4 distinct categories: general_and_administrative, research_and_development, sales_and_marketing, services
- About 1 in 5 positions cannot be classified into these categories

**job_title_role** (STRING)
- Mid-level categorization of job function (21.86% nulls)
- 23 distinct roles including: advisory, analyst, creative, education, engineering, finance, fulfillment, health, hospitality, operations, partnerships, professional_service
- Same null percentage as job_title_class suggests consistent classification coverage

**job_title_sub_role** (STRING)
- Granular categorization of specific function (40.13% nulls)
- 103 distinct sub-roles including: account_executive, account_management, accounting, administrative, advisor, executive, investment_banking, product_management, software, revenue_operations
- Higher null rate indicates more positions lack this detailed classification

### **Secondary Position Information (Previous/Other Company)**

**other_company_id** (STRING)
- Identifier for the company the person is moving from/to (39.86% nulls)
- 75,125 unique other companies
- Nulls represent cases where previous/next company is unknown or the person is entering/leaving the workforce

**other_company_job_title** (STRING)
- Job title at the other company (39.86% nulls)
- 69,232 unique titles
- Examples: "director, marketing and international licensing", "vice president, global ocean logistics"
- Same null rate as other_company_id (consistently paired data)

**other_company_job_title_role** (STRING)
- Role classification at other company (53.80% nulls)
- 23 distinct values (same categories as primary job_title_role)
- Higher null rate than primary position classifications

**other_company_job_title_sub_role** (STRING)
- Sub-role classification at other company (64.73% nulls)
- 105 distinct values
- Similar categories to primary sub_role but with more nulls

**other_company_job_title_class** (STRING)
- Class classification at other company (87.16% nulls)
- 4 distinct values (same as primary job_title_class)
- Very high null percentage - classification rarely available for other company positions

### **Event Type**

**record_type** (STRING)
- Type of talent flow event (0% nulls)
- Only 2 values: "hire" or "departure"
- Critical field for determining direction of talent movement

## Potential Query Considerations

### **Good for Filtering:**
- `event_date` - Limited distinct values make it efficient for time-based filtering
- `record_type` - Binary field perfect for hire vs. departure analysis
- `job_title_class`, `job_title_role` - Good for functional area filtering despite nulls
- `company_id` - For company-specific talent flow analysis

### **Good for Grouping/Aggregation:**
- `event_date` - Trend analysis over months
- `record_type` - Aggregate hire vs. departure metrics
- `job_title_class`, `job_title_role`, `job_title_sub_role` - Talent flow by job function
- `company_id` - Company-level talent metrics (hiring rate, attrition, etc.)

### **Potential Join Keys:**
- `person_id` - Can join to people/employee tables
- `company_id`, `other_company_id` - Can join to company master tables for enrichment
- Consider self-joins on person_id to track individual career progression

### **Data Quality Considerations:**

1. **Null Handling Required:**
   - Job classification fields (class, role, sub_role) have 20-65% nulls
   - "Other company" fields have 40-87% nulls
   - Always use `IS NULL` or `IS NOT NULL` checks when filtering on these fields
   - Consider using `COALESCE()` or `IFNULL()` for default values

2. **Date Limitations:**
   - Only month-level granularity (no specific day)
   - Data appears incomplete (missing Sept/Oct 2025)
   - Not suitable for day-level time series analysis

3. **Bidirectional Logic:**
   - "Hire" records show: current company + previous company
   - "Departure" records show: company being left (may not have other_company populated)
   - Need to carefully interpret the relationship between company_id and other_company_id based on record_type

4. **Title Standardization:**
   - 78,750 unique job titles for primary roles suggests minimal standardization
   - May need text matching/fuzzy matching for title-based analysis
   - Classification fields (role, sub_role, class) provide more standardized grouping but with nulls

5. **Duplicate Considerations:**
   - Multiple records per person_id suggest tracking over time
   - May need to deduplicate or use window functions for "current position" queries

## Keywords

talent flow, employee movement, hiring, departures, attrition, workforce analytics, job transitions, career progression, talent acquisition, employee turnover, job titles, organizational structure, human resources, HR analytics, recruitment, retention, company transitions, employment history, talent mobility, workforce planning, people analytics, job roles, job functions, job classifications, executive movements, employee tracking, headcount changes, personnel changes, staff movements, career changes

## Table and Column Documentation

**Table Comment:** Not provided

**Column Comments:** Not provided