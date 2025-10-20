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
# Table Analysis Summary: compass-bigquery-demo.github_dataset.repo_popularity_metrics

## Overall Dataset Characteristics

- **Total Rows**: 123,312 repositories
- **Data Quality**: Excellent - no null values in any column (0.00% null rate across all fields)
- **Uniqueness**: Each repository has a unique name (123,312 unique repo names)
- **Structure**: Contains categorized metrics for GitHub repositories with all data pre-bucketed into meaningful tiers
- **Coverage**: Comprehensive dataset covering repositories across all popularity and activity levels

## Column Details

### repo_name (STRING)
- **Data Type**: String identifier
- **Null Values**: None (0.00%)
- **Uniqueness**: 123,312 unique values (100% unique - primary identifier)
- **Format**: Standard GitHub repository format (owner/repository-name)
- **Examples**: `andresriancho/race-condition-exploit`, `circuithub/elm-list-extra`

### popularity_tier (STRING)
- **Data Type**: Categorical string with 5 tiers
- **Null Values**: None (0.00%)
- **Categories**: 
  - Minimal (<10)
  - Low (10-99)
  - Moderate (100-999)
  - Popular (1K-9.9K)
  - Very Popular (10K+)
- **Usage**: Represents repository popularity/star count ranges

### team_size_bucket (STRING)
- **Data Type**: Categorical string with 5 buckets
- **Null Values**: None (0.00%)
- **Categories**:
  - Individual (1)
  - Pair (2-4)
  - Small Team (5-19)
  - Medium Team (20-99)
  - Large Team (100+)
- **Usage**: Indicates contributor count ranges

### activity_level_bucket (STRING)
- **Data Type**: Categorical string with 5 levels
- **Null Values**: None (0.00%)
- **Categories**:
  - Low (10-49)
  - Low-Medium (50-99)
  - Medium (100-999)
  - High (1K-9.9K)
  - Very High (10K+)
- **Usage**: Represents repository activity/commit frequency ranges

### project_size_bucket (STRING)
- **Data Type**: Categorical string with 5 sizes
- **Null Values**: None (0.00%)
- **Categories**:
  - Minimal (<10)
  - Tiny (10-99)
  - Small (100-999)
  - Medium (1K-9.9K)
  - Large (10K+)
- **Usage**: Indicates codebase size ranges

### productivity_bucket (STRING)
- **Data Type**: Categorical string with 5 levels
- **Null Values**: None (0.00%)
- **Categories**:
  - Very Low (<10)
  - Low (10-19)
  - Medium (20-49)
  - High (50-99)
  - Very High (100+)
- **Usage**: Represents development productivity metrics

### change_scope_bucket (STRING)
- **Data Type**: Categorical string with 4 levels
- **Null Values**: None (0.00%)
- **Categories**:
  - Very Low (<2)
  - Low (2-4)
  - Medium (5-9)
  - High (10+)
- **Usage**: Indicates scope of changes in commits/PRs

## Query Considerations

### Filtering Columns
- **All categorical columns** are excellent for filtering due to pre-defined, meaningful buckets
- **repo_name** for exact repository lookups
- **popularity_tier** for analyzing repositories by popularity segments
- **team_size_bucket** for team size-based analysis

### Grouping/Aggregation Columns
- **All bucket columns** are ideal for GROUP BY operations
- Common aggregation patterns:
  - Count repositories by popularity tier
  - Analyze productivity across team sizes
  - Cross-tabulate activity levels with project sizes

### Potential Relationships
- **Primary Key**: `repo_name` (unique identifier)
- **Cross-analysis opportunities**: All metrics can be correlated (e.g., team size vs. productivity)
- **No obvious foreign keys** - this appears to be a summary/metrics table

### Data Quality Considerations
- **No data quality issues** - complete dataset with no nulls
- **Pre-bucketed data** means ranges are already defined and consistent
- **Categorical nature** makes data very suitable for analytical queries
- **Ordinal relationships** exist within buckets (e.g., Minimal < Low < Moderate)

## Keywords
GitHub repositories, repository metrics, popularity analysis, team size analysis, project analytics, activity levels, productivity metrics, change scope, repository categorization, software development metrics, open source analysis, repository statistics

## Table and Column Documentation
- **Table Comment**: Not provided
- **Column Comments**: Not provided