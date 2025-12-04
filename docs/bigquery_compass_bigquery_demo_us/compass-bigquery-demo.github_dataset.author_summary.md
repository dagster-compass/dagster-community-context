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
# Comprehensive Table Summary: compass-bigquery-demo.github_dataset.author_summary

## 1. Overall Dataset Characteristics

**Total Rows:** 2,173,918

**Dataset Purpose:** This table contains aggregated summary statistics about GitHub authors (developers/contributors), tracking their commit behavior, activity patterns, and contribution characteristics over time.

**Data Quality:** 
- Excellent data completeness - 0% null values across all columns
- All data is pre-aggregated into categorical buckets for analysis convenience
- Author identities are anonymized using hash values (SHA-256 format)
- Time range spans from January 2015 (201501) to approximately April 2024 (224502)

**Notable Patterns:**
- Heavy skew toward low-activity authors: Most authors fall into "Rare (<30)" activity frequency
- Majority of authors contribute to few repositories (Low 2-4 bucket most common)
- Most commit messages are "Very Short (<50)" characters
- Dataset captures ~1.8M unique authors, suggesting some aggregation (fewer unique authors than total rows)
- The presence of future dates (204002, 224502) suggests either data quality issues or test data

## 2. Column Details

### author_id (STRING)
- **Type:** Hashed identifier (SHA-256 format, 64 hex characters)
- **Uniqueness:** 1,799,074 unique values out of 2,173,918 rows (~83% unique)
- **Nulls:** None (0%)
- **Purpose:** Primary anonymized identifier for GitHub contributors
- **Note:** Multiple rows per author suggest either temporal snapshots or different aggregation dimensions

### repo_diversity_bucket (STRING)
- **Type:** Categorical (5 ordinal buckets)
- **Nulls:** None (0%)
- **Values:** 
  - "Low (2-4)" - Author contributed to 2-4 repositories
  - "Low-Medium (5-9)" - 5-9 repositories
  - "Medium (10-19)" - 10-19 repositories
  - "High (20-49)" - 20-49 repositories
  - "Very High (50+)" - 50 or more repositories
- **Distribution:** "Low (2-4)" appears most frequently in samples
- **Use Case:** Measures author's breadth of contribution across different projects

### commit_count_bucket (STRING)
- **Type:** Categorical (5 ordinal buckets)
- **Nulls:** None (0%)
- **Values:**
  - "Low (5-49)" - 5-49 total commits
  - "Low-Medium (50-99)" - 50-99 commits
  - "Medium (100-499)" - 100-499 commits
  - "High (500-999)" - 500-999 commits
  - "Very High (1000+)" - 1000+ commits
- **Distribution:** "Low (5-49)" and "Low-Medium (50-99)" appear frequently
- **Use Case:** Measures author's total volume of contributions

### first_commit_ym (INT64)
- **Type:** Integer representing YYYYMM format
- **Nulls:** None (0%)
- **Range:** 201501 (January 2015) to 204002 (February 2040 - likely error)
- **Format:** 6-digit integer (e.g., 201511 = November 2015)
- **Unique Values:** 101
- **Use Case:** Tracks when author first appeared in the dataset; useful for cohort analysis
- **Note:** Values beyond current date suggest data quality issues

### last_commit_ym (INT64)
- **Type:** Integer representing YYYYMM format
- **Nulls:** None (0%)
- **Range:** 201501 (January 2015) to 224502 (May 2245 - likely error)
- **Format:** 6-digit integer (e.g., 201911 = November 2019)
- **Unique Values:** 152
- **Use Case:** Tracks author's most recent activity; useful for identifying active vs. dormant contributors
- **Note:** Future dates present in data

### activity_frequency_bucket (STRING)
- **Type:** Categorical (5 ordinal buckets)
- **Nulls:** None (0%)
- **Values:**
  - "Rare (<30)" - Active less than 30 days
  - "Occasional (30-89)" - Active 30-89 days
  - "Moderate (90-179)" - Active 90-179 days
  - "Active (180-364)" - Active 180-364 days
  - "Very Active (365+)" - Active 365+ days
- **Distribution:** "Rare (<30)" dominates the sample rows
- **Use Case:** Measures the span of days an author was active (not necessarily consecutive)

### message_length_bucket (STRING)
- **Type:** Categorical (4 ordinal buckets)
- **Nulls:** None (0%)
- **Values:**
  - "Very Short (<50)" - Average message length under 50 characters
  - "Short (50-99)" - 50-99 characters
  - "Medium (100-199)" - 100-199 characters
  - "Long (200+)" - 200+ characters
- **Distribution:** "Very Short (<50)" appears most common
- **Use Case:** Indicates commit message verbosity; may correlate with project documentation practices

## 3. Potential Query Considerations

### Good Filtering Columns:
- **activity_frequency_bucket**: Filter for active vs. inactive contributors
- **commit_count_bucket**: Identify prolific vs. casual contributors
- **repo_diversity_bucket**: Find specialists (low diversity) vs. generalists (high diversity)
- **first_commit_ym / last_commit_ym**: Temporal filtering for specific time periods or cohorts
- **message_length_bucket**: Filter by documentation quality/verbosity

### Good Grouping/Aggregation Columns:
- **All bucket columns**: Natural grouping for distribution analysis
- **first_commit_ym**: Cohort analysis by onboarding period
- **last_commit_ym**: Retention/churn analysis
- **Combinations**: Cross-tabulations (e.g., activity frequency by repo diversity)

### Potential Join Keys:
- **author_id**: Primary key for joining with other author-related tables
- **first_commit_ym / last_commit_ym**: Can join with time-series or calendar tables

### Data Quality Considerations:

1. **Future Dates**: Queries should filter out impossible future dates:
   ```sql
   WHERE first_commit_ym <= 202412 AND last_commit_ym <= 202412
   ```

2. **Multiple Rows Per Author**: Since there are more rows than unique authors, queries counting authors should use `COUNT(DISTINCT author_id)` or understand the grain of the data

3. **Bucketed Data**: Original numeric values are not available, limiting precise calculations (medians, percentiles, etc.)

4. **Activity Span Calculation**: To calculate tenure, convert YYYYMM format:
   ```sql
   CAST(last_commit_ym AS STRING) formatted as date
   ```

5. **Ordinal Bucket Comparisons**: When filtering buckets, be aware of string sorting vs. logical ordering

## 4. Keywords

GitHub, authors, contributors, developers, commits, commit frequency, repository diversity, contribution patterns, activity metrics, message length, tenure, cohort analysis, retention, churn, open source, version control, code contributions, developer behavior, commit history, temporal analysis, engagement metrics, contribution volume, project diversity, commit messages, developer activity, YYYYMM format, bucketed data, categorical analysis

## 5. Table and Column Documentation

**Table Comment:** Not provided

**Column Comments:** 
- author_id: No comment provided
- repo_diversity_bucket: No comment provided
- commit_count_bucket: No comment provided
- first_commit_ym: No comment provided
- last_commit_ym: No comment provided
- activity_frequency_bucket: No comment provided
- message_length_bucket: No comment provided