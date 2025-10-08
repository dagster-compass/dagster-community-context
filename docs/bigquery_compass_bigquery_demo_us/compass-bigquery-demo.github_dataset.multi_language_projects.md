---
columns:
- activity_bucket (STRING)
- language_diversity_bucket (STRING)
- license (STRING)
- popularity_bucket (STRING)
- primary_language (STRING)
- primary_language_size_bucket (STRING)
- repo_id (STRING)
- team_size_bucket (STRING)
schema_hash: 4d505ee05317b2b1b61697ed72e894bda1322381b4e868971fb5ba624d10b41b

---
# Table Analysis Summary: compass-bigquery-demo.github_dataset.multi_language_projects

## Overall Dataset Characteristics

- **Total Records**: 1,753,925 rows
- **Data Quality**: Excellent - 0% null values across all columns
- **Dataset Focus**: GitHub repositories with multi-language codebases, categorized by various project characteristics
- **Unique Repositories**: Each row represents a unique repository (repo_id is 100% unique)
- **Data Structure**: All columns use categorical bucket classifications for easy analysis and filtering

## Column Details

### repo_id (STRING)
- **Type**: Unique identifier (hash-based)
- **Completeness**: 100% populated
- **Uniqueness**: 1,753,925 unique values (one per row)
- **Format**: 64-character hexadecimal hash
- **Usage**: Primary key for individual repository identification

### language_diversity_bucket (STRING)
- **Type**: Categorical classification of programming language variety
- **Categories**: 5 buckets ranging from "Dual (2)" to "Very Diverse (20+)"
- **Distribution**: Includes Dual, Multi (3-4), Mixed (5-9), Diverse (10-19), Very Diverse (20+)
- **Usage**: Ideal for filtering and grouping by language complexity

### primary_language (STRING)
- **Type**: Programming language identifier
- **Variety**: 372 distinct languages
- **Examples**: Objective-C, C, CSS, HTML, Perl, JavaScript, Python, etc.
- **Range**: From common languages (JavaScript, Python) to specialized ones (1C Enterprise, AIDL, APL)
- **Usage**: Primary grouping dimension for language-based analysis

### primary_language_size_bucket (STRING)
- **Type**: Categorical size classification of primary language codebase
- **Categories**: 5 buckets from "Tiny (<1K)" to "Very Large (1M+)"
- **Progression**: Tiny → Small (1K-9.9K) → Medium (10K-99K) → Large (100K-999K) → Very Large (1M+)
- **Usage**: Filtering by project scale and complexity

### popularity_bucket (STRING)
- **Type**: Repository popularity/engagement metric
- **Categories**: 5 levels from "Minimal (<10)" to "Very Popular (10K+)"
- **Scale**: Minimal → Low (10-99) → Moderate (100-999) → Popular (1K-9.9K) → Very Popular (10K+)
- **Distribution**: Heavy concentration in "Minimal (<10)" category
- **Usage**: Analyzing project visibility and community engagement

### activity_bucket (STRING)
- **Type**: Development activity level classification
- **Categories**: 5 levels from "Low (10-49)" to "Very High (10K+)"
- **Range**: Low → Low-Medium (50-99) → Medium (100-999) → High (1K-9.9K) → Very High (10K+)
- **Pattern**: Most repositories show lower activity levels
- **Usage**: Filtering by project maintenance and development intensity

### license (STRING)
- **Type**: Open source license classification
- **Variety**: 15 distinct license types
- **Common Licenses**: MIT, GPL-2.0, GPL-3.0, Apache-2.0, BSD variants
- **Coverage**: Includes permissive (MIT, BSD) and copyleft (GPL, AGPL) licenses
- **Usage**: Legal and licensing analysis, compliance filtering

### team_size_bucket (STRING)
- **Type**: Development team size classification
- **Categories**: 5 buckets from "Individual (1)" to "Large Team (100+)"
- **Scale**: Individual → Pair (2-4) → Small Team (5-19) → Medium Team (20-99) → Large Team (100+)
- **Pattern**: Strong representation across all team sizes
- **Usage**: Analyzing collaboration patterns and project management approaches

## Query Considerations

### Excellent Filtering Columns
- **language_diversity_bucket**: Multi-language project complexity analysis
- **primary_language**: Language-specific repository analysis
- **popularity_bucket**: Community engagement filtering
- **license**: Legal compliance and license distribution studies
- **team_size_bucket**: Collaboration scale analysis

### Strong Grouping/Aggregation Dimensions
- **primary_language**: Language popularity and ecosystem analysis
- **license**: License adoption patterns
- **Combination analysis**: Cross-tabulation of language diversity × team size, popularity × activity, etc.

### Key Relationships
- **Size correlations**: primary_language_size_bucket vs. team_size_bucket vs. activity_bucket
- **Popularity patterns**: popularity_bucket vs. activity_bucket relationships
- **Language ecosystems**: primary_language vs. language_diversity_bucket analysis

### Data Quality Advantages
- **No missing data**: All columns 100% populated, eliminating need for null handling
- **Consistent categorization**: All metrics use standardized bucket ranges
- **Unique identification**: repo_id provides perfect granularity for detailed analysis

## Keywords

GitHub repositories, multi-language projects, programming languages, open source licenses, software development, team collaboration, project metrics, repository analysis, language diversity, code size analysis, popularity metrics, development activity, MIT license, GPL license, Apache license, software engineering analytics

## Table and Column Documentation

No table comment or column comments are present in this dataset.