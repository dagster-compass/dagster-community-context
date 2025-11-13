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
# Table Documentation Summary: people_labs_data.companies_talent_flow_details

## Overall Dataset Characteristics

This table tracks **talent flow events** (hires and departures) for companies, containing **211,892 records** representing employee movements between organizations. The data spans 5 months in 2025 (May through August, plus November) and captures detailed information about job roles, titles, and company transitions.

**Key Observations:**
- Dataset tracks 179,589 unique individuals across 113,007 companies
- Nearly balanced between hire and departure events (2 record types)
- High variability in job titles (78,750 unique titles)
- Significant null values in classification fields suggest incomplete categorization
- Data appears to be sourced from professional profile/employment tracking systems
- Strong focus on tracking career transitions with origin and destination companies

**Data Quality Notes:**
- Core fields (company_id, person_id, event_date, job_title, record_type) have 0% nulls
- Classification fields have moderate to high null rates (21-87%)
- "Other company" fields (representing previous/next employer) have 40-87% nulls, which is expected for departures without known destinations or hires without known origins

## Column Details

### **job_title** (STRING)
- **Null Rate:** 0% - Complete data
- **Cardinality:** 78,750 unique values (high diversity)
- **Description:** Current/primary job title for the person at the company
- **Sample Values:** "co president", "chief sales officer (cso)", "senior vice president of it"
- **Patterns:** Mix of executive titles, specialized roles, and various seniority levels

### **event_date** (STRING)
- **Null Rate:** 0% - Complete data
- **Cardinality:** 5 values only
- **Values:** 2025-05, 2025-06, 2025-07, 2025-08, 2025-11
- **Format:** YYYY-MM format (year-month)
- **Note:** Gap between August and November may indicate data collection periods or actual business patterns

### **person_id** (STRING)
- **Null Rate:** 0% - Complete data
- **Cardinality:** 179,589 unique individuals
- **Format:** Alphanumeric hash with "_0000" suffix pattern
- **Purpose:** Unique identifier for individuals in the talent database

### **company_id** (STRING)
- **Null Rate:** 0% - Complete data
- **Cardinality:** 113,007 unique companies
- **Format:** Alphanumeric hash (variable length)
- **Purpose:** Unique identifier for the primary company in the event

### **job_title_sub_role** (STRING)
- **Null Rate:** 40.13% - Moderate missing data
- **Cardinality:** 103 values
- **Values:** Standardized categories like "executive", "financial", "quality_assurance", "investment_banking", "training"
- **Purpose:** Granular role classification beneath the role level

### **job_title_role** (STRING)
- **Null Rate:** 21.86% - Some missing data
- **Cardinality:** 23 values
- **Values:** Broad categories like "operations", "sales", "finance", "engineering", "manufacturing", "professional_service", "human_resources"
- **Purpose:** Mid-level job function classification

### **job_title_class** (STRING)
- **Null Rate:** 21.86% - Some missing data
- **Cardinality:** 4 values only
- **Values:** "general_and_administrative", "research_and_development", "sales_and_marketing", "services"
- **Purpose:** Highest-level departmental classification
- **Pattern:** Aligns with standard financial reporting categories

### **other_company_id** (STRING)
- **Null Rate:** 39.86% - Significant missing data
- **Cardinality:** 75,125 unique companies
- **Format:** Same as company_id
- **Purpose:** Identifier for the previous employer (for hires) or next employer (for departures)
- **Note:** Nulls expected when destination/origin is unknown

### **other_company_job_title_role** (STRING)
- **Null Rate:** 53.80% - High missing data
- **Cardinality:** 23 values (same categories as job_title_role)
- **Purpose:** Role classification at the other company

### **other_company_job_title** (STRING)
- **Null Rate:** 39.86% - Significant missing data
- **Cardinality:** 69,232 unique values
- **Purpose:** Job title at the other company
- **Pattern:** Similar diversity to primary job_title field

### **other_company_job_title_class** (STRING)
- **Null Rate:** 87.16% - Very high missing data
- **Cardinality:** 4 values (same as job_title_class)
- **Purpose:** Departmental classification at other company
- **Note:** Most sparse classification field

### **other_company_job_title_sub_role** (STRING)
- **Null Rate:** 64.73% - High missing data
- **Cardinality:** 105 values
- **Purpose:** Granular role at other company

### **record_type** (STRING)
- **Null Rate:** 0% - Complete data
- **Cardinality:** 2 values only
- **Values:** "departure", "hire"
- **Purpose:** Indicates whether event is an employee joining or leaving
- **Pattern:** Core classification for talent flow direction

## Potential Query Considerations

### **Excellent for Filtering:**
- `event_date` - Limited values, perfect for time-based analysis
- `record_type` - Binary classification (hire/departure) for flow direction
- `job_title_class` - Only 4 categories, good for high-level department filtering
- `job_title_role` - 23 categories, useful for functional area analysis
- `company_id` - For company-specific talent analysis

### **Good for Grouping/Aggregation:**
- `event_date` - Time series analysis of talent flows
- `record_type` - Comparing hire vs. departure volumes
- `job_title_class` / `job_title_role` / `job_title_sub_role` - Hierarchical role analysis
- `company_id` - Company-level metrics (turnover, hiring activity)
- `other_company_id` - Talent source/destination analysis

### **Potential Join Keys:**
- `company_id` - Primary key for joining to company dimension tables
- `person_id` - For tracking individual career trajectories
- `other_company_id` - For company relationship/network analysis
- Consider self-joins on person_id for career path analysis

### **Data Quality Considerations:**

1. **Null Handling Critical:**
   - Classification fields have 21-87% nulls - always use `IS NULL` checks or COALESCE
   - "Other company" fields naturally null for some scenarios (departures without known destination)
   - Queries on classified roles will lose 20-40% of records without null handling

2. **Text Analysis Needed:**
   - `job_title` fields are free-text with 78K variants - use LIKE patterns or regex for role matching
   - Consider case-insensitive matching for title searches

3. **Temporal Patterns:**
   - Limited to 5 months with a gap - be careful with trend analysis
   - Use WHERE clauses to specify exact months rather than date ranges

4. **Cardinality Considerations:**
   - High person_id cardinality (179K) - good for aggregation but watch for performance on GROUP BY
   - Very high company cardinality (113K) - similar consideration

5. **Bidirectional Flow Analysis:**
   - Can track company-to-company talent movement by matching `company_id` to `other_company_id`
   - Useful for competitive talent analysis and company relationship networks

## Keywords

talent flow, employee movement, hiring data, departures, turnover, workforce analytics, job titles, career transitions, company recruitment, talent acquisition, employee retention, job roles, organizational structure, headcount changes, talent pipeline, employment history, career mobility, company transitions, workforce planning, HR analytics, people analytics, professional roles, job classifications, departmental assignments, talent tracking, employment events, hire dates, departure dates, company transfers, job functions, role hierarchies

## Table and Column Docs

**Table Comment:** Not provided

**Column Comments:** Not provided for any columns

---

*Note: This table appears to be part of a People Labs data product focused on tracking talent movements across companies. The structure supports both point-in-time snapshots of hiring/departure events and longitudinal analysis of career paths and company talent flows.*