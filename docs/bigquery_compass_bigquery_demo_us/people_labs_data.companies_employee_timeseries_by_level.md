---
columns:
- company_id (STRING)
- employee_count (INT64)
- level (STRING)
- month_date (STRING)
schema_hash: a4a68bd81a642b890c2263843fc594c3f207689ec7e49ebbdc4834e6f89e20d9

---
# Comprehensive Table Summary: companies_employee_timeseries_by_level

## Overall Dataset Characteristics

- **Total Rows**: 10,466,558,360 (over 10 billion records)
- **Table Type**: Time-series employee count data segmented by organizational level
- **Data Quality**: Excellent - 0% null values across all columns
- **Time Range**: January 2010 onwards (188 unique months, suggesting data through approximately 2025)
- **Granularity**: Monthly snapshots of employee counts at different organizational levels for each company

**Key Patterns**:
- This is a massive time-series dataset tracking workforce composition over time
- Each row represents a specific company's employee count at a particular level for a given month
- Many records show 0 employees (indicating either no employees at that level or historical gaps)
- Data structure suggests comprehensive tracking of organizational hierarchy changes

## Column Details

### month_date (STRING)
- **Format**: YYYY-MM (e.g., "2010-01", "2014-08", "2023-08")
- **Null Values**: None (0.00%)
- **Unique Values**: 188 distinct months
- **Date Range**: 2010-01 through approximately 2025-08 (based on sample showing 2023-08)
- **Notes**: Stored as string rather than DATE type; represents the first day of each month
- **Use Cases**: Primary time-series dimension for trend analysis, filtering by date ranges, temporal aggregations

### level (STRING)
- **Null Values**: None (0.00%)
- **Unique Values**: 10 distinct organizational levels
- **Complete Value Set**:
  - `cxo` - C-suite executives (CEO, CFO, CTO, etc.)
  - `director` - Director-level positions
  - `entry` - Entry-level employees
  - `manager` - Manager positions
  - `owner` - Business owners
  - `partner` - Partners (common in professional services)
  - `senior` - Senior-level individual contributors
  - `training` - Employees in training programs
  - `unpaid` - Unpaid positions (interns, volunteers)
  - `vp` - Vice President positions
- **Notes**: Represents a hierarchical classification from entry to executive levels
- **Use Cases**: Grouping by organizational level, filtering for specific hierarchy tiers, workforce composition analysis

### employee_count (INT64)
- **Null Values**: None (0.00%)
- **Unique Values**: 26,016 distinct counts
- **Range**: 0 to 120,165 employees
- **Distribution**: Heavy skew toward lower values (many 0s and small counts in samples)
- **Notes**: Integer counts representing number of employees at a specific level for a company in a given month
- **Use Cases**: Primary metric for aggregation, trend analysis, workforce size calculations

### company_id (STRING)
- **Null Values**: None (0.00%)
- **Unique Values**: 16,020,211 distinct companies
- **Format**: Alphanumeric hash strings (28 characters, mixed case)
- **Examples**: "jozwklhnXe5kK10qrotwkgow3A6X", "SAYH9H3NbLsp3Oz8jflRYQGheSIW"
- **Notes**: Anonymized/hashed company identifiers; primary entity dimension
- **Use Cases**: Filtering specific companies, joining with other company tables, grouping for company-level aggregations

## Potential Query Considerations

### Optimal Filtering Columns
1. **month_date**: Essential for time-based queries and trend analysis
   - Consider converting to DATE type in queries for proper date operations
   - Format: `PARSE_DATE('%Y-%m', month_date)`
2. **company_id**: For company-specific analysis (though may require additional lookup tables for meaningful company names)
3. **level**: For organizational tier analysis (e.g., executive vs. entry-level trends)
4. **employee_count**: For filtering by company size thresholds (e.g., WHERE employee_count > 100)

### Optimal Grouping/Aggregation Columns
1. **month_date**: Time-series aggregations (monthly, quarterly, yearly trends)
2. **level**: Workforce composition analysis across hierarchy
3. **company_id**: Company-level summaries
4. **Combinations**: month_date + level for hierarchical trends over time

### Join Considerations
- **company_id**: Primary join key to other company dimension tables (e.g., company details, industry, location)
- Likely part of a star schema where this is a fact table
- No obvious foreign keys to other tables in this dataset alone

### Data Quality Considerations

**Strengths**:
- Zero null values ensures reliable aggregations
- Consistent formatting across all fields
- Complete time-series coverage (188 months)

**Query Optimization Concerns**:
1. **Massive Scale**: 10+ billion rows require careful query optimization
   - Always use partitioning on month_date if available
   - Limit date ranges in WHERE clauses
   - Use appropriate aggregation levels to reduce result sets
2. **Zero Values**: Many records have employee_count = 0
   - Consider whether to include zeros in analyses (depends on use case)
   - May want to filter WHERE employee_count > 0 for active workforce analysis
3. **String Date Format**: Requires parsing for date operations
   - Pre-parse dates in subqueries for complex temporal logic
4. **Cardinality**: 16M companies × 188 months × 10 levels = theoretical max of ~30B records
   - Actual data (~10B) suggests sparse data or filtered companies

### Recommended Query Patterns

1. **Time-Series Analysis**: Always partition/filter by date range first
2. **Company Analysis**: Aggregate across time and levels for company profiles
3. **Level Distribution**: Sum employee_count by level and month for organizational trends
4. **Growth Metrics**: Use LAG/LEAD window functions with PARTITION BY company_id, level
5. **Active Companies**: Consider filtering companies with employee_count > 0 for meaningful analysis

## Keywords

time-series, employee data, workforce analytics, organizational hierarchy, company employees, headcount, staffing levels, employee count by level, monthly snapshots, organizational structure, CXO, executives, directors, managers, senior staff, entry level, business owners, partners, unpaid staff, training programs, company_id, workforce composition, employee trends, headcount tracking, organizational levels, temporal data, people analytics, HR analytics, workforce intelligence, company growth, staffing trends

## Table and Column Documentation

**Table Comment**: Not provided

**Column Comments**: Not provided

---

**Analysis Note**: This table appears to be a core fact table in a people analytics/workforce intelligence system, tracking how companies' workforce composition changes over time across different organizational levels. The massive scale and comprehensive coverage make it suitable for enterprise-level workforce analytics, market intelligence, and trend analysis applications.