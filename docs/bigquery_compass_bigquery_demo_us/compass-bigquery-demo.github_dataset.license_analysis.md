---
columns:
- activity_bucket (STRING)
- adoption_level_bucket (STRING)
- license (STRING)
- message_length_bucket (STRING)
- popularity_bucket (STRING)
- project_size_bucket (STRING)
- team_size_bucket (STRING)
schema_hash: 9e14690fd77c715f5a541fe91e99d1d212128c14fe00d8073697a4bf4bd9f1e2

---
# Table Summary: compass-bigquery-demo.github_dataset.license_analysis

## Overall Dataset Characteristics

**Total Rows:** 15

**Dataset Purpose:** This table appears to be an aggregated analysis of GitHub repositories categorized by their open-source licenses and various project metrics. Each row represents a unique combination of license type and project characteristic buckets.

**Data Quality:** 
- Excellent data quality with 0% null values across all columns
- Small, curated dataset (15 rows)
- All data is pre-categorized into bucket ranges
- Complete data integrity for all records

**Notable Patterns:**
- All projects have "Low (10-99)" popularity bucket (100% of records)
- Most projects (majority) have "Very High (10K+)" adoption levels
- Activity levels are predominantly "Medium (100-999)"
- Team sizes vary but trend toward smaller teams
- Project sizes are mostly "Small (100-999)"

## Column Details

### license (STRING)
- **Data Type:** Categorical identifier
- **Null Values:** None (0%)
- **Unique Values:** 15 distinct open-source licenses
- **Common Values:** mit, apache-2.0, gpl-3.0, bsd-3-clause, lgpl-3.0, agpl-3.0, artistic-2.0, cc0-1.0, epl-1.0, isc, bsd-2-clause, gpl-2.0
- **Usage:** Primary identifier/dimension for license type analysis
- **Pattern:** Standard SPDX license identifiers in lowercase with version numbers

### adoption_level_bucket (STRING)
- **Data Type:** Ordinal categorical (bucketed metric)
- **Null Values:** None (0%)
- **Unique Values:** 2 categories
- **Values:** "Very High (10K+)", "High (1K-9.9K)"
- **Distribution:** Heavily skewed toward "Very High (10K+)"
- **Usage:** Measures how widely adopted projects with this license are

### popularity_bucket (STRING)
- **Data Type:** Ordinal categorical (bucketed metric)
- **Null Values:** None (0%)
- **Unique Values:** 1 category only
- **Value:** "Low (10-99)" (100% of records)
- **Usage:** Limited analytical value due to uniform distribution
- **Note:** All projects in this dataset fall into the same popularity range

### activity_bucket (STRING)
- **Data Type:** Ordinal categorical (bucketed metric)
- **Null Values:** None (0%)
- **Unique Values:** 2 categories
- **Values:** "Medium (100-999)", "High (1K-9.9K)"
- **Distribution:** Primarily "Medium (100-999)"
- **Usage:** Measures project activity levels (likely commits, PRs, or issues)

### team_size_bucket (STRING)
- **Data Type:** Ordinal categorical (bucketed metric)
- **Null Values:** None (0%)
- **Unique Values:** 3 categories
- **Values:** "Small Team (5-19)", "Medium Team (20-99)", "Large Team (100+)"
- **Distribution:** Most common is "Small Team (5-19)"
- **Usage:** Indicates contributor/team size for projects with each license

### message_length_bucket (STRING)
- **Data Type:** Ordinal categorical (bucketed metric)
- **Null Values:** None (0%)
- **Unique Values:** 2 categories
- **Values:** "Very Short (<50)", "Short (50-99)"
- **Usage:** Likely measures commit message or description lengths
- **Pattern:** All projects have short message lengths

### project_size_bucket (STRING)
- **Data Type:** Ordinal categorical (bucketed metric)
- **Null Values:** None (0%)
- **Unique Values:** 2 categories
- **Values:** "Small (100-999)", "Medium (1K-9.9K)"
- **Distribution:** Primarily "Small (100-999)"
- **Usage:** Measures project size (likely lines of code or file count)

## Query Considerations

### Good for Filtering:
- **license:** Primary dimension for filtering by specific open-source licenses
- **activity_bucket:** Filter for high vs. medium activity projects
- **team_size_bucket:** Filter by organizational scale
- **project_size_bucket:** Filter by codebase size

### Good for Grouping/Aggregation:
- **license:** Primary grouping dimension for comparative license analysis
- **team_size_bucket:** Group by organizational structure
- **activity_bucket:** Group by project activity level
- All bucket columns can be used for crosstab analysis

### Limited Analytical Value:
- **popularity_bucket:** Single value across all records - not useful for filtering or grouping

### Potential Relationships:
- This appears to be a summary/aggregation table
- May join to detailed repository tables on license field
- Could be part of a star schema with license as a dimension

### Data Quality Considerations:
1. Small dataset (15 rows) means limited statistical significance
2. All metrics are pre-bucketed - original numeric values not available
3. Bucket ranges use descriptive labels rather than numeric bounds
4. No temporal dimension - appears to be a snapshot
5. Popularity_bucket uniformity suggests possible filtering at source or specific dataset scope

## Keywords

open source licenses, GitHub repositories, license analysis, software licensing, project metrics, repository statistics, commit activity, team size, project size, adoption metrics, SPDX licenses, MIT license, Apache license, GPL license, BSD license, AGPL, LGPL, EPL, ISC license, Creative Commons, bucketed data, categorical analysis, aggregated metrics, software development, repository analysis

## Table and Column Docs

**Table Comment:** Not provided

**Column Comments:** Not provided

---

**Note:** This table is ideal for high-level comparative analysis of different open-source licenses and their associated project characteristics. The bucketed nature of the data makes it suitable for categorical analysis and visualization but limits precision for detailed statistical analysis.