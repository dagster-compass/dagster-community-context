---
columns:
- activity_bucket (STRING)
- adoption_level_bucket (STRING)
- license (STRING)
- message_length_bucket (STRING)
- popularity_bucket (STRING)
- project_size_bucket (STRING)
- team_size_bucket (STRING)
schema_hash: 9e14690fd77c715f5a541fe91e99d1d212128c14fe00d8073697a4bf4bd9f1e2

---
# Table Summary: compass-bigquery-demo.github_dataset.license_analysis

## Overall Dataset Characteristics

- **Total Rows**: 15
- **Data Quality**: Excellent - no null values across any columns
- **Dataset Purpose**: Analysis of software licenses with associated project metrics bucketed into categorical ranges
- **Notable Patterns**: 
  - All projects fall into "Low (10-99)" popularity bucket, suggesting this dataset focuses on smaller/niche projects
  - Most projects (majority) have "Very High (10K+)" adoption levels despite low popularity
  - Data appears to be aggregated/summarized with metric buckets rather than raw values

## Column Details

### license (STRING)
- **Data Type**: String identifier for software licenses
- **Null Values**: 0% (complete data)
- **Unique Values**: 15 distinct licenses
- **Key Values**: apache-2.0, gpl-2.0, gpl-3.0, bsd-2-clause, bsd-3-clause, mit, mpl-2.0, agpl-3.0, cc0-1.0, epl-1.0, isc, artistic-2.0
- **Pattern**: Standard SPDX license identifiers (lowercase, hyphenated format)

### popularity_bucket (STRING)
- **Data Type**: Categorical bucket for popularity metrics
- **Null Values**: 0%
- **Unique Values**: 1 (all records have same value)
- **Value**: "Low (10-99)" - all projects fall in this range
- **Pattern**: Consistent low popularity across all licenses in dataset

### adoption_level_bucket (STRING)
- **Data Type**: Categorical bucket for adoption metrics  
- **Null Values**: 0%
- **Unique Values**: 2
- **Values**: "Very High (10K+)", "High (1K-9.9K)"
- **Distribution**: Majority are "Very High (10K+)"

### activity_bucket (STRING)
- **Data Type**: Categorical bucket for project activity
- **Null Values**: 0%
- **Unique Values**: 2
- **Values**: "High (1K-9.9K)", "Medium (100-999)"
- **Distribution**: Mix of High and Medium activity levels

### team_size_bucket (STRING)
- **Data Type**: Categorical bucket for team size
- **Null Values**: 0%
- **Unique Values**: 3
- **Values**: "Large Team (100+)", "Medium Team (20-99)", "Small Team (5-19)"
- **Distribution**: Spans all team size categories

### project_size_bucket (STRING)
- **Data Type**: Categorical bucket for project size
- **Null Values**: 0%
- **Unique Values**: 2
- **Values**: "Medium (1K-9.9K)", "Small (100-999)"
- **Distribution**: Mostly small projects with some medium-sized

### message_length_bucket (STRING)
- **Data Type**: Categorical bucket for commit message length
- **Null Values**: 0%
- **Unique Values**: 2
- **Values**: "Short (50-99)", "Very Short (<50)"
- **Distribution**: Predominantly short commit messages

## Query Considerations

### Good for Filtering:
- **license**: Primary dimension for license-specific analysis
- **adoption_level_bucket**: Filter for high vs very high adoption projects
- **activity_bucket**: Filter by project activity levels
- **team_size_bucket**: Analyze by organizational size
- **project_size_bucket**: Filter by codebase size

### Good for Grouping/Aggregation:
- **license**: Group by license type for comparative analysis
- **team_size_bucket**: Aggregate metrics by team size
- **adoption_level_bucket**: Group by adoption levels
- **activity_bucket**: Aggregate by activity levels

### Potential Relationships:
- **license** as primary key for license characteristics
- Cross-tabulation opportunities between license types and project metrics
- No obvious foreign key relationships (appears to be a summary/analytics table)

### Data Quality Considerations:
- All bucket columns use consistent range notation with parentheses
- No missing data concerns
- Categorical nature means exact values are not available
- Limited variability in popularity_bucket may reduce analytical value for that dimension

## Keywords

license analysis, software licenses, github projects, project metrics, team size, adoption levels, activity buckets, project size, commit messages, open source, SPDX licenses, categorical data, bucketed metrics

## Table and Column Documentation

No table comment or column comments were provided in the source data.