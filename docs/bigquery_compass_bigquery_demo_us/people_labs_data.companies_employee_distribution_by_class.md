---
columns:
- company_id (STRING)
- employee_count (INT64)
- job_class (STRING)
schema_hash: 4ec24a365c9a3456a129cb767dfa91c019b0ce2f0616e25f58b04bc0bf5e7f13

---
# Table Summary: people_labs_data.companies_employee_distribution_by_class

## Overall Dataset Characteristics

**Dataset Size:** 17,813,054 rows

**Purpose:** This table stores the distribution of employees across different job classes/departments for companies. Each row represents a specific job class within a company and the count of employees in that class.

**Data Quality:** Excellent - 0% null values across all columns, indicating complete and well-maintained data.

**Key Patterns:**
- The table appears to be a many-to-one relationship where multiple job classes map to individual companies
- With ~10 million unique companies and ~17.8 million rows, companies have on average 1-2 job class entries
- Employee counts vary dramatically from 1 to 306,179, suggesting the dataset includes companies of all sizes from startups to large enterprises
- The data is structured as a fact table tracking employee distribution by job function

## Column Details

### company_id (STRING)
- **Type:** Unique identifier (appears to be a hash/encoded ID)
- **Nulls:** None (0.00%)
- **Cardinality:** 10,078,178 unique companies
- **Format:** Alphanumeric string (e.g., "ho6amsz8ze9iz7sC0fMJ8wmNBZh5")
- **Purpose:** Primary key for joining to company dimension tables

### job_class (STRING)
- **Type:** Categorical dimension
- **Nulls:** None (0.00%)
- **Cardinality:** Only 5 distinct values
- **Values:**
  - `general_and_administrative` - Corporate functions (HR, Finance, Legal, etc.)
  - `sales_and_marketing` - Revenue-generating and customer-facing roles
  - `research_and_development` - Product development and engineering
  - `services` - Customer service and support functions
  - `other_uncategorized` - Roles not fitting standard classifications
- **Purpose:** Categorizes employee distribution by functional area

### employee_count (INT64)
- **Type:** Numeric measure
- **Nulls:** None (0.00%)
- **Range:** 1 to 306,179 employees
- **Cardinality:** 5,880 unique values
- **Distribution:** Heavily right-skewed (small counts are most common, large counts are rare)
- **Common Values:** Low single-digit values (1, 2, 3, etc.) are most frequent
- **Purpose:** Quantifies workforce size within each job class

## Potential Query Considerations

### Filtering Opportunities
- **job_class:** Excellent for filtering by department type (only 5 values, very efficient)
- **company_id:** Can filter to specific companies or sets of companies
- **employee_count:** Use for size-based filtering (e.g., large departments, small teams)
  - Consider thresholds like >100, >1000 for enterprise analysis
  - Use small counts (<10) for startup/SMB analysis

### Aggregation Scenarios
- **GROUP BY job_class:** Analyze workforce distribution across functional areas
- **GROUP BY company_id:** Get total employee counts per company (SUM employee_count)
- **Combined grouping:** Analyze patterns like "average G&A headcount by company size tier"
- **Statistical aggregations:** MIN, MAX, AVG, PERCENTILE on employee_count

### Join Considerations
- **company_id** is the obvious join key to other company-related tables
- Likely joins to:
  - Company master/dimension tables (for industry, location, size classification)
  - Company financial data
  - Company metadata (founding date, funding rounds, etc.)

### Query Performance Tips
- Pre-filter by job_class early in queries (high selectivity)
- When calculating total employees per company, SUM(employee_count) GROUP BY company_id
- Beware of NULL handling in LEFT JOINs (though this table has no nulls)
- Consider company_id distribution - some companies may have all 5 job classes, others may have only 1-2

### Data Quality Considerations
- **Completeness:** Data is 100% complete (no nulls), reliable for calculations
- **Consistency:** Job class taxonomy is standardized (only 5 categories)
- **Granularity caveat:** "other_uncategorized" may contain heterogeneous roles
- **Temporal aspect:** No date columns visible - this appears to be point-in-time or regularly refreshed snapshot data
- **Potential duplicates:** Verify no duplicate (company_id, job_class) pairs exist before aggregation

### Common Query Patterns
1. Total workforce by company: `SUM(employee_count) GROUP BY company_id`
2. Department size analysis: `AVG(employee_count) GROUP BY job_class`
3. Companies with specific functions: `WHERE job_class = 'research_and_development'`
4. Workforce composition: Calculate percentage of workforce in each job class per company
5. Size segmentation: Classify companies by total employee count thresholds

## Keywords

employee distribution, workforce analytics, job classification, company headcount, departmental analysis, organizational structure, employee segmentation, job function, functional areas, R&D headcount, sales team size, administrative staff, service employees, company size, workforce composition, HR analytics, people data, employee counts, organizational breakdown, staffing levels, department size, company_id, job_class, general and administrative, sales and marketing, research and development, services, uncategorized employees

## Table and Column Documentation

**Table Comment:** Not provided

**Column Comments:** Not provided