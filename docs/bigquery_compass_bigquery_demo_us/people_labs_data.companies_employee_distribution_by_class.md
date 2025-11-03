---
columns:
- company_id (STRING)
- employee_count (INT64)
- job_class (STRING)
schema_hash: 4ec24a365c9a3456a129cb767dfa91c019b0ce2f0616e25f58b04bc0bf5e7f13

---
# Table Summary: people_labs_data.companies_employee_distribution_by_class

## Overall Dataset Characteristics

**Total Rows:** 17,813,054

**Purpose:** This table provides a breakdown of employee distribution across different job classifications for companies. It's a dimensional table that segments workforce composition by functional areas.

**Data Quality:** 
- Excellent data quality with 0% null values across all columns
- Fully populated dataset with no missing data
- Clean, structured categorical data for job classifications

**Notable Patterns:**
- The table covers over 10 million unique companies, suggesting comprehensive business coverage
- Employee counts range from individual contributors (1) to large divisions (306,179)
- Distribution appears granular, with most unique values in employee_count being on the lower end (1-10)
- Five distinct job classification categories provide standard functional breakdowns

## Column Details

### company_id (STRING)
- **Data Type:** String identifier
- **Null Values:** 0% (fully populated)
- **Cardinality:** 10,078,178 unique companies
- **Format:** Alphanumeric hash/identifier (e.g., "kxTfEknSAigAeHKTmtYZOw62fw21")
- **Purpose:** Primary identifier for companies; likely a foreign key to a companies master table
- **Pattern:** Fixed-length alphanumeric strings, case-sensitive

### job_class (STRING)
- **Data Type:** Categorical string
- **Null Values:** 0% (fully populated)
- **Cardinality:** 5 unique values
- **Categories:**
  1. `general_and_administrative` - Corporate functions (HR, Finance, Legal, Admin)
  2. `research_and_development` - R&D, Engineering, Product Development
  3. `sales_and_marketing` - Revenue-generating and brand functions
  4. `services` - Customer service, support, implementation
  5. `other_uncategorized` - Catch-all for non-standard roles
- **Distribution:** Sample shows broad representation across categories
- **Format:** Lowercase with underscores as separators

### employee_count (INT64)
- **Data Type:** Integer
- **Null Values:** 0% (fully populated)
- **Cardinality:** 5,880 unique values
- **Range:** 1 to 306,179 employees
- **Distribution:** Heavy concentration at lower values (1-10 visible in samples)
- **Pattern:** The maximum value of 306,179 suggests large enterprise divisions are included
- **Interpretation:** Represents the number of employees in a specific job_class for a given company

## Potential Query Considerations

### Ideal for Filtering:
- **job_class:** Perfect for filtering by functional area (5 categories make it efficient)
- **employee_count ranges:** Can filter for company size tiers (small: 1-10, medium: 11-100, large: 100+)
- **company_id:** Direct lookup for specific company analysis

### Ideal for Aggregation/Grouping:
- **job_class:** Natural grouping dimension for workforce composition analysis
- **SUM(employee_count):** Calculate total workforce by company or by job class
- **AVG(employee_count):** Understand average team sizes per function
- **company_id + job_class:** Combined grouping for company-level functional analysis

### Join Considerations:
- **company_id:** Primary join key to company master tables (likely contains company name, industry, size, location)
- **Grain:** Each row represents one job_class per company (companies will have multiple rows)
- **Expected Relationships:** Many-to-one with a companies table

### Data Quality Considerations:
- **Multiple rows per company:** A single company can have up to 5 rows (one per job_class)
- **Not all companies have all classes:** Some companies may only have certain job_class entries
- **Summation accuracy:** To get total company headcount, must SUM across all job_class values for that company_id
- **Snapshot nature:** This appears to be a point-in-time snapshot; no date/timestamp column suggests it's current state only

### Analytical Use Cases:
1. **Workforce composition:** Percentage breakdown by function across companies
2. **Company sizing:** Total headcount calculation via aggregation
3. **Industry benchmarking:** Compare job_class distributions across similar companies
4. **Organizational structure analysis:** Identify companies with heavy R&D vs. sales focus
5. **Segmentation:** Classify companies by workforce characteristics

## Keywords

employee distribution, workforce composition, job classification, company headcount, organizational structure, functional areas, employee count, R&D staff, sales staff, administrative staff, services staff, company size, team size, human resources data, labor force analysis, business intelligence, company_id, people analytics, workforce segmentation, employment data

## Table and Column Documentation

**Table Comment:** Not provided

**Column Comments:** Not provided