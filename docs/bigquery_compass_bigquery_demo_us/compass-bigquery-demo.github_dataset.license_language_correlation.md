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
# Comprehensive Table Analysis Summary: compass-bigquery-demo.github_dataset.license_language_correlation

## Overall Dataset Characteristics

- **Total Rows**: 1,502 records
- **Data Quality**: Excellent - all columns have 0% null values, indicating complete data coverage
- **Dataset Focus**: This table appears to analyze the correlation between software licenses and programming languages in GitHub repositories, with additional metrics around project characteristics
- **Distribution Pattern**: The data shows a diverse range of programming languages (259 unique values) paired with a smaller set of common open-source licenses (15 unique values)

## Column Details

### license (STRING)
- **Data Type**: Categorical string
- **Completeness**: 100% (0% nulls)
- **Unique Values**: 15 distinct licenses
- **Common Licenses**: Includes major open-source licenses like MIT, Apache-2.0, GPL variants, BSD variants, and others
- **Pattern**: Standard SPDX license identifiers (lowercase with hyphens)

### popularity_bucket (STRING) 
- **Data Type**: Categorical string with numeric ranges
- **Completeness**: 100% (0% nulls)
- **Categories**: 4 ordinal buckets from "Minimal (<10)" to "Popular (1K-9.9K)"
- **Distribution Pattern**: Likely skewed toward lower popularity ranges based on typical GitHub repository distributions

### adoption_level_bucket (STRING)
- **Data Type**: Categorical string with numeric ranges  
- **Completeness**: 100% (0% nulls)
- **Categories**: 5 ordinal buckets from "Low (10-49)" to "Very High (10K+)"
- **Range**: Broader range than popularity, suggesting different measurement criteria

### primary_language (STRING)
- **Data Type**: Categorical string
- **Completeness**: 100% (0% nulls) 
- **Diversity**: 259 unique programming languages - very high diversity
- **Examples**: Includes both common (Ruby, CSS) and specialized languages (MATLAB, Stata, VimL, Cap'n Proto)

### activity_bucket (STRING)
- **Data Type**: Categorical string with numeric ranges
- **Completeness**: 100% (0% nulls)
- **Categories**: 5 ordinal buckets from "Low (<50)" to "Very High (10K+)"
- **Pattern**: Similar structure to adoption_level_bucket but measuring different activity metrics

### team_size_bucket (STRING)
- **Data Type**: Categorical string with descriptive labels
- **Completeness**: 100% (0% nulls)
- **Categories**: 5 buckets from "Individual (1)" to "Large Team (100+)"
- **Pattern**: Uses both descriptive names and numeric ranges

### diversity_bucket (STRING)
- **Data Type**: Categorical string with descriptive labels
- **Completeness**: 100% (0% nulls)
- **Categories**: 5 buckets from "Single (1)" to "Very Diverse (10+)"
- **Interpretation**: Likely measures contributor or technology diversity

### license_share_bucket (STRING)
- **Data Type**: Categorical string with percentage ranges
- **Completeness**: 100% (0% nulls)
- **Categories**: 4 percentage-based buckets from "Minimal (<5%)" to "Major (25-49%)"
- **Pattern**: Measures relative license adoption within some reference group

## Query Considerations

### Filtering Columns
- **license**: Excellent for filtering by specific open-source licenses
- **primary_language**: Good for language-specific analysis despite high cardinality
- All bucket columns are ideal for range-based filtering

### Grouping/Aggregation Columns
- **license**: Perfect for license adoption analysis (15 distinct values)
- **popularity_bucket, adoption_level_bucket, activity_bucket**: Excellent for trend analysis across ordinal categories
- **team_size_bucket, diversity_bucket**: Good for organizational pattern analysis
- **primary_language**: Can be grouped but may need LIMIT clauses due to high cardinality (259 values)

### Potential Relationships
- Strong correlation potential between all bucket metrics (popularity, adoption, activity, team size)
- License and language combinations for ecosystem analysis
- Team characteristics (size, diversity) correlation with project metrics

### Data Quality Considerations
- **Excellent data quality**: No null handling required
- **Consistent bucketing**: All bucket columns use clear, non-overlapping ranges
- **High language diversity**: May need aggregation strategies for language analysis
- **Ordinal nature**: Bucket columns have natural ordering for trend analysis

## Keywords

license analysis, programming languages, GitHub repositories, open source, software metrics, team collaboration, project popularity, adoption patterns, diversity metrics, SPDX licenses, repository statistics, software development, code analysis, programming language correlation

## Table and Column Docs

No table comment or column comments were provided in the analysis report.