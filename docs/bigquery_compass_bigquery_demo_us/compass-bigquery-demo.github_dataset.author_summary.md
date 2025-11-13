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
# Table Summary: author_summary

## Overall Dataset Characteristics

**Total Rows:** 2,173,918

**General Description:** This table contains summary statistics for GitHub authors/contributors, tracking their commit activity patterns and behavior across repositories. Each row represents a unique author with aggregated metrics about their contribution history.

**Data Quality:** Excellent - 0% null values across all columns, indicating complete data coverage for all authors in the dataset.

**Notable Patterns:**
- The dataset covers activity from January 2015 (201501) to as late as 2245 (far future dates likely indicate data quality issues or placeholder values)
- Approximately 1.8M unique authors out of 2.2M total rows, suggesting some authors may have multiple entries or the data is segmented by time periods
- Most authors fall into the "Rare (<30)" activity frequency bucket and "Low (5-49)" commit count bucket, indicating a long-tail distribution typical of open source contributions
- Author IDs are hashed/anonymized (64-character hexadecimal strings)

## Column Details

### author_id (STRING)
- **Data Type:** STRING (hexadecimal hash)
- **Format:** 64-character SHA-256 hash
- **Null Values:** None (0%)
- **Unique Values:** 1,799,074 (83% of total rows are unique)
- **Purpose:** Anonymized unique identifier for each GitHub author
- **Note:** The ratio of unique IDs to total rows (83%) suggests possible duplicate entries or time-based segmentation

### commit_count_bucket (STRING)
- **Data Type:** STRING (categorical)
- **Null Values:** None (0%)
- **Unique Values:** 5 categories
- **Distribution:**
  - Low (5-49): Most common
  - Low-Medium (50-99)
  - Medium (100-499)
  - High (500-999)
  - Very High (1000+): Least common
- **Purpose:** Categorizes authors by total number of commits
- **Query Use:** Excellent for filtering power users vs. casual contributors

### repo_diversity_bucket (STRING)
- **Data Type:** STRING (categorical)
- **Null Values:** None (0%)
- **Unique Values:** 5 categories
- **Distribution:**
  - Low (2-4): Most common
  - Low-Medium (5-9)
  - Medium (10-19)
  - High (20-49)
  - Very High (50+): Least common
- **Purpose:** Measures how many different repositories an author has contributed to
- **Query Use:** Useful for identifying specialized vs. diverse contributors

### message_length_bucket (STRING)
- **Data Type:** STRING (categorical)
- **Null Values:** None (0%)
- **Unique Values:** 4 categories
- **Distribution:**
  - Very Short (<50): Most common
  - Short (50-99)
  - Medium (100-199)
  - Long (200+)
- **Purpose:** Categorizes average commit message length
- **Query Use:** Can indicate documentation quality or commit message verbosity patterns

### activity_frequency_bucket (STRING)
- **Data Type:** STRING (categorical)
- **Null Values:** None (0%)
- **Unique Values:** 5 categories
- **Distribution:**
  - Rare (<30): Overwhelmingly most common
  - Occasional (30-89)
  - Moderate (90-179)
  - Active (180-364)
  - Very Active (365+): Least common
- **Purpose:** Measures commit frequency (likely days with commits per year)
- **Query Use:** Identifies engagement levels and active vs. dormant contributors

### first_commit_ym (INT64)
- **Data Type:** INT64
- **Format:** YYYYMM (year-month as integer)
- **Null Values:** None (0%)
- **Range:** 201501 to 204002 (January 2015 to February 2040)
- **Unique Values:** 101
- **Note:** Future dates (2040) suggest data quality issues or test data
- **Purpose:** Tracks when author first contributed
- **Query Use:** Excellent for cohort analysis and identifying new vs. veteran contributors

### last_commit_ym (INT64)
- **Data Type:** INT64
- **Format:** YYYYMM (year-month as integer)
- **Null Values:** None (0%)
- **Range:** 201501 to 224502 (January 2015 to May 2245)
- **Unique Values:** 152
- **Note:** Extreme future dates (2245) indicate significant data quality issues
- **Purpose:** Tracks most recent contribution
- **Query Use:** Identify active vs. inactive contributors, churn analysis

## Potential Query Considerations

### Filtering Columns:
- **commit_count_bucket**: Filter for high-volume contributors or casual users
- **activity_frequency_bucket**: Identify active vs. inactive users
- **first_commit_ym / last_commit_ym**: Time-based filtering (be cautious of future dates)
- **repo_diversity_bucket**: Find specialists vs. generalists
- **message_length_bucket**: Analyze documentation practices

### Grouping/Aggregation:
- All bucket columns are ideal for GROUP BY operations
- **first_commit_ym**: Cohort analysis by joining period
- **last_commit_ym**: Activity trend analysis
- Combine buckets to create multi-dimensional contributor profiles

### Join Keys:
- **author_id**: Primary key for joining with other author-related tables
- Time columns (first/last_commit_ym) can join with date dimensions

### Data Quality Considerations:
- **Future dates**: Filter out records where last_commit_ym > current date (e.g., > 202412)
- **Author ID duplicates**: Investigate why unique authors (1.8M) < total rows (2.2M)
- **Date validation**: Consider adding WHERE clauses to exclude unrealistic dates
- **Bucket ranges**: Understand bucket definitions to avoid misinterpretation in queries

### Recommended Query Patterns:
```sql
-- Example: Active contributors analysis
WHERE activity_frequency_bucket IN ('Active (180-364)', 'Very Active (365+)')
  AND last_commit_ym >= 202301
  AND last_commit_ym <= 202412

-- Example: New contributor cohorts
WHERE first_commit_ym BETWEEN 202101 AND 202112
GROUP BY first_commit_ym, commit_count_bucket
```

## Keywords
GitHub, authors, contributors, commits, repository diversity, commit frequency, activity patterns, contributor analysis, open source, commit messages, developer activity, author metrics, contribution patterns, cohort analysis, developer engagement, commit history, repository contributions, developer profiles, author summary, GitHub analytics, contribution metrics, developer statistics, commit behavior, author activity, repository engagement

## Table and Column Documentation

**Table Comment:** Not provided in the analysis report.

**Column Comments:** No column-level comments were provided in the analysis report.