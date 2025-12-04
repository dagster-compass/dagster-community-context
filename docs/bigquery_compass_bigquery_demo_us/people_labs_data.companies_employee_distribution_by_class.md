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

**General Description:** This table contains employee distribution data across different job classifications for companies. It represents a many-to-many relationship where each company can have multiple job class entries, showing how employees are distributed across functional areas within each organization.

**Data Quality:** 
- Excellent data quality with 0% null values across all columns
- No missing data detected in any field
- Complete dataset suitable for analytical queries

**Notable Patterns:**
- Dataset covers over 10 million unique companies
- Small to medium-sized companies dominate (employee counts typically range 1-10 per job class)
- Some very large organizations present (maximum 306,179 employees in a single job class)
- Five distinct job classification categories standardized across all companies

## Column Details

### 1. company_id (STRING)
- **Data Type:** STRING identifier
- **Null Pattern:** No nulls (0.00%)
- **Cardinality:** 10,078,178 unique companies
- **Format:** Alphanumeric hash-like identifiers (e.g., "UlpKeFqGGEoRDsCXZpOaGQZaVg9i")
- **Characteristics:** Primary identifier for companies; each company typically appears multiple times (once per job class they have employees in)
- **Average Records per Company:** ~1.77 job classes per company

### 2. job_class (STRING)
- **Data Type:** STRING (categorical)
- **Null Pattern:** No nulls (0.00%)
- **Cardinality:** 5 unique values (enumerated list)
- **Possible Values:**
  - `general_and_administrative` - Corporate support functions
  - `other_uncategorized` - Employees not fitting standard classifications
  - `research_and_development` - R&D and innovation roles
  - `sales_and_marketing` - Revenue-generating functions
  - `services` - Service delivery and operations roles
- **Distribution:** Services appears frequently in samples, suggesting it may be a common category
- **Use Case:** Categorical grouping variable for employee classification

### 3. employee_count (INT64)
- **Data Type:** Integer
- **Null Pattern:** No nulls (0.00%)
- **Range:** 1 to 306,179 employees
- **Cardinality:** 5,880 distinct values
- **Distribution Characteristics:**
  - Heavy concentration in low values (1-10 employees per job class)
  - Long tail distribution with some extremely large counts
  - Sample data shows predominantly small counts (1, 1, 1, 7, 1)
- **Statistical Notes:** Represents employee headcount within a specific job classification for a given company

## Potential Query Considerations

### Excellent for Filtering:
- **job_class**: Perfect for filtering by functional area (5 distinct categories)
- **company_id**: Ideal for company-specific analysis
- **employee_count**: Good for range filters (e.g., WHERE employee_count > 100)

### Excellent for Grouping/Aggregation:
- **job_class**: Natural grouping dimension for organizational analysis
- **company_id**: Group by company to get total workforce or distribution profiles
- **Combined grouping**: GROUP BY company_id, job_class provides granular breakdowns

### Aggregation Opportunities:
- SUM(employee_count) by job_class for industry-wide workforce composition
- COUNT(DISTINCT company_id) for company prevalence by job class
- AVG(employee_count) for typical workforce size by classification
- Percentile analysis of employee_count distributions

### Join Key Capabilities:
- **company_id**: Primary join key to other company-related tables
- Likely joins to:
  - Company master tables (company details, industry, location)
  - Financial data tables
  - Other employee-related datasets

### Data Quality Considerations:
- **No null handling required**: All fields are complete
- **Small company bias**: Many companies have single-digit employee counts per class
- **Outlier awareness**: Some extreme values (306K+) may skew averages
- **Categorical stability**: Fixed set of 5 job classes ensures consistent queries
- **Consider using MEDIAN instead of AVG** for employee_count due to long-tail distribution

### Recommended Query Patterns:
1. Total workforce by company: `SUM(employee_count) GROUP BY company_id`
2. Workforce composition: `SUM(employee_count) GROUP BY job_class`
3. Company size segmentation: Use CASE statements on summed employee_count
4. Distribution analysis: Use percentile functions (PERCENTILE_CONT) for employee_count
5. Classification prevalence: `COUNT(DISTINCT company_id) GROUP BY job_class`

## Keywords

employee distribution, workforce composition, job classification, company workforce, organizational structure, headcount analysis, functional areas, employee segmentation, R&D headcount, sales workforce, administrative staff, service employees, company demographics, workforce analytics, people data, HR analytics, employee categories, organizational breakdown, staffing levels, company size, workforce metrics

## Table and Column Documentation

**Table Comment:** Not provided

**Column Comments:** Not provided