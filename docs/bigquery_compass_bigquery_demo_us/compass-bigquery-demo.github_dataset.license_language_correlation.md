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
- **Data Quality**: Excellent - no null values in any column
- **Dataset Purpose**: This table appears to analyze the correlation between software licenses and programming languages, along with various project metrics in GitHub repositories
- **Key Pattern**: The data is structured around license-language combinations with associated project characteristics measured in categorical buckets

## Column Details

### license (STRING)
- **Data Type**: String, categorical
- **Null Values**: 0.00% (complete data)
- **Unique Values**: 15 distinct license types
- **Common Licenses**: MIT, GPL-3.0, Apache-2.0, GPL-2.0, BSD variants
- **Value Pattern**: Standard open-source license identifiers (SPDX format)
- **Query Use**: Primary filtering and grouping column for license analysis

### primary_language (STRING)
- **Data Type**: String, categorical
- **Null Values**: 0.00% (complete data)
- **Unique Values**: 259 distinct programming languages
- **Diversity**: High variety including mainstream (HTML, JavaScript) and niche languages (EmberScript, QML, Smarty)
- **Query Use**: Primary filtering and grouping column for language-based analysis

### adoption_level_bucket (STRING)
- **Data Type**: String, ordinal categorical
- **Null Values**: 0.00% (complete data)
- **Unique Values**: 5 buckets ranging from "Low (10-49)" to "Very High (10K+)"
- **Pattern**: Measures project adoption with clear numeric ranges
- **Query Use**: Good for filtering by adoption levels and trend analysis

### popularity_bucket (STRING)
- **Data Type**: String, ordinal categorical
- **Null Values**: 0.00% (complete data)
- **Unique Values**: 4 buckets from "Minimal (<10)" to "Popular (1K-9.9K)"
- **Pattern**: Measures popularity with ascending numeric thresholds
- **Query Use**: Filtering and comparison of popularity levels

### activity_bucket (STRING)
- **Data Type**: String, ordinal categorical
- **Null Values**: 0.00% (complete data)
- **Unique Values**: 5 buckets from "Low (<50)" to "Very High (10K+)"
- **Pattern**: Similar structure to adoption_level_bucket
- **Query Use**: Analysis of project activity levels

### team_size_bucket (STRING)
- **Data Type**: String, ordinal categorical
- **Null Values**: 0.00% (complete data)
- **Unique Values**: 5 buckets from "Individual (1)" to "Large Team (100+)"
- **Pattern**: Clear progression of team sizes
- **Query Use**: Team size analysis and correlation studies

### diversity_bucket (STRING)
- **Data Type**: String, ordinal categorical
- **Null Values**: 0.00% (complete data)
- **Unique Values**: 5 buckets from "Single (1)" to "Very Diverse (10+)"
- **Pattern**: Appears to measure contributor diversity
- **Query Use**: Diversity analysis and team composition studies

### license_share_bucket (STRING)
- **Data Type**: String, ordinal categorical
- **Null Values**: 0.00% (complete data)
- **Unique Values**: 4 buckets from "Minimal (<5%)" to "Major (25-49%)"
- **Pattern**: Percentage-based buckets measuring license adoption within languages
- **Query Use**: License market share analysis

## Query Considerations

### Excellent Filtering Columns
- `license`: 15 distinct values, perfect for license-specific analysis
- `primary_language`: High cardinality (259 values) for language-specific queries
- All bucket columns: Pre-categorized for easy range filtering

### Ideal Grouping/Aggregation Columns
- `license` and `primary_language`: Primary dimensions for correlation analysis
- All bucket columns: Pre-aggregated categories perfect for summary statistics
- Combinations like license-language pairs for cross-tabulation

### Potential Relationships
- **Primary Key**: Likely combination of license + primary_language
- **No Foreign Keys**: Appears to be a denormalized analytical table
- **Correlation Focus**: Designed to analyze relationships between licenses and languages

### Data Quality Considerations
- **Perfect Completeness**: No missing data concerns
- **Consistent Categorization**: All bucket columns use consistent naming patterns
- **Ordinal Nature**: Bucket columns have inherent ordering that should be preserved in analysis
- **Sample Bias**: Data represents GitHub repositories, may not reflect all software development

## Keywords

license analysis, programming languages, GitHub data, open source licenses, software development metrics, project characteristics, adoption levels, team size analysis, diversity metrics, license correlation, software analytics, repository data, SPDX licenses, development activity, project popularity

## Table and Column Documentation

**Table Comment**: Not provided

**Column Comments**: No individual column comments provided in the analysis report.