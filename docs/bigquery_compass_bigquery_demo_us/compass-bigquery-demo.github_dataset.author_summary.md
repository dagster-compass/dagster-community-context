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

This table contains **2,173,918 rows** of GitHub author activity summaries, representing approximately 1.8 million unique authors. The dataset appears to be a pre-aggregated summary table that captures key behavioral metrics about GitHub contributors over time.

**Data Quality:** Excellent - no null values detected in any column. All fields are fully populated.

**Time Coverage:** The data spans from January 2015 (201501) to early 2025, with some outlier records extending to 2245 (likely data quality issues or placeholder values).

**Key Pattern:** The majority of authors fall into "Low" activity buckets across multiple dimensions (commit count, repo diversity, activity frequency), suggesting a long-tail distribution typical of open-source contributions where most contributors make limited contributions.

## Column Details

### author_id (STRING)
- **Type:** String identifier (appears to be SHA-256 hash)
- **Nulls:** None (0.00%)
- **Cardinality:** 1,799,074 unique values out of 2,173,918 rows
- **Pattern:** 64-character hexadecimal strings (e.g., "0165f0be744d25935d1cde6fe5252418e015f23fa19d6664915c9ffa4ba6f0ee")
- **Note:** Some authors have multiple records (likely due to different time period aggregations or data duplication)
- **Purpose:** Primary identifier for GitHub authors, anonymized via hashing

### repo_diversity_bucket (STRING)
- **Type:** Categorical ordinal string
- **Nulls:** None (0.00%)
- **Values:** 5 distinct categories
  - "Low (2-4)" - Works on 2-4 repositories
  - "Low-Medium (5-9)" - Works on 5-9 repositories
  - "Medium (10-19)" - Works on 10-19 repositories
  - "High (20-49)" - Works on 20-49 repositories
  - "Very High (50+)" - Works on 50+ repositories
- **Distribution:** Heavily skewed toward "Low (2-4)", indicating most authors contribute to few repositories
- **Purpose:** Measures breadth of an author's contribution across different projects

### commit_count_bucket (STRING)
- **Type:** Categorical ordinal string
- **Nulls:** None (0.00%)
- **Values:** 5 distinct categories
  - "Low (5-49)" - 5-49 commits
  - "Low-Medium (50-99)" - 50-99 commits
  - "Medium (100-499)" - 100-499 commits
  - "High (500-999)" - 500-999 commits
  - "Very High (1000+)" - 1000+ commits
- **Distribution:** Most authors in "Low (5-49)" bucket, following typical long-tail pattern
- **Purpose:** Measures total volume of author contributions

### first_commit_ym (INT64)
- **Type:** Integer representing YYYYMM format
- **Nulls:** None (0.00%)
- **Range:** 201501 to 204002 (January 2015 to February 2040)
- **Cardinality:** 101 unique values
- **Format:** YYYYMM (e.g., 201802 = February 2018)
- **Valid Range:** Primarily 2015-2024, with some future dates likely being data errors
- **Purpose:** Captures when author made their first commit in the dataset

### last_commit_ym (INT64)
- **Type:** Integer representing YYYYMM format
- **Nulls:** None (0.00%)
- **Range:** 201501 to 224502 (January 2015 to February 2245)
- **Cardinality:** 152 unique values
- **Format:** YYYYMM (e.g., 202107 = July 2021)
- **Data Quality Note:** Contains far-future dates (e.g., 2245) that are likely data quality issues
- **Purpose:** Captures when author made their most recent commit in the dataset

### activity_frequency_bucket (STRING)
- **Type:** Categorical ordinal string
- **Nulls:** None (0.00%)
- **Values:** 5 distinct categories
  - "Rare (<30)" - Active fewer than 30 days
  - "Occasional (30-89)" - Active 30-89 days
  - "Moderate (90-179)" - Active 90-179 days
  - "Active (180-364)" - Active 180-364 days
  - "Very Active (365+)" - Active 365+ days
- **Distribution:** Most authors fall into "Rare (<30)" category
- **Purpose:** Measures consistency/frequency of author activity over time

### message_length_bucket (STRING)
- **Type:** Categorical ordinal string
- **Nulls:** None (0.00%)
- **Values:** 4 distinct categories
  - "Very Short (<50)" - Average message length < 50 characters
  - "Short (50-99)" - Average message length 50-99 characters
  - "Medium (100-199)" - Average message length 100-199 characters
  - "Long (200+)" - Average message length 200+ characters
- **Distribution:** Mix of "Very Short" and "Short" most common, with "Long" appearing frequently in samples
- **Purpose:** Characterizes commit message verbosity/documentation practices

## Query Considerations

### Ideal for Filtering:
- **first_commit_ym / last_commit_ym**: Good for time-based filtering (e.g., "authors who started in 2020", "authors active in last 6 months")
- **All bucket columns**: Excellent for segmentation queries (e.g., "high-volume, low-diversity authors")
- **author_id**: For specific author lookups

### Ideal for Grouping/Aggregation:
- **All bucket columns**: Perfect for distribution analysis (e.g., COUNT by commit_count_bucket)
- **first_commit_ym**: For cohort analysis (authors by onboarding period)
- **Combinations**: Multi-dimensional analysis (e.g., repo_diversity vs commit_count)

### Potential Join Keys:
- **author_id**: Primary key for joining with detailed commit/repository tables
- **Time fields**: Could join with temporal dimension tables

### Data Quality Considerations:

1. **Duplicate author_ids**: ~375K more rows than unique authors suggests either:
   - Multiple time period snapshots per author
   - Data quality issues requiring deduplication
   - Multiple profiles/emails for same author

2. **Future dates**: The last_commit_ym field contains dates extending to year 2245 - queries should filter these out (e.g., `WHERE last_commit_ym <= 202412`)

3. **Bucket ordering**: All bucket columns use text that includes the range in parentheses, making lexicographic sorting incorrect. Use CASE statements for proper ordering.

4. **Activity period calculation**: Can derive activity span by `last_commit_ym - first_commit_ym`, but watch for same-month scenarios

5. **Temporal validity**: When querying for "active" authors, consider defining appropriate thresholds for last_commit_ym

## Keywords

GitHub, git, authors, contributors, developers, commit analysis, repository diversity, activity patterns, contribution metrics, developer engagement, open source, code commits, commit frequency, developer behavior, author analytics, contribution history, developer segmentation, activity buckets, commit messages, developer cohorts, time series, longitudinal analysis, developer productivity, engagement metrics

## Table and Column Documentation

**Table Comment:** Not provided in the analysis report.

**Column Comments:** No column-level comments were provided in the analysis report. All column descriptions above are inferred from the data patterns and naming conventions.