---
columns:
- activity_bucket (STRING)
- adoption_level_bucket (STRING)
- diversity_bucket (STRING)
- license (STRING)
- license_share_bucket (STRING)
- popularity_bucket (STRING)
- primary_language (STRING)
- team_size_bucket (STRING)
schema_hash: bf4a477045a44380b9aad17fb9704f18c0cb62fcc40daa98f11a37894927e341

---
# Table Summary: compass-bigquery-demo.github_dataset.license_language_correlation

## Overall Dataset Characteristics

- **Total Rows**: 1,502
- **Data Quality**: Excellent - no null values in any columns (0.00% null percentage across all fields)
- **Dataset Nature**: This appears to be an analysis table correlating programming languages with open source licenses and various project metrics
- **Distribution Pattern**: The data represents categorized/bucketed metrics rather than raw values, suggesting this is an analytical summary table

## Column Details

### primary_language (STRING)
- **Data Type**: String
- **Null Values**: None (0.00%)
- **Unique Values**: 259 distinct programming languages
- **Sample Values**: AutoHotkey, C, Vim script, Shell, Tcl, LabVIEW, PLpgSQL, ASP
- **Characteristics**: Wide variety of programming languages from mainstream (C) to specialized (LabVIEW, AutoHotkey)

### popularity_bucket (STRING)
- **Data Type**: String (categorical)
- **Null Values**: None (0.00%)
- **Unique Values**: 4 categories
- **Categories**: 
  - Minimal (<10)
  - Low (10-99)
  - Moderate (100-999)
  - Popular (1K-9.9K)
- **Pattern**: Hierarchical popularity classification system

### license (STRING)
- **Data Type**: String
- **Null Values**: None (0.00%)
- **Unique Values**: 15 distinct licenses
- **Sample Values**: MIT, GPL-2.0, GPL-3.0, ISC, BSD-2-clause, CC0-1.0
- **Characteristics**: Common open source licenses, with MIT appearing frequently in samples

### adoption_level_bucket (STRING)
- **Data Type**: String (categorical)
- **Null Values**: None (0.00%)
- **Unique Values**: 5 categories
- **Categories**:
  - Low (10-49)
  - Low-Medium (50-99)
  - Medium (100-999)
  - High (1K-9.9K)
  - Very High (10K+)
- **Pattern**: Progressive adoption scale

### team_size_bucket (STRING)
- **Data Type**: String (categorical)
- **Null Values**: None (0.00%)
- **Unique Values**: 5 categories
- **Categories**:
  - Individual (1)
  - Pair (2-4)
  - Small Team (5-19)
  - Medium Team (20-99)
  - Large Team (100+)
- **Pattern**: "Pair (2-4)" appears very frequently in samples

### license_share_bucket (STRING)
- **Data Type**: String (categorical)
- **Null Values**: None (0.00%)
- **Unique Values**: 4 categories
- **Categories**:
  - Minimal (<5%)
  - Trace (5-9%)
  - Minor (10-24%)
  - Major (25-49%)
- **Pattern**: "Minimal (<5%)" appears most frequently in samples

### activity_bucket (STRING)
- **Data Type**: String (categorical)
- **Null Values**: None (0.00%)
- **Unique Values**: 5 categories
- **Categories**:
  - Low (<50)
  - Low-Medium (50-99)
  - Medium (100-999)
  - High (1K-9.9K)
  - Very High (10K+)
- **Pattern**: Similar scale to adoption_level_bucket

### diversity_bucket (STRING)
- **Data Type**: String (categorical)
- **Null Values**: None (0.00%)
- **Unique Values**: 5 categories
- **Categories**:
  - Single (1)
  - Dual (2)
  - Mixed (3-4)
  - Diverse (5-9)
  - Very Diverse (10+)
- **Pattern**: Lower diversity levels (Single, Dual) appear frequently

## Potential Query Considerations

### Good for Filtering:
- **license**: Filter by specific open source licenses (MIT, GPL, Apache, etc.)
- **primary_language**: Filter by programming language
- **popularity_bucket**: Filter by project popularity tiers
- All bucket columns for range-based filtering

### Good for Grouping/Aggregation:
- **license**: Group by license type for license adoption analysis
- **primary_language**: Group by language for language-specific insights
- **popularity_bucket**, **adoption_level_bucket**, **activity_bucket**: Excellent for trend analysis across different scales
- **team_size_bucket**: Analyze patterns by team size

### Potential Relationships:
- **primary_language + license**: Core relationship for language-license correlations
- **popularity_bucket + license**: Understand which licenses are used by popular projects
- **team_size_bucket + diversity_bucket**: Analyze team composition patterns
- Cross-bucket analysis (popularity vs adoption vs activity) for comprehensive project profiling

### Data Quality Considerations:
- All data is clean with no null values
- Categorical data is well-structured and consistent
- Bucket ranges are clearly defined and non-overlapping
- Sample data suggests possible skew toward smaller projects/teams

## Keywords
GitHub, open source licenses, programming languages, project metrics, software development, license adoption, team size analysis, project popularity, software diversity, repository analysis, MIT license, GPL license, Apache license, development activity

## Table and Column Docs
No table comment or column comments were provided in the source analysis.