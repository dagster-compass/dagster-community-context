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

**General Description:** This table contains an analysis of open-source software licenses and their associated project characteristics. Each row represents a unique license type with bucketed metrics describing the projects using that license.

**Data Quality:** 
- Excellent data quality with 0% null values across all columns
- Complete dataset with all 15 rows containing valid data
- Consistent bucketing methodology across all metric columns

**Notable Patterns:**
- All licenses show "Low (10-99)" popularity, indicating uniform distribution in this metric
- Most licenses (likely ~13-14 out of 15) fall into "Very High (10K+)" adoption levels
- Project characteristics vary across licenses, suggesting different communities favor different licenses

---

## Column Details

### license (STRING)
**Primary identifier column containing open-source license names**
- **Data Type:** STRING
- **Nulls:** 0% (complete)
- **Cardinality:** 15 unique values (each row has a unique license)
- **Common Values:** agpl-3.0, apache-2.0, artistic-2.0, bsd-2-clause, bsd-3-clause, cc0-1.0, epl-1.0, gpl-2.0, gpl-3.0, isc, lgpl-2.1, mpl-2.0, and 3 others
- **Format:** Lowercase license identifiers with version numbers (e.g., "apache-2.0", "gpl-3.0")

### adoption_level_bucket (STRING)
**Categorizes license adoption by project count ranges**
- **Data Type:** STRING (categorical/ordinal)
- **Nulls:** 0%
- **Cardinality:** 2 categories
- **Values:** 
  - "High (1K-9.9K)" - 1,000 to 9,999 projects
  - "Very High (10K+)" - 10,000+ projects (appears to be the dominant category)
- **Distribution:** Heavily skewed toward "Very High (10K+)"

### popularity_bucket (STRING)
**Measures popularity metric (likely stars, forks, or watches)**
- **Data Type:** STRING (categorical/ordinal)
- **Nulls:** 0%
- **Cardinality:** 1 category (uniform across all rows)
- **Values:** "Low (10-99)" only
- **Note:** This column has no variance in the dataset; all licenses have the same popularity bucket

### activity_bucket (STRING)
**Categorizes repository activity levels (commits, PRs, issues)**
- **Data Type:** STRING (categorical/ordinal)
- **Nulls:** 0%
- **Cardinality:** 2 categories
- **Values:**
  - "Medium (100-999)" - appears more frequently
  - "High (1K-9.9K)" - less common
- **Distribution:** Majority are "Medium" with some "High" outliers

### message_length_bucket (STRING)
**Categorizes commit message lengths**
- **Data Type:** STRING (categorical/ordinal)
- **Nulls:** 0%
- **Cardinality:** 2 categories
- **Values:**
  - "Very Short (<50)" - less than 50 characters
  - "Short (50-99)" - 50 to 99 characters
- **Distribution:** Roughly balanced between the two categories

### project_size_bucket (STRING)
**Categorizes project size (likely by lines of code or file count)**
- **Data Type:** STRING (categorical/ordinal)
- **Nulls:** 0%
- **Cardinality:** 2 categories
- **Values:**
  - "Small (100-999)"
  - "Medium (1K-9.9K)"
- **Distribution:** Appears to favor "Small" projects

### team_size_bucket (STRING)
**Categorizes contributor team sizes**
- **Data Type:** STRING (categorical/ordinal)
- **Nulls:** 0%
- **Cardinality:** 3 categories
- **Values:**
  - "Small Team (5-19)" - most common
  - "Medium Team (20-99)" - moderately common
  - "Large Team (100+)" - least common
- **Distribution:** Skewed toward smaller teams

---

## Query Considerations

### Filtering Columns
- **license:** Primary key for filtering specific licenses (e.g., `WHERE license = 'apache-2.0'`)
- **adoption_level_bucket:** Filter for high-adoption vs. lower-adoption licenses
- **activity_bucket:** Identify more active vs. less active license communities
- **team_size_bucket:** Filter by development team sizes
- **project_size_bucket:** Segment by project complexity

### Grouping/Aggregation Columns
- **All bucket columns** are suitable for GROUP BY operations
- Count aggregations would work well: `COUNT(*) by adoption_level_bucket`
- Cross-tabulation opportunities (e.g., team size vs. project size by license type)

### Important Notes for Queries
- **popularity_bucket has no variance** - filtering or grouping by this column is not useful
- All bucket columns use **ordinal categories** - be aware when sorting that string sorting may not reflect logical order
- The dataset is **small (15 rows)** - suitable for complete scans
- **No natural join keys** visible, but license names could potentially join with other GitHub license tables

### Data Quality Considerations
- No null handling required
- Consider bucket ranges when interpreting aggregations
- String comparisons needed for bucket filtering (use exact matches)
- When comparing across buckets, remember these are ranges, not precise values

---

## Keywords

open-source licenses, GitHub analysis, license adoption, software licenses, Apache, GPL, AGPL, BSD, MIT, ISC, EPL, MPL, LGPL, CC0, artistic license, project metrics, team size, project size, commit messages, repository activity, software popularity, license comparison, open source metrics, license statistics, developer metrics, code metrics, repository analysis

---

## Table and Column Documentation

**Table Comment:** Not provided

**Column Comments:** Not provided for any columns