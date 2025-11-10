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
# Table Summary: license_language_correlation

## Overall Dataset Characteristics

- **Total Rows**: 1,502
- **Data Quality**: Excellent - no null values in any column (0% null rate across all fields)
- **Dataset Purpose**: This table captures the relationship between open-source software licenses and programming languages, along with various project metrics bucketed into categorical ranges
- **Distribution Pattern**: Data is heavily bucketed/categorized, with all metrics converted to human-readable range strings rather than raw numbers

## Column Details

### license (STRING)
- **Type**: Categorical identifier
- **Null Values**: None (0%)
- **Cardinality**: 15 unique licenses
- **Common Values**: mit, apache-2.0, gpl-2.0
- **Purpose**: Represents open-source license types (e.g., MIT, Apache, GPL variants, BSD, Creative Commons, etc.)
- **Query Note**: Good filtering column for license-specific analysis

### primary_language (STRING)
- **Type**: Categorical identifier
- **Null Values**: None (0%)
- **Cardinality**: 259 unique programming languages
- **Sample Values**: Puppet, Common Lisp, Brainfuck, Matlab, Racket, Apex, Batchfile, Fortran
- **Purpose**: Primary programming language used in projects
- **Query Note**: High cardinality makes it excellent for grouping and detailed language-specific queries

### adoption_level_bucket (STRING)
- **Type**: Bucketed metric (range string)
- **Null Values**: None (0%)
- **Cardinality**: 5 distinct buckets
- **Values**: 
  - Low (10-49)
  - Low-Medium (50-99)
  - Medium (100-999)
  - High (1K-9.9K)
  - Very High (10K+)
- **Purpose**: Indicates adoption level/usage count for the license-language combination
- **Query Note**: Ordered categorical data suitable for range filtering and aggregation

### popularity_bucket (STRING)
- **Type**: Bucketed metric (range string)
- **Null Values**: None (0%)
- **Cardinality**: 4 distinct buckets
- **Values**:
  - Minimal (<10)
  - Low (10-99)
  - Moderate (100-999)
  - Popular (1K-9.9K)
- **Purpose**: Measures project popularity (likely stars, forks, or similar metric)
- **Query Note**: Ordered categorical for popularity analysis

### activity_bucket (STRING)
- **Type**: Bucketed metric (range string)
- **Null Values**: None (0%)
- **Cardinality**: 5 distinct buckets
- **Values**:
  - Low (<50)
  - Low-Medium (50-99)
  - Medium (100-999)
  - High (1K-9.9K)
  - Very High (10K+)
- **Purpose**: Indicates project activity level (commits, updates, etc.)
- **Query Note**: Similar bucketing pattern to adoption_level_bucket

### team_size_bucket (STRING)
- **Type**: Bucketed metric (range string)
- **Null Values**: None (0%)
- **Cardinality**: 5 distinct buckets
- **Values**:
  - Individual (1)
  - Pair (2-4)
  - Small Team (5-19)
  - Medium Team (20-99)
  - Large Team (100+)
- **Purpose**: Number of contributors/team members
- **Query Note**: Ordered categorical from individual to large teams

### diversity_bucket (STRING)
- **Type**: Bucketed metric (range string)
- **Null Values**: None (0%)
- **Cardinality**: 5 distinct buckets
- **Values**:
  - Single (1)
  - Dual (2)
  - Mixed (3-4)
  - Diverse (5-9)
  - Very Diverse (10+)
- **Purpose**: Likely measures language diversity or contributor diversity in projects
- **Query Note**: Ordered categorical for diversity analysis

### license_share_bucket (STRING)
- **Type**: Bucketed percentage (range string)
- **Null Values**: None (0%)
- **Cardinality**: 4 distinct buckets
- **Values**:
  - Minimal (<5%)
  - Trace (5-9%)
  - Minor (10-24%)
  - Major (25-49%)
- **Purpose**: Percentage share of specific license within the language/category
- **Sample Pattern**: Most samples show "Minimal (<5%)" indicating fragmented distribution
- **Query Note**: Useful for understanding license dominance in specific contexts

## Potential Query Considerations

### Best Filtering Columns:
- **license**: Low cardinality (15 values) - excellent for WHERE clauses
- **adoption_level_bucket**: 5 buckets - good for filtering by project scale
- **popularity_bucket**: 4 buckets - filter by project visibility
- **team_size_bucket**: 5 buckets - filter by organizational size

### Best Grouping/Aggregation Columns:
- **primary_language**: High cardinality (259) - excellent for detailed breakdowns
- **license**: Moderate cardinality - good for license comparison
- All bucket columns work well for categorical aggregations

### Potential Join Keys:
- **license**: Could join with license metadata tables
- **primary_language**: Could join with language statistics or ecosystem data
- Composite key of (license, primary_language) represents unique combinations

### Data Quality Considerations:
1. **No Missing Data**: All columns are complete - no null handling needed
2. **Bucketed Data**: All metrics are pre-aggregated into ranges; original raw values not available
3. **String Buckets**: Numeric comparisons require careful string matching or CASE statements
4. **Ordering**: Bucket strings include ranges in parentheses which need parsing for numeric-style sorting
5. **Distribution Skew**: Sample data suggests many entries in "Minimal" and "Low" categories

## Keywords

open source licenses, programming languages, GitHub repositories, software adoption, project metrics, license compatibility, language ecosystems, MIT license, Apache license, GPL license, BSD license, project popularity, team size, contributor diversity, activity metrics, adoption levels, software development, code statistics, repository analysis, license distribution, language correlation

## Table and Column Documentation

**Table Comment**: Not provided

**Column Comments**: Not provided

---

**Analysis Note**: This appears to be a correlation/summary table from GitHub data analyzing the relationship between software licenses and programming languages, with all continuous metrics converted to human-readable categorical buckets for easier analysis and reporting.