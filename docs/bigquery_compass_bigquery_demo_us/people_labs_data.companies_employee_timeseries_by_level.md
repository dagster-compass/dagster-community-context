---
columns:
- company_id (STRING)
- employee_count (INT64)
- level (STRING)
- month_date (STRING)
schema_hash: a4a68bd81a642b890c2263843fc594c3f207689ec7e49ebbdc4834e6f89e20d9

---
# Summary: people_labs_data.companies_employee_timeseries_by_level

## Overall Dataset Characteristics

- **Total Rows**: 10,466,558,360 (over 10 billion records)
- **Data Quality**: Excellent - 0% null values across all columns
- **Time Range**: Monthly data from 2010-01 through 2024+ (188 unique months, ~15.7 years)
- **Scope**: Employee count tracking by organizational level across 16+ million companies
- **Notable Patterns**: 
  - Many records show 0 employee counts, suggesting comprehensive tracking including periods of no employees at certain levels
  - Employee counts range from 0 to 120,165, indicating coverage of companies from startups to large enterprises
  - Data appears to be a comprehensive time series for workforce analytics

## Column Details

### level (STRING)
- **Data Type**: Categorical string with 10 distinct organizational levels
- **Null Values**: 0% (complete data)
- **Values**: `cxo`, `director`, `entry`, `manager`, `owner`, `partner`, `senior`, `training`, `unpaid`, `vp`
- **Pattern**: Represents hierarchical organizational structure from entry-level to C-suite

### company_id (STRING)
- **Data Type**: Alphanumeric identifier string
- **Null Values**: 0% (complete data)
- **Unique Values**: 16,020,211 companies
- **Format**: 28-character alphanumeric strings (e.g., "0001FB6m8lpCOvqlHQLq9gdUhMF4")
- **Pattern**: Appears to be encoded/hashed company identifiers for privacy

### month_date (STRING)
- **Data Type**: Date string in YYYY-MM format
- **Null Values**: 0% (complete data)
- **Range**: 188 unique months spanning ~15.7 years
- **Format**: Consistent "YYYY-MM" pattern (e.g., "2010-01", "2024-04")
- **Pattern**: Monthly time series data for longitudinal analysis

### employee_count (INT64)
- **Data Type**: Integer count
- **Null Values**: 0% (complete data)
- **Range**: 0 to 120,165 employees
- **Distribution**: Many zero values indicate tracking of all level/company/month combinations
- **Pattern**: Actual headcount at each organizational level per company per month

## Potential Query Considerations

### Filtering Opportunities
- **Time-based filtering**: `month_date` for specific periods, quarters, or years
- **Level filtering**: `level` for specific organizational tiers (e.g., leadership vs. individual contributors)
- **Size filtering**: `employee_count` for company size categories or growth analysis
- **Company filtering**: `company_id` for specific company analysis

### Grouping/Aggregation Opportunities
- **Temporal aggregation**: Group by `month_date` for time series analysis
- **Organizational analysis**: Group by `level` for workforce composition analysis
- **Company segmentation**: Group by `company_id` for individual company trends
- **Cross-dimensional**: Combine groupings for complex workforce analytics

### Potential Relationships
- **Primary composite key**: Likely (`company_id`, `month_date`, `level`)
- **Time series key**: `company_id` + `month_date` for company evolution
- **Level analysis key**: `level` + `month_date` for industry-wide level trends
- **External joins**: `company_id` could join to company metadata tables

### Data Quality Considerations
- **Zero counts**: Many legitimate zero values - filter appropriately for meaningful analysis
- **Date consistency**: Month-end snapshots - consider date arithmetic for period calculations
- **Scale considerations**: 10+ billion rows require efficient query strategies and appropriate sampling
- **Level completeness**: All 10 levels may not be present for every company/month combination

## Keywords
employee timeseries, workforce analytics, organizational levels, company headcount, employment data, time series analysis, corporate structure, staffing levels, CXO directors managers, employee tracking, monthly snapshots, organizational hierarchy, workforce composition

## Table and Column Documentation
*No table comment or column comments were provided in the source analysis.*