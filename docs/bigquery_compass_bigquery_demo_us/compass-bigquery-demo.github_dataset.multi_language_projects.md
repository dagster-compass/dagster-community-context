---
columns:
- activity_bucket (STRING)
- language_diversity_bucket (STRING)
- license (STRING)
- popularity_bucket (STRING)
- primary_language (STRING)
- primary_language_size_bucket (STRING)
- repo_name (STRING)
- team_size_bucket (STRING)
schema_hash: c2aadb686f159e86814deb0799aad621fe4a3583cbee2e5cc96cab3fe0a011c2

---
# Table Summary: compass-bigquery-demo.github_dataset.multi_language_projects

## Overall Dataset Characteristics

This table contains **1,753,925 GitHub repositories** with comprehensive metadata about multi-language projects. The dataset exhibits:

- **Perfect data quality**: 0% null values across all columns
- **High cardinality in repository names**: Each repository (repo_name) appears to be unique with 1,753,925 distinct values
- **Bucketed/categorical data**: Most columns use predefined buckets or categories for standardized analysis
- **Focus on multi-language projects**: As indicated by the table name and language_diversity_bucket column
- **Skewed distribution patterns**: Sample data suggests most repositories fall into "Minimal" popularity and lower activity categories

## Column Details

### primary_language (STRING)
- **Type**: Categorical text field
- **Cardinality**: 372 unique programming languages
- **Null values**: None (0%)
- **Pattern**: Represents the dominant programming language in each repository
- **Examples**: Ranges from mainstream languages (C, Assembly, Batchfile) to specialized ones (1C Enterprise, AIDL, AMPL)
- **Query consideration**: Excellent for filtering and grouping; useful for language-specific analysis

### primary_language_size_bucket (STRING)
- **Type**: Categorical size classification
- **Categories**: 5 predefined buckets
  - "Tiny (<1K)" - Less than 1,000 bytes
  - "Small (1K-9.9K)" - 1,000 to 9,999 bytes
  - "Medium (10K-99K)" - 10,000 to 99,999 bytes
  - "Large (100K-999K)" - 100,000 to 999,999 bytes
  - "Very Large (1M+)" - 1 million+ bytes
- **Null values**: None (0%)
- **Pattern**: Measures the size of code written in the primary language
- **Query consideration**: Good for filtering projects by code base size; useful for understanding project scale

### language_diversity_bucket (STRING)
- **Type**: Categorical diversity classification
- **Categories**: 5 predefined buckets
  - "Dual (2)" - 2 languages
  - "Multi (3-4)" - 3-4 languages
  - "Mixed (5-9)" - 5-9 languages
  - "Diverse (10-19)" - 10-19 languages
  - "Very Diverse (20+)" - 20 or more languages
- **Null values**: None (0%)
- **Pattern**: Indicates how many different programming languages are used in the repository
- **Distribution**: Sample shows "Multi (3-4)" and "Mixed (5-9)" are common
- **Query consideration**: Key metric for analyzing multi-language project complexity

### repo_name (STRING)
- **Type**: Unique identifier text field
- **Cardinality**: 1,753,925 unique values (100% unique)
- **Null values**: None (0%)
- **Format**: Appears to follow "owner/repository" GitHub convention
- **Examples**: "JoeKarlsson/app-all-o-gizer", "thepcvit/thepcvit.github.io"
- **Query consideration**: Primary key candidate; ideal for JOIN operations and unique record identification

### license (STRING)
- **Type**: Categorical license classification
- **Cardinality**: 15 unique license types
- **Null values**: None (0%)
- **Common values**: "mit", "apache-2.0", "gpl-3.0"
- **All possible values**: agpl-3.0, apache-2.0, artistic-2.0, bsd-2-clause, bsd-3-clause, cc0-1.0, epl-1.0, gpl-2.0, gpl-3.0, isc (and 5 more)
- **Pattern**: Standard open-source license identifiers in SPDX format
- **Query consideration**: Useful for filtering by licensing requirements; good for grouping/aggregation

### popularity_bucket (STRING)
- **Type**: Categorical popularity classification
- **Categories**: 5 predefined buckets (likely based on stars/forks)
  - "Minimal (<10)" - Less than 10 units
  - "Low (10-99)" - 10-99 units
  - "Moderate (100-999)" - 100-999 units
  - "Popular (1K-9.9K)" - 1,000-9,999 units
  - "Very Popular (10K+)" - 10,000+ units
- **Null values**: None (0%)
- **Distribution**: Sample data heavily skewed toward "Minimal (<10)"
- **Query consideration**: Excellent filter for analyzing popular vs. niche projects

### activity_bucket (STRING)
- **Type**: Categorical activity classification
- **Categories**: 5 predefined buckets (likely based on commits/contributions)
  - "Low (10-49)" - 10-49 activities
  - "Low-Medium (50-99)" - 50-99 activities
  - "Medium (100-999)" - 100-999 activities
  - "High (1K-9.9K)" - 1,000-9,999 activities
  - "Very High (10K+)" - 10,000+ activities
- **Null values**: None (0%)
- **Distribution**: Sample shows concentration in lower activity ranges
- **Query consideration**: Useful for identifying active vs. dormant projects

### team_size_bucket (STRING)
- **Type**: Categorical team size classification
- **Categories**: 5 predefined buckets
  - "Individual (1)" - Solo developer
  - "Pair (2-4)" - 2-4 contributors
  - "Small Team (5-19)" - 5-19 contributors
  - "Medium Team (20-99)" - 20-99 contributors
  - "Large Team (100+)" - 100+ contributors
- **Null values**: None (0%)
- **Distribution**: Sample shows mix of Individual, Pair, and Small Team sizes
- **Query consideration**: Good for analyzing collaboration patterns and team dynamics

## Potential Query Considerations

### Ideal Filtering Columns
- **primary_language**: Filter by specific programming languages
- **license**: Filter by licensing requirements
- **popularity_bucket**: Identify popular or trending projects
- **team_size_bucket**: Analyze solo vs. team projects
- **language_diversity_bucket**: Focus on simple vs. complex multi-language projects

### Ideal Grouping/Aggregation Columns
- **primary_language**: Count repositories by language
- **license**: Analyze license distribution
- **popularity_bucket**: Group by popularity tiers
- **activity_bucket**: Segment by activity levels
- All bucket columns work well for aggregation due to predefined categories

### Potential Join Keys
- **repo_name**: Unique identifier, ideal primary key for joining with other GitHub-related tables
- Could join with tables containing repository metrics, contributor data, or commit histories

### Data Quality Considerations
- **No null handling needed**: All columns have 0% null values
- **Bucket boundaries**: When querying, remember that bucket values are strings with embedded ranges (e.g., "Small (1K-9.9K)")
- **Skewed distribution**: Queries should account for heavy concentration in lower-tier buckets (Minimal popularity, Low activity)
- **String comparisons**: All data types are STRING, including numeric bucket classifications
- **Case sensitivity**: Be mindful of exact string matching for license and language values

### Analytical Use Cases
1. **Language popularity analysis**: Cross-reference primary_language with popularity_bucket
2. **Team dynamics**: Correlate team_size_bucket with activity_bucket or language_diversity
3. **License trends**: Analyze which licenses are preferred for different languages or team sizes
4. **Project complexity**: Examine relationships between language_diversity_bucket and project size/activity
5. **Solo vs. team projects**: Compare characteristics of Individual vs. team projects

## Keywords

GitHub, repositories, programming languages, multi-language projects, project metrics, open source, licenses, SPDX, team size, code size, project popularity, project activity, language diversity, software development, code base, contributors, repository analysis, project classification, bucketed data, categorical analysis, MIT license, Apache license, GPL, repo metrics, project scale, collaboration patterns

## Table and Column Docs

**Table Comment**: Not provided

**Column Comments**: Not provided for any columns