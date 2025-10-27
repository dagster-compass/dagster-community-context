---
columns:
- activity_level_bucket (STRING)
- change_scope_bucket (STRING)
- popularity_tier (STRING)
- productivity_bucket (STRING)
- project_size_bucket (STRING)
- repo_name (STRING)
- team_size_bucket (STRING)
schema_hash: bb7477a10c09930493371c66241dc4c5f6befcd6494d133ded1747cdbc92e464

---
# Table Summary: compass-bigquery-demo.github_dataset.repo_popularity_metrics

## Overall Dataset Characteristics

- **Total Rows**: 123,312 repositories
- **Data Quality**: Excellent - 0% null values across all columns
- **Primary Characteristic**: GitHub repository metrics dataset with categorical bucketing of various repository attributes
- **Data Structure**: Each row represents a unique GitHub repository with associated popularity and activity metrics
- **Table Comment**: Not provided

## Column Details

### repo_name (STRING)
- **Data Type**: String identifier
- **Uniqueness**: 100% unique (123,312 distinct values)
- **Format**: GitHub repository naming convention (owner/repository-name)
- **Null Values**: None (0.00%)
- **Usage**: Primary identifier for repositories
- **Column Comment**: Not provided

### popularity_tier (STRING)
- **Data Type**: Categorical string with 5 tiers
- **Null Values**: None (0.00%)
- **Categories**: 
  - Minimal (<10)
  - Low (10-99)
  - Moderate (100-999)
  - Popular (1K-9.9K)
  - Very Popular (10K+)
- **Usage**: Repository popularity classification based on metrics like stars/forks
- **Column Comment**: Not provided

### activity_level_bucket (STRING)
- **Data Type**: Categorical string with 5 activity levels
- **Null Values**: None (0.00%)
- **Categories**:
  - Low (10-49)
  - Low-Medium (50-99)
  - Medium (100-999)
  - High (1K-9.9K)
  - Very High (10K+)
- **Usage**: Repository activity classification based on commits/contributions
- **Column Comment**: Not provided

### team_size_bucket (STRING)
- **Data Type**: Categorical string with 5 team size categories
- **Null Values**: None (0.00%)
- **Categories**:
  - Individual (1)
  - Pair (2-4)
  - Small Team (5-19)
  - Medium Team (20-99)
  - Large Team (100+)
- **Usage**: Classification of contributor count ranges
- **Column Comment**: Not provided

### productivity_bucket (STRING)
- **Data Type**: Categorical string with 5 productivity levels
- **Null Values**: None (0.00%)
- **Categories**:
  - Very Low (<10)
  - Low (10-19)
  - Medium (20-49)
  - High (50-99)
  - Very High (100+)
- **Usage**: Repository productivity/output measurement classification
- **Column Comment**: Not provided

### project_size_bucket (STRING)
- **Data Type**: Categorical string with 5 size categories
- **Null Values**: None (0.00%)
- **Categories**:
  - Minimal (<10)
  - Tiny (10-99)
  - Small (100-999)
  - Medium (1K-9.9K)
  - Large (10K+)
- **Usage**: Project size classification (likely based on lines of code or files)
- **Column Comment**: Not provided

### change_scope_bucket (STRING)
- **Data Type**: Categorical string with 4 scope levels
- **Null Values**: None (0.00%)
- **Categories**:
  - Very Low (<2)
  - Low (2-4)
  - Medium (5-9)
  - High (10+)
- **Usage**: Classification of change scope (possibly files changed per commit)
- **Column Comment**: Not provided

## Potential Query Considerations

### Filtering Columns
- **repo_name**: Exact repository lookups or pattern matching
- **popularity_tier**: Filter by popularity levels for trend analysis
- **team_size_bucket**: Analyze repositories by team structure
- **All bucket columns**: Excellent for filtering by specific ranges or categories

### Grouping/Aggregation Columns
- **All bucket columns**: Perfect for GROUP BY operations to analyze distributions
- **Cross-tabulations**: Combine multiple buckets (e.g., popularity vs. team size)
- **Statistical analysis**: Count repositories in each category combination

### Join Considerations
- **repo_name**: Primary key for joining with other GitHub datasets
- **No apparent foreign keys**: This appears to be a metrics summary table

### Data Quality Considerations
- **Excellent data quality**: No null values to handle
- **Consistent categorization**: All buckets use clear, non-overlapping ranges
- **Ordinal nature**: Most buckets have natural ordering (Low → High)
- **String comparisons**: Be aware that bucket comparisons require understanding of the hierarchy

## Keywords

GitHub, repositories, popularity metrics, activity levels, team size, productivity, project size, change scope, categorical data, bucketing, repository analysis, software development metrics, commit analysis, contributor metrics, open source projects

## Table and Column Documentation

**Table Comment**: Not provided

**Column Comments**: Not provided for any columns