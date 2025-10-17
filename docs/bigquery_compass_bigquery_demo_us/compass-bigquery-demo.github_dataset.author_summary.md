---
columns:
- activity_frequency_bucket (STRING)
- author_id (STRING)
- commit_count_bucket (STRING)
- first_commit_ym (INT64)
- last_commit_ym (INT64)
- message_length_bucket (STRING)
- repo_diversity_bucket (STRING)
schema_hash: 21b4ce290adcb3be38013ddcaf50e8e9e32e404a658e7bda6ffac5b0bf98350b

---
# Table Summary: compass-bigquery-demo.github_dataset.author_summary

## Overall Dataset Characteristics

- **Total Rows**: 2,173,918 records
- **Data Quality**: Excellent - no null values in any column (0.00% null percentage across all fields)
- **Dataset Type**: Author behavior analysis table with pre-computed buckets/categories for various GitHub activity metrics
- **Time Span**: Covers activity from January 2015 (201501) to potentially February 2045 (224502), though most activity appears concentrated in earlier years
- **Notable Patterns**: 
  - Majority of authors fall into "Low" activity categories across multiple dimensions
  - Heavy skew toward newer/less active contributors
  - Data appears to be aggregated/summarized from raw GitHub commit data

## Column Details

### author_id (STRING)
- **Type**: String identifier (appears to be SHA-256 hash)
- **Uniqueness**: 1,799,074 unique values out of 2,173,918 rows (some authors may have multiple records)
- **Format**: 64-character hexadecimal hash
- **Purpose**: Primary identifier for GitHub authors (anonymized)

### repo_diversity_bucket (STRING)
- **Type**: Categorical ordinal variable
- **Values**: 5 buckets ranging from "Low (2-4)" to "Very High (50+)"
- **Distribution**: Heavily skewed toward "Low (2-4)" category
- **Purpose**: Measures how many different repositories an author has contributed to

### commit_count_bucket (STRING)
- **Type**: Categorical ordinal variable  
- **Values**: 5 buckets ranging from "Low (5-49)" to "Very High (1000+)"
- **Distribution**: Heavily skewed toward "Low (5-49)" category
- **Purpose**: Measures total number of commits made by an author

### first_commit_ym (INT64)
- **Type**: Integer representing year-month (YYYYMM format)
- **Range**: 201501 to 204002 (January 2015 to February 2040)
- **Unique Values**: 101 different year-month combinations
- **Purpose**: Tracks when author made their first commit

### last_commit_ym (INT64)
- **Type**: Integer representing year-month (YYYYMM format)
- **Range**: 201501 to 224502 (January 2015 to February 2245)
- **Unique Values**: 152 different year-month combinations
- **Purpose**: Tracks when author made their most recent commit

### message_length_bucket (STRING)
- **Type**: Categorical ordinal variable
- **Values**: 4 buckets from "Very Short (<50)" to "Long (200+)"
- **Distribution**: Heavily skewed toward "Very Short (<50)" category
- **Purpose**: Categorizes typical commit message length for an author

### activity_frequency_bucket (STRING)
- **Type**: Categorical ordinal variable
- **Values**: 5 buckets from "Rare (<30)" to "Very Active (365+)"
- **Distribution**: Heavily skewed toward "Rare (<30)" category
- **Purpose**: Measures how frequently an author commits (likely days per year)

## Potential Query Considerations

### Good for Filtering:
- **Time-based filtering**: `first_commit_ym` and `last_commit_ym` for temporal analysis
- **Activity level filtering**: All bucket columns for segmenting users by behavior
- **Author identification**: `author_id` for individual author analysis

### Good for Grouping/Aggregation:
- **All bucket columns** are excellent for grouping and creating distribution analyses
- **Time periods**: Year-month fields can be grouped by year or time ranges
- **Cross-tabulation**: Multiple bucket dimensions can be combined for multi-dimensional analysis

### Potential Join Keys:
- **author_id**: Can likely join with other GitHub author/contributor tables
- **Time fields**: Can join with time-series data or other temporal GitHub datasets

### Data Quality Considerations:
- **Future dates**: Some `last_commit_ym` values extend far into the future (2245) - may indicate data quality issues or placeholder values
- **Bucket interpretation**: Bucket ranges are clearly defined in parentheses, making analysis straightforward
- **Skewed distributions**: Most metrics show heavy skew toward low activity - consider this when performing statistical analysis
- **Multiple records per author**: Since unique authors (1.8M) < total rows (2.2M), some authors may have multiple records (possibly time-based segments)

## Keywords

GitHub, author analysis, commit behavior, repository diversity, activity frequency, commit volume, message length, contributor segmentation, open source analytics, developer behavior, time series, categorical buckets

## Table and Column Documentation

*No table comment or column comments were provided in the source data.*