---
columns:
- company_id (STRING)
- employee_count (INT64)
- level (STRING)
- month_date (STRING)
schema_hash: a4a68bd81a642b890c2263843fc594c3f207689ec7e49ebbdc4834e6f89e20d9

---
# Table Analysis Summary: people_labs_data.companies_employee_timeseries_by_level

## Overall Dataset Characteristics

This is a large-scale employee timeseries dataset containing **10,466,558,360 rows** that tracks employee counts by company and organizational level over time. The dataset spans from 2010 to 2023 (188 months) and covers over 16 million unique companies. The data appears to be of high quality with no null values across any columns.

**Notable Patterns:**
- Comprehensive temporal coverage spanning 13+ years of monthly data
- Hierarchical organizational structure captured through 10 distinct employee levels
- Many zero employee counts, suggesting the dataset tracks both active and inactive periods for companies
- Wide range of company sizes (0 to 120,165 employees at a single level)

## Column Details

### company_id (STRING)
- **Type**: Unique company identifier (alphanumeric hash)
- **Completeness**: 100% (no nulls)
- **Cardinality**: 16,020,211 unique companies
- **Format**: 32-character alphanumeric strings (e.g., "zwdtcmq5ANbc9hW7hW4cGgNxJYuy")
- **Usage**: Primary entity identifier for filtering and grouping

### month_date (STRING)
- **Type**: Temporal dimension in YYYY-MM format
- **Completeness**: 100% (no nulls)
- **Range**: 188 unique months from 2010-01 to 2023+ 
- **Format**: Consistent "YYYY-MM" string format
- **Usage**: Time-based filtering, trending, and temporal aggregations

### level (STRING)
- **Type**: Categorical organizational hierarchy
- **Completeness**: 100% (no nulls)
- **Values**: 10 distinct levels
  - `cxo` - C-suite executives
  - `director` - Director level
  - `entry` - Entry level positions
  - `manager` - Management level
  - `owner` - Company owners
  - `partner` - Partnership level
  - `senior` - Senior level roles
  - `training` - Training/internship positions
  - `unpaid` - Unpaid positions
  - `vp` - Vice President level
- **Usage**: Hierarchical analysis and organizational structure queries

### employee_count (INT64)
- **Type**: Numeric count of employees
- **Completeness**: 100% (no nulls)
- **Range**: 0 to 120,165 employees
- **Distribution**: High frequency of zero values, suggesting many inactive periods
- **Usage**: Aggregation target for workforce analytics

## Potential Query Considerations

### Excellent for Filtering:
- **company_id**: Direct company lookups and multi-company comparisons
- **month_date**: Time-range filtering (quarters, years, specific periods)
- **level**: Organizational analysis by hierarchy level
- **employee_count**: Size-based filtering (small vs large organizations)

### Excellent for Grouping/Aggregation:
- **month_date**: Temporal trending and seasonality analysis
- **level**: Organizational structure distribution analysis  
- **company_id**: Company-specific workforce evolution
- **employee_count**: Workforce size distributions and growth patterns

### Potential Join Keys:
- **company_id**: Primary key for joining with other company-related tables
- **month_date**: Temporal joins with other time-series datasets

### Data Quality Considerations:
- **Zero Values**: High frequency of zero employee counts should be considered in analyses
- **Date Format**: String format may require conversion for advanced temporal operations
- **Scale**: Massive dataset size requires careful query optimization and potentially sampling for exploratory analysis
- **Completeness**: Excellent data quality with no missing values across all dimensions

## Keywords

employee timeseries, workforce analytics, organizational hierarchy, company staffing, employee levels, temporal data, CXO executives, management structure, workforce trends, company growth, employee counts by level, organizational analysis, time series analysis, corporate hierarchy, staffing patterns

## Table and Column Documentation

**Table Comment**: Not provided

**Column Comments**: Not provided