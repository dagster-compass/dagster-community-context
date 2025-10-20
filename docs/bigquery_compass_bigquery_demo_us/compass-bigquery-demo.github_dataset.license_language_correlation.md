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
- **Data Quality**: Excellent - no null values across all columns (0% null percentage for all fields)
- **Dataset Type**: Correlation analysis table examining relationships between software licenses and programming languages along with various project metrics
- **Structure**: Each row represents a unique combination of license type, programming language, and associated project characteristics grouped into categorical buckets

## Column Details

### license (STRING)
- **Type**: Categorical identifier for software license types
- **Completeness**: 100% (no nulls)
- **Cardinality**: 15 unique license types
- **Common Values**: Includes popular open-source licenses like apache-2.0, gpl-3.0, bsd-3-clause, mit, mpl-2.0
- **Pattern**: Standard SPDX license identifiers in lowercase with hyphens

### adoption_level_bucket (STRING)
- **Type**: Categorical bucket representing project adoption levels
- **Completeness**: 100% (no nulls)
- **Cardinality**: 5 buckets ranging from low to very high adoption
- **Buckets**: Low (10-49), Low-Medium (50-99), Medium (100-999), High (1K-9.9K), Very High (10K+)
- **Usage**: Good for analyzing adoption patterns across licenses and languages

### popularity_bucket (STRING)
- **Type**: Categorical bucket for project popularity metrics
- **Completeness**: 100% (no nulls)
- **Cardinality**: 4 buckets from minimal to popular
- **Buckets**: Minimal (<10), Low (10-99), Moderate (100-999), Popular (1K-9.9K)
- **Usage**: Ideal for popularity-based filtering and analysis

### primary_language (STRING)
- **Type**: Programming language identifier
- **Completeness**: 100% (no nulls)
- **Cardinality**: 259 unique programming languages
- **Diversity**: Wide range from common languages (JavaScript, Python) to specialized ones (QML, Ren'Py, AMPL)
- **Usage**: Primary dimension for language-based analysis and correlations

### activity_bucket (STRING)
- **Type**: Categorical bucket for project activity levels
- **Completeness**: 100% (no nulls)
- **Cardinality**: 5 buckets similar to adoption levels
- **Buckets**: Low (<50), Low-Medium (50-99), Medium (100-999), High (1K-9.9K), Very High (10K+)
- **Usage**: Good for analyzing project activity patterns

### team_size_bucket (STRING)
- **Type**: Categorical bucket for development team sizes
- **Completeness**: 100% (no nulls)
- **Cardinality**: 5 buckets from individual to large teams
- **Buckets**: Individual (1), Pair (2-4), Small Team (5-19), Medium Team (20-99), Large Team (100+)
- **Usage**: Useful for team size correlation analysis

### diversity_bucket (STRING)
- **Type**: Categorical bucket for team/contributor diversity
- **Completeness**: 100% (no nulls)
- **Cardinality**: 5 buckets measuring diversity levels
- **Buckets**: Single (1), Dual (2), Mixed (3-4), Diverse (5-9), Very Diverse (10+)
- **Usage**: Good for diversity analysis across different dimensions

### license_share_bucket (STRING)
- **Type**: Categorical bucket for license market share
- **Completeness**: 100% (no nulls)
- **Cardinality**: 4 buckets from minimal to major share
- **Buckets**: Minimal (<5%), Trace (5-9%), Minor (10-24%), Major (25-49%)
- **Usage**: Important for understanding license prevalence

## Query Considerations

### Filtering Columns
- **license**: Excellent for filtering by specific license types (15 distinct values)
- **primary_language**: High cardinality (259 values) - good for specific language analysis
- **All bucket columns**: Perfect for range-based filtering using bucket categories

### Grouping/Aggregation Columns
- **license**: Ideal for license-based aggregations
- **primary_language**: Good for language-based grouping, though high cardinality may require careful handling
- **All bucket columns**: Excellent for categorical analysis and cross-tabulations
- **Combination grouping**: License + language combinations for correlation analysis

### Potential Relationships
- **Primary Key**: Likely combination of license + primary_language (possibly with some bucket dimensions)
- **Correlation Analysis**: All bucket columns can be cross-referenced to identify patterns
- **Hierarchical Analysis**: Bucket columns represent different scales of the same underlying metrics

### Data Quality Considerations
- **Excellent Quality**: No missing data across all columns
- **Consistent Formatting**: All bucket columns follow consistent naming patterns with ranges in parentheses
- **Categorical Nature**: All columns are categorical, making them suitable for frequency analysis and cross-tabulations
- **Bucket Consistency**: Similar bucket structures across multiple dimensions enable comparative analysis

## Keywords
license correlation, programming languages, github projects, open source licenses, project metrics, adoption analysis, team size analysis, software diversity, license market share, SPDX identifiers, project activity, popularity metrics, categorical data analysis, correlation matrix, open source statistics

## Table and Column Documentation
*No table comment or column comments were provided in the source data.*