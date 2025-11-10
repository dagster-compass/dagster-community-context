---
columns:
- company_id (STRING)
- employee_count (INT64)
- role (STRING)
schema_hash: 51368c4f020428e9d698aaf80c8cd3744fb72c34ed4d1d8ed34fc89cbe090029

---
# Table Documentation Summary: people_labs_data.companies_employee_distribution_by_role

## Overall Dataset Characteristics

**Total Rows:** 22,588,172

**Data Quality:** Excellent - No null values detected in any column (0.00% null across all fields)

**Dataset Purpose:** This table provides a detailed breakdown of employee distribution across different job roles/functions for approximately 10 million companies. It represents a many-to-many relationship where each company can have multiple role entries, each with its associated employee count.

**Key Patterns:**
- High cardinality in company_id (~10M unique companies)
- Low cardinality in role (24 distinct role categories)
- Wide range of employee counts (1 to 303,046 employees per role)
- Most common employee counts are small numbers (1-10), suggesting many small companies or specialized roles
- Average of ~2.24 role entries per company (22.6M rows / 10M companies)

## Column Details

### 1. **company_id** (STRING)
- **Data Type:** STRING identifier
- **Null Pattern:** No nulls (0.00%)
- **Cardinality:** 10,078,178 unique values
- **Format:** Alphanumeric hash-like identifiers (e.g., "AQo2HdrWxX4s7kfP8zQaMgEVUs1B")
- **Distribution:** High cardinality - serves as the primary entity identifier
- **Purpose:** Unique identifier for companies; acts as the dimensional key

### 2. **role** (STRING)
- **Data Type:** STRING categorical
- **Null Pattern:** No nulls (0.00%)
- **Cardinality:** 24 unique values
- **Known Values:** advisory, analyst, creative, education, engineering, finance, fulfillment, health, hospitality, human_resources, manufacturing, operations, other_uncategorized
- **Distribution:** Limited set of business function categories
- **Purpose:** Categorizes employees by their functional role/department within companies
- **Note:** Includes catch-all category "other_uncategorized" for roles not fitting standard classifications

### 3. **employee_count** (INT64)
- **Data Type:** Integer
- **Null Pattern:** No nulls (0.00%)
- **Cardinality:** 5,454 unique values
- **Range:** 1 to 303,046 employees
- **Distribution:** Heavily skewed toward lower values (samples show predominantly 1-10)
- **Common Values:** Small numbers (1, 2, 3, etc.) appear most frequently
- **Maximum:** 303,046 suggests very large enterprises represented
- **Purpose:** Quantifies the number of employees in each role category for a given company

## Table and Column Documentation

**Table Comment:** Not provided

**Column Comments:** Not provided

## Potential Query Considerations

### Ideal for Filtering:
- **role:** Perfect for filtering by specific job functions (e.g., `WHERE role = 'engineering'`)
- **employee_count:** Useful for size-based filtering (e.g., `WHERE employee_count >= 100` for large departments)
- **company_id:** Essential for company-specific queries

### Ideal for Grouping/Aggregation:
- **role:** Excellent GROUP BY dimension for cross-company role analysis
- **company_id:** GROUP BY to aggregate total employees per company or count roles per company
- **Aggregation patterns:**
  - `SUM(employee_count)` to get total employees
  - `COUNT(DISTINCT role)` to measure role diversity
  - `AVG(employee_count)` for average department sizes

### Join Key Candidates:
- **company_id:** Primary join key to other company-related tables (company details, revenue, industry, location, etc.)
- Likely joins to tables with company master data, financials, or geographic information

### Query Use Cases:
1. **Company Size Analysis:** Calculate total headcount per company
2. **Role Distribution:** Analyze which roles are most common across industries
3. **Department Size Benchmarking:** Compare engineering vs sales team sizes
4. **Organizational Structure:** Identify companies with diverse vs specialized workforces
5. **Filtering Large Companies:** Identify enterprises with >1000 employees in specific roles

### Data Quality Considerations:
- **No null handling required** - all fields are complete
- **Employee count accuracy:** Values represent point-in-time snapshots; may need date context from related tables
- **Role classification:** Some ambiguity with "other_uncategorized" category
- **Completeness:** Not all companies may have all roles represented (absence of role ≠ 0 employees)
- **Aggregation caveat:** One company can have multiple role entries; always use SUM for total headcount
- **Scale considerations:** 22M+ rows require efficient indexing for performant queries

### Performance Optimization Tips:
- Index on `company_id` for company-specific lookups
- Index on `role` for role-based filtering
- Consider partitioning by role or company_id ranges for large analytical queries
- Pre-aggregate totals if frequently querying total company headcount

## Keywords

employee distribution, workforce composition, company headcount, organizational structure, job roles, business functions, department sizes, employee counts, company staffing, role categories, engineering, finance, operations, sales, human resources, people analytics, workforce analytics, company demographics, organizational analysis, headcount by role, functional teams, company size, enterprise data, B2B data, company intelligence