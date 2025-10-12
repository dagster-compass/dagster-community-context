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
- **Data Quality**: Excellent - no null values in any column (0.00% null percentage across all fields)
- **Dataset Type**: GitHub author behavior analysis with bucketed metrics
- **Time Range**: January 2015 to February 2045 (note: future dates likely indicate ongoing/projected data)
- **Key Pattern**: Most authors fall into low-activity categories based on sample data

## Column Details

### author_id (STRING)
- **Type**: Unique identifier (likely hashed)
- **Uniqueness**: 1,799,074 unique values out of 2,173,918 rows (indicating some authors may have multiple entries)
- **Format**: 64-character hexadecimal hash
- **Use Case**: Primary key for author identification

### repo_diversity_bucket (STRING)
- **Type**: Categorical with 5 ordinal levels
- **Values**: Low (2-4), Low-Medium (5-9), Medium (10-19), High (20-49), Very High (50+)
- **Pattern**: Measures how many different repositories an author contributes to
- **Distribution**: Sample data shows predominance of "Low" diversity

### commit_count_bucket (STRING)
- **Type**: Categorical with 5 ordinal levels
- **Values**: Low (5-49), Low-Medium (50-99), Medium (100-499), High (500-999), Very High (1000+)
- **Pattern**: Measures total commit volume per author
- **Distribution**: Sample shows mix of Low and Medium activity levels

### first_commit_ym (INT64)
- **Type**: Year-month integer (YYYYMM format)
- **Range**: 201501 to 204002 (Jan 2015 to Feb 2040)
- **Unique Values**: 101 distinct time periods
- **Pattern**: Tracks when authors first became active

### last_commit_ym (INT64)
- **Type**: Year-month integer (YYYYMM format)
- **Range**: 201501 to 224502 (Jan 2015 to Feb 2245)
- **Unique Values**: 152 distinct time periods
- **Pattern**: Tracks authors' most recent activity

### message_length_bucket (STRING)
- **Type**: Categorical with 4 ordinal levels
- **Values**: Very Short (<50), Short (50-99), Medium (100-199), Long (200+)
- **Pattern**: Measures typical commit message verbosity
- **Distribution**: Sample data shows predominance of "Very Short" messages

### activity_frequency_bucket (STRING)
- **Type**: Categorical with 5 ordinal levels
- **Values**: Rare (<30), Occasional (30-89), Moderate (90-179), Active (180-364), Very Active (365+)
- **Pattern**: Likely measures commits or active days per year
- **Distribution**: Sample data heavily skewed toward "Rare" activity

## Potential Query Considerations

### Excellent for Filtering:
- **Time-based queries**: `first_commit_ym` and `last_commit_ym` for temporal analysis
- **Activity level filtering**: All bucket columns for segmenting user types
- **Author lookup**: `author_id` for specific user analysis

### Ideal for Grouping/Aggregation:
- **Behavior segmentation**: All bucket columns are perfect for GROUP BY operations
- **Trend analysis**: Time columns for temporal grouping
- **Distribution analysis**: Cross-tabulating different bucket dimensions

### Join Considerations:
- **Primary Key**: `author_id` can join with other GitHub author tables
- **Temporal Joins**: Time columns can join with date dimension tables
- **Note**: Some authors appear multiple times, suggesting this might be a time-series or multi-dimensional view

### Data Quality Considerations:
- **Future Dates**: Some last_commit_ym values extend far into the future (2245) - may need filtering
- **Bucket Consistency**: All categorical values follow consistent naming patterns
- **No Missing Data**: Perfect data completeness enables reliable aggregations
- **Hash Anonymization**: Author IDs are anonymized, limiting demographic analysis

## Keywords

GitHub, authors, commits, repository diversity, activity analysis, behavioral segmentation, open source, developer metrics, time series, user engagement, commit frequency, message length, contribution patterns, developer analytics

## Table and Column Documentation

No table comment or column comments were provided in the source data.