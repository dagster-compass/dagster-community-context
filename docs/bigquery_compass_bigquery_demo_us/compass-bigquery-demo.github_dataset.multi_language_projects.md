---
columns:
- activity_bucket (STRING)
- language_diversity_bucket (STRING)
- license (STRING)
- popularity_bucket (STRING)
- primary_language (STRING)
- primary_language_size_bucket (STRING)
- repo_name (STRING)
- team_size_bucket (STRING)
schema_hash: c2aadb686f159e86814deb0799aad621fe4a3583cbee2e5cc96cab3fe0a011c2

---
# Table Summary: compass-bigquery-demo.github_dataset.multi_language_projects

## Overall Dataset Characteristics

**Total Rows:** 1,753,925

**General Description:**
This table contains GitHub repository metadata focused on multi-language projects. Each row represents a unique GitHub repository with bucketed/categorical metrics about the repository's characteristics including language diversity, size, popularity, activity levels, and team composition.

**Data Quality:**
- Excellent data quality with 0% null values across all columns
- All columns use categorical/bucketed values rather than raw numbers
- Each repo_name is unique (1,753,925 unique values matching total rows)
- Consistent bucketing scheme across similar metrics (using ranges like <10, 10-49, 50-99, etc.)

**Notable Patterns:**
- Most repositories fall into the "Minimal (<10)" popularity bucket based on sample data
- Language diversity is categorized into 5 clear tiers (Dual, Multi, Mixed, Diverse, Very Diverse)
- All metrics use human-readable bucket labels with numeric ranges in parentheses
- The dataset focuses on repositories with multiple programming languages (hence "multi_language_projects")

## Column Details

### repo_name (STRING)
- **Uniqueness:** Primary key - every value is unique (1,753,925 distinct values)
- **Format:** Follows GitHub's "owner/repository" naming convention
- **Examples:** "siostechcorp/Windows_Signal", "lindabli/startbootstrap-landing-page"
- **Query Consideration:** Ideal for exact lookups, filtering specific repositories

### language_diversity_bucket (STRING)
- **Values:** 5 distinct buckets measuring number of programming languages
  - "Dual (2)" - 2 languages
  - "Multi (3-4)" - 3-4 languages
  - "Mixed (5-9)" - 5-9 languages
  - "Diverse (10-19)" - 10-19 languages
  - "Very Diverse (20+)" - 20+ languages
- **Pattern:** Ordered categorical variable from least to most diverse
- **Query Consideration:** Excellent for grouping and filtering by language complexity

### primary_language (STRING)
- **Diversity:** 372 unique programming languages
- **Range:** Includes mainstream (C, JavaScript, Python) to niche languages (1C Enterprise, AIDL, APL)
- **Examples:** Batchfile, C, CoffeeScript, CSS, Go, Assembly, ApacheConf
- **Query Consideration:** Good for filtering by specific languages or grouping/aggregating language statistics

### primary_language_size_bucket (STRING)
- **Values:** 5 size buckets measuring bytes of primary language code
  - "Tiny (<1K)" - Less than 1,000 bytes
  - "Small (1K-9.9K)" - 1,000-9,999 bytes
  - "Medium (10K-99K)" - 10,000-99,999 bytes
  - "Large (100K-999K)" - 100,000-999,999 bytes
  - "Very Large (1M+)" - 1,000,000+ bytes
- **Pattern:** Logarithmic scale bucketing
- **Query Consideration:** Useful for analyzing projects by code size

### popularity_bucket (STRING)
- **Values:** 5 popularity tiers (likely based on stars/forks/watchers)
  - "Minimal (<10)"
  - "Low (10-99)"
  - "Moderate (100-999)"
  - "Popular (1K-9.9K)"
  - "Very Popular (10K+)"
- **Distribution:** Heavily skewed toward "Minimal" based on samples
- **Query Consideration:** Key metric for filtering high-visibility projects

### license (STRING)
- **Values:** 15 distinct open-source licenses
- **Examples:** mit, apache-2.0, lgpl-3.0, bsd-2-clause, gpl-2.0, gpl-3.0, agpl-3.0, isc, cc0-1.0, epl-1.0
- **Pattern:** Uses SPDX license identifiers in lowercase
- **Query Consideration:** Good for compliance queries and license type analysis

### activity_bucket (STRING)
- **Values:** 5 activity levels (likely commits/updates/contributions)
  - "Low (10-49)"
  - "Low-Medium (50-99)"
  - "Medium (100-999)"
  - "High (1K-9.9K)"
  - "Very High (10K+)"
- **Query Consideration:** Useful for identifying actively maintained vs. stale projects

### team_size_bucket (STRING)
- **Values:** 5 team size categories (likely based on contributors)
  - "Individual (1)" - Solo developer
  - "Pair (2-4)" - 2-4 contributors
  - "Small Team (5-19)" - 5-19 contributors
  - "Medium Team (20-99)" - 20-99 contributors
  - "Large Team (100+)" - 100+ contributors
- **Query Consideration:** Excellent for analyzing collaboration patterns and team dynamics

## Potential Query Considerations

### Good for Filtering:
- **repo_name:** Exact repository lookups
- **primary_language:** Projects in specific programming languages
- **license:** License compliance queries
- **popularity_bucket:** High-visibility or niche projects
- **language_diversity_bucket:** Polyglot vs. focused projects

### Good for Grouping/Aggregation:
- **primary_language:** Language ecosystem statistics
- **license:** License distribution analysis
- **All bucket columns:** Cross-tabulations and distribution analysis
- **team_size_bucket + activity_bucket:** Team dynamics vs. project activity
- **language_diversity_bucket + primary_language:** Language diversity patterns

### Potential Join Keys:
- **repo_name:** Can join with other GitHub dataset tables using repository name
- **primary_language:** Could join with language-specific metadata tables
- **license:** Could join with license detail tables

### Data Quality Considerations:
- All values are pre-bucketed, so range queries require bucket selection rather than numeric comparisons
- No raw numeric values available (stars, forks, LOC, etc.) - only categorical buckets
- Bucket boundaries are inclusive/exclusive, requiring careful interpretation (e.g., does "10-99" include 10 and 99?)
- Time dimension is absent - no way to filter by creation date, last update, etc.
- "Minimal (<10)" popularity dominates the dataset, suggesting a long-tail distribution

## Keywords

GitHub, repositories, multi-language, polyglot, programming languages, open source, licenses, team size, contributors, code size, repository activity, project popularity, language diversity, software projects, code metrics, project metadata, bucketed data, categorical analysis, repository statistics

## Table and Column Documentation

**Table Comment:** Not provided

**Column Comments:** Not provided