---
columns:
- company_id (STRING)
- employee_count (INT64)
- level (STRING)
- month_date (STRING)
schema_hash: a4a68bd81a642b890c2263843fc594c3f207689ec7e49ebbdc4834e6f89e20d9

---
# Table Summary: people_labs_data.companies_employee_timeseries_by_level

## Overall Dataset Characteristics

- **Total Rows**: 10,466,558,360 (approximately 10.5 billion rows)
- **Dataset Type**: Time-series data tracking employee counts by organizational level across companies
- **Time Range**: Data spans from 2010-01 to at least 2025-04 (188 unique months, approximately 15+ years)
- **Data Quality**: Excellent - 0% null values across all columns
- **Key Pattern**: This appears to be a comprehensive employee census table with monthly snapshots of headcount segmented by job level for millions of companies
- **Notable Observation**: Many records show 0 employee counts, suggesting either sparse data, company dormancy periods, or placeholder records for complete time-series continuity

## Column Details

### month_date (STRING)
- **Type**: String representation of year-month (format: YYYY-MM)
- **Nulls**: 0.00% (complete data)
- **Cardinality**: 188 unique months
- **Range**: 2010-01 to 2025-04 (includes future projections/planned data)
- **Format Pattern**: Consistent YYYY-MM format
- **Usage**: Primary temporal dimension for time-series analysis

### level (STRING)
- **Type**: Categorical string representing organizational hierarchy
- **Nulls**: 0.00% (complete data)
- **Cardinality**: 10 distinct levels
- **Values**: 
  - `cxo` - C-suite executives
  - `director` - Director level
  - `entry` - Entry-level positions
  - `manager` - Management level
  - `owner` - Business owners
  - `partner` - Partners
  - `senior` - Senior level
  - `training` - Trainees/interns
  - `unpaid` - Unpaid positions (volunteers, interns)
  - `vp` - Vice Presidents
- **Hierarchy**: Represents standard corporate organizational structure
- **Usage**: Primary grouping dimension for workforce composition analysis

### employee_count (INT64)
- **Type**: Integer count
- **Nulls**: 0.00% (complete data)
- **Cardinality**: 26,016 unique values
- **Range**: 0 to 120,165
- **Distribution**: Heavy concentration at 0 and low single digits (0-9 appear frequently in samples)
- **Pattern**: Right-skewed distribution - most companies have small headcounts per level, with rare cases of very large counts (max 120k+)
- **Zero Values**: Significant presence of zeros suggests sparse data or inactive periods
- **Usage**: Primary metric for aggregation and analysis

### company_id (STRING)
- **Type**: Alphanumeric identifier
- **Nulls**: 0.00% (complete data)
- **Cardinality**: 16,020,211 unique companies (approximately 16 million)
- **Format**: 28-character alphanumeric strings (e.g., "0001FB6m8lpCOvqlHQLq9gdUhMF4")
- **Pattern**: Consistent length and character set (likely base62 or similar encoding)
- **Usage**: Primary key component (with month_date and level), foreign key for joining to company dimension tables

## Potential Query Considerations

### Filtering Recommendations
- **month_date**: Excellent for date range filtering; use string comparison (e.g., `>= '2020-01'`) or PARSE_DATE for temporal operations
- **level**: Ideal for filtering specific organizational levels or excluding certain categories (e.g., exclude 'unpaid' and 'training')
- **company_id**: Direct lookup for specific company analysis
- **employee_count**: Filter for active companies (`WHERE employee_count > 0`) to exclude sparse/inactive records

### Grouping/Aggregation Opportunities
- **Time-series analysis**: GROUP BY month_date for trend analysis
- **Organizational composition**: GROUP BY level to understand workforce distribution
- **Company-level aggregates**: SUM(employee_count) GROUP BY company_id, month_date for total headcount
- **Multi-dimensional analysis**: GROUP BY month_date, level for detailed workforce evolution

### Join Considerations
- **company_id**: Primary foreign key to join with company dimension tables (likely containing company name, industry, size, location, etc.)
- **Composite key**: (company_id, month_date, level) forms a unique identifier for each record
- **Potential relationships**: 
  - Company master table (company_id)
  - Employee detail tables (company_id, month_date)
  - Industry/sector classification tables

### Data Quality Considerations
1. **Zero-value handling**: Determine if zeros represent true absence or data gaps
2. **Sparse data**: Many company-month-level combinations may have zero employees; consider filtering for performance
3. **Scale**: 10.5 billion rows require careful query optimization (partitioning by month_date recommended)
4. **Aggregation efficiency**: Pre-aggregate where possible; full table scans will be expensive
5. **Date range selection**: Always filter on month_date to limit scan size
6. **Future dates**: Data includes months beyond current date (through 2025-04); clarify whether these are projections or planned data
7. **Level completeness**: Verify if all 10 levels are expected for every company-month combination

### Performance Optimization Strategies
- Use month_date for partition pruning
- Filter out employee_count = 0 if not needed
- Limit company_id sets when possible
- Use approximate aggregation functions (APPROX_COUNT_DISTINCT) for exploratory queries
- Consider materialized views for common aggregation patterns

## Keywords

time-series, employee data, headcount, workforce analytics, organizational hierarchy, company employees, employee count by level, monthly snapshots, job levels, C-suite, directors, managers, entry-level, corporate structure, workforce composition, people analytics, HR analytics, labor data, employment trends, organizational levels, company workforce, employee census, headcount trends, talent analytics, workforce segmentation, org chart data, employee hierarchy, staffing levels, human capital, workforce planning

## Table and Column Documentation

**Table Comment**: Not provided in the analysis report.

**Column Comments**: 
- No column-level comments were provided in the analysis report.