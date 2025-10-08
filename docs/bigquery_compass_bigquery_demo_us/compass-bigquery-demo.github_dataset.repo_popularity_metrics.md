---
columns:
- activity_level_bucket (STRING)
- change_scope_bucket (STRING)
- popularity_tier (STRING)
- productivity_bucket (STRING)
- project_size_bucket (STRING)
- repo_id (STRING)
- team_size_bucket (STRING)
schema_hash: 01ae4b1aa11687c4319fa55114d74f1555837549c33ab12fc084fa2aea7aa46f

---
# Dataset Summary: compass-bigquery-demo.github_dataset.repo_popularity_metrics

## Overall Dataset Characteristics

- **Total Rows**: 123,312 repositories
- **Data Quality**: Excellent - no null values across any columns
- **Structure**: Each row represents a unique repository with categorized metrics
- **Pattern**: Repository metrics are pre-bucketed into ordinal categories (Very Low to Very High)
- **Uniqueness**: Each repository has a unique hashed identifier (repo_id)

## Column Details

### repo_id (STRING)
- **Type**: Unique identifier (appears to be SHA-256 hash)
- **Characteristics**: 64-character hexadecimal strings, 100% unique
- **Usage**: Primary key for repository identification
- **Pattern**: Cryptographic hash format (no nulls, all unique)

### popularity_tier (STRING)
- **Type**: Ordinal categorical with 5 levels
- **Categories**: Minimal (<10) → Low (10-99) → Moderate (100-999) → Popular (1K-9.9K) → Very Popular (10K+)
- **Pattern**: Likely based on stars, forks, or similar popularity metrics
- **Distribution**: Sample data shows concentration in lower tiers (Minimal, Low)

### activity_level_bucket (STRING)
- **Type**: Ordinal categorical with 5 levels  
- **Categories**: Low (10-49) → Low-Medium (50-99) → Medium (100-999) → High (1K-9.9K) → Very High (10K+)
- **Pattern**: Likely measures commits, issues, or overall repository activity
- **Distribution**: Medium activity level appears common in samples

### team_size_bucket (STRING)
- **Type**: Ordinal categorical with 5 levels
- **Categories**: Individual (1) → Pair (2-4) → Small Team (5-19) → Medium Team (20-99) → Large Team (100+)
- **Pattern**: Based on number of contributors
- **Distribution**: Small teams and pairs appear most common

### project_size_bucket (STRING)
- **Type**: Ordinal categorical with 5 levels
- **Categories**: Minimal (<10) → Tiny (10-99) → Small (100-999) → Medium (1K-9.9K) → Large (10K+)
- **Pattern**: Likely based on lines of code, files, or repository size
- **Distribution**: Wide range from minimal to medium sizes in samples

### productivity_bucket (STRING)
- **Type**: Ordinal categorical with 5 levels
- **Categories**: Very Low (<10) → Low (10-19) → Medium (20-49) → High (50-99) → Very High (100+)
- **Pattern**: Likely productivity metrics (commits per contributor, etc.)
- **Distribution**: Various levels represented in sample data

### change_scope_bucket (STRING)
- **Type**: Ordinal categorical with 4 levels
- **Categories**: Very Low (<2) → Low (2-4) → Medium (5-9) → High (10+)
- **Pattern**: Possibly measures files changed per commit or scope of changes
- **Distribution**: Heavily skewed toward "Very Low" in sample data

## Query Considerations

### Excellent for Filtering
- **popularity_tier**: Filter by popularity levels for market analysis
- **team_size_bucket**: Analyze by team structure
- **activity_level_bucket**: Find active vs. inactive repositories
- All categorical columns support range filtering due to ordinal nature

### Ideal for Grouping/Aggregation
- All bucketed columns are perfect for GROUP BY operations
- Cross-tabulation analysis between any combination of metrics
- Distribution analysis across popularity, activity, and team characteristics
- Cohort analysis by combining multiple dimensions

### Analytical Opportunities
- **Correlation Analysis**: Examine relationships between team size, productivity, and popularity
- **Segmentation**: Create repository archetypes based on multiple dimensions
- **Trend Analysis**: Compare distributions across different metric combinations
- **Performance Benchmarking**: Identify high-performing repository characteristics

### Data Quality Considerations
- No missing data concerns (0% nulls across all columns)
- Consistent categorical formatting with clear value ranges
- Pre-aggregated nature means no need for complex calculations
- Ordinal categories support both equality and range queries

## Keywords

repository metrics, GitHub analytics, software development, team productivity, project popularity, repository categorization, development team analysis, software project metrics, repository classification, GitHub repositories, developer productivity, project activity, team collaboration, software engineering metrics

## Table and Column Documentation

*No table comment or column comments were provided in the source analysis.*