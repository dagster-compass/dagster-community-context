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
# Comprehensive Summary: compass-bigquery-demo.github_dataset.license_language_correlation

## Overall Dataset Characteristics

- **Total Rows**: 1,502 records
- **Data Quality**: Excellent - No null values present in any column (0% null percentage across all fields)
- **Dataset Purpose**: This table appears to correlate open-source software licenses with programming languages and various project metrics, creating a multi-dimensional view of GitHub repository characteristics
- **Data Completeness**: 100% complete dataset with categorical bucketed metrics
- **Notable Pattern**: All data is pre-categorized into meaningful buckets/ranges rather than raw numerical values, making it optimized for aggregation and analysis

## Column Details

### 1. **license** (STRING)
- **Data Type**: Categorical string
- **Null Values**: None (0%)
- **Cardinality**: 15 unique license types
- **Values Include**: agpl-3.0, apache-2.0, artistic-2.0, bsd-2-clause, bsd-3-clause, cc0-1.0, epl-1.0, gpl-2.0, gpl-3.0, isc, mit, unlicense, and others
- **Distribution**: Includes major open-source licenses commonly used in software projects
- **Usage Notes**: Primary dimension for license-based analysis; "mit" and "apache-2.0" appear frequently in samples

### 2. **primary_language** (STRING)
- **Data Type**: Categorical string
- **Null Values**: None (0%)
- **Cardinality**: 259 unique programming languages
- **Values Include**: Swift, Groff, Puppet, Arduino, IDL, Smarty, Tcl, Assembly, and 251+ others
- **Distribution**: High diversity indicating comprehensive coverage of programming ecosystems
- **Usage Notes**: Includes both mainstream (Swift, Assembly) and niche languages (Groff, Smarty, IDL)

### 3. **adoption_level_bucket** (STRING)
- **Data Type**: Categorical string (ordinal)
- **Null Values**: None (0%)
- **Cardinality**: 5 distinct buckets
- **Categories** (ascending order):
  - "Low (10-49)"
  - "Low-Medium (50-99)"
  - "Medium (100-999)"
  - "High (1K-9.9K)"
  - "Very High (10K+)"
- **Interpretation**: Likely represents repository count or adoption frequency
- **Distribution**: Medium bucket appears common in samples

### 4. **popularity_bucket** (STRING)
- **Data Type**: Categorical string (ordinal)
- **Null Values**: None (0%)
- **Cardinality**: 4 distinct buckets
- **Categories** (ascending order):
  - "Minimal (<10)"
  - "Low (10-99)"
  - "Moderate (100-999)"
  - "Popular (1K-9.9K)"
- **Interpretation**: Likely represents stars, forks, or similar engagement metrics
- **Distribution**: "Minimal" and "Low" appear frequently in samples

### 5. **activity_bucket** (STRING)
- **Data Type**: Categorical string (ordinal)
- **Null Values**: None (0%)
- **Cardinality**: 5 distinct buckets
- **Categories** (ascending order):
  - "Low (<50)"
  - "Low-Medium (50-99)"
  - "Medium (100-999)"
  - "High (1K-9.9K)"
  - "Very High (10K+)"
- **Interpretation**: Likely represents commit count or contribution activity
- **Distribution**: Medium and High buckets appear common

### 6. **team_size_bucket** (STRING)
- **Data Type**: Categorical string (ordinal)
- **Null Values**: None (0%)
- **Cardinality**: 5 distinct buckets
- **Categories** (ascending order):
  - "Individual (1)"
  - "Pair (2-4)"
  - "Small Team (5-19)"
  - "Medium Team (20-99)"
  - "Large Team (100+)"
- **Interpretation**: Number of contributors to repositories
- **Distribution**: "Small Team" and "Pair" appear frequently in samples

### 7. **diversity_bucket** (STRING)
- **Data Type**: Categorical string (ordinal)
- **Null Values**: None (0%)
- **Cardinality**: 5 distinct buckets
- **Categories** (ascending order):
  - "Single (1)"
  - "Dual (2)"
  - "Mixed (3-4)"
  - "Diverse (5-9)"
  - "Very Diverse (10+)"
- **Interpretation**: Likely represents programming language diversity within repositories
- **Distribution**: Ranges from single-language to multi-language projects

### 8. **license_share_bucket** (STRING)
- **Data Type**: Categorical string (ordinal)
- **Null Values**: None (0%)
- **Cardinality**: 4 distinct buckets
- **Categories** (ascending order):
  - "Minimal (<5%)"
  - "Trace (5-9%)"
  - "Minor (10-24%)"
  - "Major (25-49%)"
- **Interpretation**: Percentage representation of license usage within a context
- **Distribution**: "Minimal" appears very frequently, suggesting long-tail distribution

## Potential Query Considerations

### Excellent Filtering Columns:
1. **license** - 15 unique values, perfect for WHERE clauses comparing license types
2. **primary_language** - 259 values, good for language-specific analysis
3. **adoption_level_bucket** - For filtering by project scale
4. **popularity_bucket** - For filtering by engagement levels

### Excellent Grouping/Aggregation Columns:
- **All columns** are pre-bucketed categorical data, making them ideal for GROUP BY operations
- **license + primary_language**: Natural combination for correlation analysis
- Any metric bucket (adoption, popularity, activity, team_size, diversity, license_share) can be aggregated with COUNT(*) for distribution analysis

### Cross-dimensional Analysis:
- **License × Language**: Core relationship (table name suggests this)
- **License × Team Size**: Understand which licenses attract certain team structures
- **Language × Popularity**: Identify trending languages
- **Diversity × Team Size**: Analyze multi-language project characteristics
- **License Share × Adoption**: Understand license dominance patterns

### Join Considerations:
- **license**: Could join to a license details/metadata table
- **primary_language**: Could join to language characteristics table
- No apparent foreign keys, but dimension values could match other GitHub analysis tables

### Query Performance Considerations:
- All string columns may benefit from exact match queries
- No null handling needed (100% complete data)
- Bucketed data means no complex numerical filtering needed
- Consider CASE statements to create custom ordinal rankings from bucket strings

### Data Quality Considerations:
- **Excellent data quality** - no missing values
- Buckets are human-readable but require parsing for numerical comparisons
- All ordinal buckets include both text labels and numerical ranges
- String comparison for buckets won't work for ordering (use CASE for proper sorting)

## Keywords

GitHub, open-source, licenses, programming languages, software repositories, license correlation, language adoption, MIT license, Apache license, GPL, project metrics, repository analysis, team size, contributor analysis, code diversity, license popularity, software development, open-source metrics, language distribution, license adoption, project activity, repository popularity, software licensing, multi-language projects, contributor diversity, GitHub statistics, license trends, language trends

## Table and Column Documentation

**Table Comment**: Not provided in the analysis report.

**Column Comments**: No column-level comments were provided in the analysis report. All column descriptions above are derived from data analysis and value patterns.