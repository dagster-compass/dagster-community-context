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
# Table Summary: compass-bigquery-demo.github_dataset.repo_popularity_metrics

## Overall Dataset Characteristics

- **Total Rows**: 123,312 repositories
- **Data Quality**: Excellent - no null values in any columns, complete dataset
- **Pattern**: Each row represents a unique repository with categorized metrics across multiple dimensions
- **Distribution**: The dataset appears to focus heavily on smaller repositories, with "Minimal" and "Low" popularity tiers being most common, and "Very Low" change scope being predominant

## Column Details

### repo_id (STRING)
- **Type**: Unique identifier (appears to be SHA-256 hash)
- **Format**: 64-character hexadecimal string
- **Uniqueness**: 100% unique (123,312 distinct values)
- **Usage**: Primary key for repository identification

### popularity_tier (STRING)
- **Type**: Categorical ranking based on repository popularity metrics
- **Categories**: 5 tiers from "Minimal (<10)" to "Very Popular (10K+)"
- **Distribution**: Heavily skewed toward lower popularity tiers
- **Common Values**: "Minimal (<10)" and "Low (10-99)" appear most frequently

### activity_level_bucket (STRING)
- **Type**: Categorical ranking of repository activity
- **Categories**: 5 levels from "Low (10-49)" to "Very High (10K+)"
- **Pattern**: Most repositories fall in lower activity ranges
- **Common Values**: "Low (10-49)" and "Low-Medium (50-99)" are prevalent

### team_size_bucket (STRING)
- **Type**: Categorical grouping by number of contributors
- **Categories**: 5 sizes from "Individual (1)" to "Large Team (100+)"
- **Distribution**: Mix of individual, pair, and small team projects
- **Common Values**: "Pair (2-4)", "Small Team (5-19)", and "Medium Team (20-99)"

### project_size_bucket (STRING)
- **Type**: Categorical classification by codebase size
- **Categories**: 5 sizes from "Minimal (<10)" to "Large (10K+)"
- **Pattern**: Most projects are small-scale
- **Common Values**: "Tiny (10-99)" and "Minimal (<10)" dominate

### productivity_bucket (STRING)
- **Type**: Categorical measure of development productivity
- **Categories**: 5 levels from "Very Low (<10)" to "Very High (100+)"
- **Distribution**: Ranges across all levels with emphasis on lower-medium productivity
- **Common Values**: "Very Low (<10)" and "Medium (20-49)" appear frequently

### change_scope_bucket (STRING)
- **Type**: Categorical measure of change complexity/scope
- **Categories**: 4 levels from "Very Low (<2)" to "High (10+)"
- **Pattern**: Heavily skewed toward minimal changes
- **Dominant Value**: "Very Low (<2)" appears to be the most common by far

## Query Considerations

### Ideal for Filtering
- All categorical columns are excellent for WHERE clause filtering
- `popularity_tier` and `activity_level_bucket` for performance-based filtering
- `team_size_bucket` for organizational analysis
- `project_size_bucket` for scale-based queries

### Ideal for Grouping/Aggregation
- All bucket columns provide natural grouping dimensions
- Cross-dimensional analysis possible (e.g., popularity vs team size)
- Suitable for COUNT(), distribution analysis, and correlation studies

### Potential Relationships
- `repo_id` serves as a foreign key for joining with other repository tables
- Strong potential correlations between metrics (e.g., team size vs activity level)
- Natural hierarchical groupings within each bucket category

### Data Quality Considerations
- No missing data handling required
- All values follow consistent categorical patterns
- Bucket ranges are clearly defined and non-overlapping
- Hash-based repo_id ensures privacy while maintaining uniqueness

## Keywords

GitHub, repository, metrics, popularity, activity, team size, project size, productivity, change scope, analytics, software development, open source, repository analysis, development metrics, collaboration, code metrics

## Table and Column Documentation

No table comments or column comments were provided in the analysis report.