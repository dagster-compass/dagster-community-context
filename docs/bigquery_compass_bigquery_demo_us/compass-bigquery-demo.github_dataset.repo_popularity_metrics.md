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
- **Data Quality**: Excellent - no null values in any column (0% null rate across all fields)
- **Structure**: Categorical/bucketed metrics table with predefined ranges for each dimension
- **Coverage**: Complete dataset with unique repository names (123,312 unique values = 100% uniqueness)
- **Distribution Pattern**: Hierarchical bucketing system using consistent range patterns across metrics

## Column Details

### repo_name (STRING)
- **Type**: Primary identifier, fully unique
- **Null Values**: None (0.00%)
- **Uniqueness**: 123,312 unique values (100% unique)
- **Format**: Follows GitHub repository naming convention (owner/repository-name)
- **Sample Pattern**: "zeekay/flask-uwsgi-websocket", "php-ddd/domain-driven-design"

### popularity_tier (STRING)
- **Type**: Categorical bucket for repository popularity
- **Null Values**: None (0.00%)
- **Categories**: 5 tiers in ascending order
  - Minimal (<10)
  - Low (10-99)
  - Moderate (100-999)
  - Popular (1K-9.9K)
  - Very Popular (10K+)
- **Pattern**: Logarithmic scaling with clear numeric thresholds

### activity_level_bucket (STRING)
- **Type**: Categorical bucket for repository activity
- **Null Values**: None (0.00%)
- **Categories**: 5 levels in ascending order
  - Low (10-49)
  - Low-Medium (50-99)
  - Medium (100-999)
  - High (1K-9.9K)
  - Very High (10K+)
- **Pattern**: Similar logarithmic scaling to popularity_tier

### team_size_bucket (STRING)
- **Type**: Categorical bucket for development team size
- **Null Values**: None (0.00%)
- **Categories**: 5 sizes in ascending order
  - Individual (1)
  - Pair (2-4)
  - Small Team (5-19)
  - Medium Team (20-99)
  - Large Team (100+)
- **Pattern**: Exponential growth ranges for team scaling

### project_size_bucket (STRING)
- **Type**: Categorical bucket for project codebase size
- **Null Values**: None (0.00%)
- **Categories**: 5 sizes in ascending order
  - Minimal (<10)
  - Tiny (10-99)
  - Small (100-999)
  - Medium (1K-9.9K)
  - Large (10K+)
- **Pattern**: Logarithmic scaling similar to popularity metrics

### productivity_bucket (STRING)
- **Type**: Categorical bucket for development productivity
- **Null Values**: None (0.00%)
- **Categories**: 5 levels in ascending order
  - Very Low (<10)
  - Low (10-19)
  - Medium (20-49)
  - High (50-99)
  - Very High (100+)
- **Pattern**: Graduated linear-to-exponential scaling

### change_scope_bucket (STRING)
- **Type**: Categorical bucket for scope of changes
- **Null Values**: None (0.00%)
- **Categories**: 4 levels in ascending order
  - Very Low (<2)
  - Low (2-4)
  - Medium (5-9)
  - High (10+)
- **Pattern**: Smallest range system, focuses on low-to-medium change scope

## Potential Query Considerations

### Excellent for Filtering
- **All categorical columns**: Perfect for WHERE clauses with exact matches
- **repo_name**: Ideal for specific repository lookups
- **Tier-based filtering**: Easy to filter by specific performance levels

### Excellent for Grouping/Aggregation
- **All bucket columns**: Pre-categorized for GROUP BY operations
- **Cross-dimensional analysis**: Compare distributions across different metrics
- **Tier analysis**: Count repositories by performance tiers

### Key Relationships
- **No explicit foreign keys**: Self-contained table
- **Potential correlations**: Between popularity, activity, team size, and productivity
- **Repository identifier**: repo_name could join with other GitHub dataset tables

### Data Quality Considerations
- **Consistent bucketing**: All categories use clear, non-overlapping ranges
- **No missing data**: 100% complete dataset requires no null handling
- **Standardized format**: Categorical values are consistent and predictable
- **Scalable ranges**: Logarithmic scaling accommodates wide value distributions

## Keywords

GitHub repositories, repository metrics, popularity analysis, development team analysis, project size analysis, productivity metrics, activity levels, categorical data, bucketed metrics, repository analytics, software development metrics, GitHub dataset, repository statistics, development activity, team productivity, project scope, repository popularity, GitHub analytics

## Table and Column Documentation

**Table Comment**: Not provided

**Column Comments**: Not provided