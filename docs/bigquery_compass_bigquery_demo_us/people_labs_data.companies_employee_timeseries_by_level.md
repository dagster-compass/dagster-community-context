---
columns:
- company_id (STRING)
- employee_count (INT64)
- level (STRING)
- month_date (STRING)
schema_hash: a4a68bd81a642b890c2263843fc594c3f207689ec7e49ebbdc4834e6f89e20d9

---
# Table Summary: companies_employee_timeseries_by_level

## Overall Dataset Characteristics

- **Total Rows**: 10,466,558,360 (over 10 billion records)
- **Data Quality**: Excellent - 0% null values across all columns
- **Time Range**: January 2010 to March 2025+ (188 unique months, ~15.7 years)
- **Scope**: Time-series tracking of employee counts by organizational level across ~16 million companies
- **Granularity**: Monthly snapshots per company per organizational level

### Notable Patterns
- High volume of zero-count records (indicating companies with no employees at certain levels in certain months)
- Wide range of employee counts (0 to 120,165) suggesting dataset includes both small businesses and large enterprises
- Data appears to include future projections (dates extend to 2025-07 based on samples)

## Column Details

### month_date (STRING)
- **Format**: YYYY-MM (year-month string format)
- **Temporal Coverage**: 188 unique months spanning 2010-01 to 2025+ 
- **Data Quality**: Complete (0% nulls)
- **Usage Pattern**: Time-series dimension, appears to be the primary temporal index
- **Query Consideration**: Should be converted to DATE type or parsed for temporal operations

### level (STRING)
- **Type**: Categorical with 10 distinct organizational levels
- **Values**: 
  - Executive: `cxo`, `vp`, `director`
  - Management: `manager`, `senior`
  - Ownership: `owner`, `partner`
  - Early Career: `entry`, `training`
  - Special: `unpaid`
- **Data Quality**: Complete (0% nulls), standardized values
- **Distribution**: Well-distributed across organizational hierarchy
- **Query Consideration**: Ideal for grouping and filtering; consider hierarchical aggregations

### employee_count (INT64)
- **Range**: 0 to 120,165 employees
- **Unique Values**: 26,016 distinct counts
- **Data Quality**: Complete (0% nulls), all non-negative integers
- **Distribution**: Heavily skewed toward lower counts (many 0s and small values)
- **Notable**: Maximum of 120K+ suggests large enterprise coverage
- **Query Consideration**: Primary metric for aggregation (SUM, AVG, MAX, etc.); zero values may need filtering depending on analysis purpose

### company_id (STRING)
- **Type**: Alphanumeric identifier (appears to be hash-based)
- **Cardinality**: 16,020,211 unique companies
- **Format**: 28-character alphanumeric strings (e.g., "TgGqHAZKUoRSNm5rmBCHnwMNHdCf")
- **Data Quality**: Complete (0% nulls), consistent format
- **Query Consideration**: Primary entity key; essential for company-level analysis and joins

## Query Considerations

### Ideal for Filtering:
- **month_date**: Time-based filtering (e.g., specific years, quarters, recent months)
- **level**: Organizational level analysis (e.g., executive trends, entry-level hiring)
- **employee_count**: Size-based filtering (e.g., exclude zeros, focus on companies with >N employees)
- **company_id**: Company-specific lookups

### Ideal for Grouping/Aggregation:
- **month_date**: Time-series analysis, trend identification, YoY/MoM comparisons
- **level**: Cross-level comparisons, organizational structure analysis
- **company_id**: Per-company aggregations, company growth trajectories

### Join Keys:
- **company_id**: Primary join key for linking to company master tables, industry data, location data, etc.
- **month_date**: Temporal joins with economic indicators, market data, or other time-series datasets

### Data Quality Considerations:
1. **Zero Counts**: Many records have employee_count=0, which may indicate:
   - Companies with no employees at that level
   - Data gaps or missing information
   - Consider filtering strategy based on analysis needs

2. **Future Dates**: Data extends beyond current date (2025-07 in samples), suggesting:
   - Projections or forecasts
   - Data ingestion timing considerations
   - May need current-date filtering for historical analysis

3. **Scale**: 10+ billion rows requires:
   - Partition-aware queries (likely partitioned by month_date)
   - Selective filtering before aggregation
   - Careful consideration of query costs and performance

4. **Time-Series Completeness**: With 10 levels × 16M companies × 188 months, theoretical maximum is ~30B rows; actual 10B suggests:
   - Not all companies tracked for all months
   - Sparse matrix structure
   - Companies may appear/disappear over time

## Keywords
employee headcount, workforce analytics, time-series data, organizational hierarchy, company growth, employment levels, CXO executives, management levels, monthly snapshots, people data, labor market, company staffing, workforce composition, employee tracking, organizational structure, business intelligence, HR analytics, talent analytics, corporate hierarchy, employee segments, workforce trends, hiring patterns, company size, employment history, organizational levels

## Table and Column Documentation

**Table Comment**: Not provided

**Column Comments**: 
- `month_date`: Not provided
- `level`: Not provided  
- `employee_count`: Not provided
- `company_id`: Not provided