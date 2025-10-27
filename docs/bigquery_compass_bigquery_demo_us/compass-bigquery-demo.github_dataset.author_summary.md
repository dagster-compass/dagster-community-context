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
# Dataset Summary: compass-bigquery-demo.github_dataset.author_summary

## Overall Dataset Characteristics

- **Total Rows**: 2,173,918 records
- **Data Quality**: Excellent - no null values detected in any column (0.00% null rate across all fields)
- **Dataset Nature**: This appears to be a summary table of GitHub author activity patterns with pre-categorized behavioral metrics
- **Time Range**: Data spans from January 2015 (201501) to February 2245 (224502), though the future dates suggest some data quality issues or test data
- **Key Pattern**: Most authors (based on sample) fall into lower activity categories (Low commit counts, Rare activity frequency)

## Column Details

### author_id (STRING)
- **Type**: String identifier (appears to be SHA-256 hashes)
- **Uniqueness**: High cardinality with 1,799,074 unique values out of 2,173,918 total rows
- **Pattern**: 64-character hexadecimal strings (anonymized author identifiers)
- **Usage**: Primary key candidate, unique identifier for authors

### repo_diversity_bucket (STRING)
- **Type**: Categorical string with 5 levels
- **Categories**: Low (2-4), Low-Medium (5-9), Medium (10-19), High (20-49), Very High (50+)
- **Pattern**: Represents the number of different repositories an author has contributed to
- **Usage**: Good for segmentation and filtering by author repository diversity

### commit_count_bucket (STRING)
- **Type**: Categorical string with 5 levels
- **Categories**: Low (5-49), Low-Medium (50-99), Medium (100-499), High (500-999), Very High (1000+)
- **Pattern**: Represents total number of commits made by an author
- **Usage**: Excellent for filtering and grouping by author productivity levels

### first_commit_ym (INT64)
- **Type**: Integer representing year-month (YYYYMM format)
- **Range**: 201501 to 204002 (January 2015 to February 2040)
- **Unique Values**: 101 distinct time periods
- **Usage**: Good for time-based filtering and cohort analysis

### last_commit_ym (INT64)
- **Type**: Integer representing year-month (YYYYMM format)  
- **Range**: 201501 to 224502 (January 2015 to February 2245)
- **Unique Values**: 152 distinct time periods
- **Usage**: Good for recency analysis and active period calculations

### activity_frequency_bucket (STRING)
- **Type**: Categorical string with 5 levels
- **Categories**: Rare (<30), Occasional (30-89), Moderate (90-179), Active (180-364), Very Active (365+)
- **Pattern**: Likely represents days active per year or similar frequency metric
- **Usage**: Excellent for segmenting authors by engagement level

### message_length_bucket (STRING)
- **Type**: Categorical string with 4 levels  
- **Categories**: Very Short (<50), Short (50-99), Medium (100-199), Long (200+)
- **Pattern**: Represents average commit message length in characters
- **Usage**: Good for analyzing author communication patterns

## Potential Query Considerations

### Excellent for Filtering:
- **Time-based queries**: Use `first_commit_ym` and `last_commit_ym` for cohort analysis
- **Activity segmentation**: All bucket columns provide natural filtering categories
- **Author-specific lookups**: `author_id` for individual author analysis

### Good for Grouping/Aggregation:
- **Behavioral analysis**: Group by activity buckets to understand user segments
- **Time series**: Group by year-month fields for trend analysis  
- **Cross-dimensional analysis**: Combine multiple bucket columns for detailed segmentation

### Potential Join Keys:
- **author_id**: Primary key for joining with other author-related tables
- **Time fields**: Can join with time-based dimension tables

### Data Quality Considerations:
- **Future dates**: Last commit dates extend to 2245, suggesting data quality issues or test records
- **Bucket consistency**: All categorical fields use consistent naming patterns
- **No missing data**: Zero null values indicate clean, processed data
- **Pre-aggregated nature**: This is clearly a summary table, not raw transactional data

## Keywords

GitHub, author analysis, commit patterns, repository diversity, activity frequency, commit volume, message length, developer behavior, time series, cohort analysis, user segmentation, open source contributions, developer productivity, engagement metrics

## Table and Column Documentation

**Table Comment**: Not provided

**Column Comments**: Not provided