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
- **Data Quality**: Good overall data quality with no null values in core identifier columns (company_id, person_id, job_title, event_date, record_type)
- **Notable Patterns**: 
  - Dataset covers talent movement events (hires and departures) across 5 months in 2025
  - High variability in job titles (78,750 unique values) suggesting detailed, specific role descriptions
  - Significant null percentages in "other_company" fields indicate many internal moves or incomplete data
  - Strong hierarchical structure with job title classifications at multiple levels

## Column Details

### **Core Identifiers**
- **company_id** (STRING): No nulls, 113,007 unique companies represented
- **person_id** (STRING): No nulls, 179,589 unique individuals tracked
- **record_type** (STRING): No nulls, binary classification (hire/departure)

### **Temporal Data**
- **event_date** (STRING): No nulls, 5 distinct months (2025-05 through 2025-11, with gaps)
- Format: YYYY-MM, suitable for time-series analysis

### **Job Classification Hierarchy**
- **job_title** (STRING): No nulls, highly granular with 78,750 unique titles
- **job_title_class** (STRING): 21.86% nulls, 4 categories (general_and_administrative, research_and_development, sales_and_marketing, services)
- **job_title_role** (STRING): 21.86% nulls, 23 categories (operations, marketing, finance, etc.)
- **job_title_sub_role** (STRING): 40.13% nulls, 103 subcategories (executive, product_management, etc.)

### **Previous/Other Company Data**
- **other_company_id** (STRING): 39.86% nulls, 75,125 unique companies
- **other_company_job_title** (STRING): 39.86% nulls, 69,232 unique titles
- **other_company_job_title_class** (STRING): 87.16% nulls, same 4 categories as main job
- **other_company_job_title_role** (STRING): 53.80% nulls, same 23 categories
- **other_company_job_title_sub_role** (STRING): 64.73% nulls, 105 subcategories

## Potential Query Considerations

### **Good for Filtering**
- `record_type`: Binary classification for hire/departure analysis
- `event_date`: Time-based filtering for trend analysis
- `job_title_class`: High-level departmental filtering
- `job_title_role`: Mid-level functional filtering
- `company_id`: Company-specific analysis

### **Good for Grouping/Aggregation**
- `event_date`: Monthly talent flow trends
- `job_title_class`: Departmental hiring/departure patterns
- `job_title_role`: Functional area analysis
- `record_type`: Hire vs departure metrics
- `company_id`: Company-level talent metrics

### **Potential Join Keys**
- `company_id` and `other_company_id`: Company master table joins
- `person_id`: Person/employee master table joins
- Job classification fields: Role hierarchy or compensation tables

### **Data Quality Considerations**
- High null percentage in `other_company_job_title_class` (87.16%) limits cross-company role comparison analysis
- Inconsistent null patterns between related fields may require careful handling in queries
- Job title variations are extremely high - consider using classification fields for consistent grouping
- Some `other_company_job_title` values appear to be personal status rather than job titles ("retired and going back to school", "man")

## Keywords

talent flow, employee movement, hiring data, departure data, job titles, company transitions, workforce analytics, talent acquisition, employee turnover, organizational structure, job classifications, career transitions, HR analytics, people data, employment history

## Table and Column Documentation

No table or column comments were provided in the analysis report.