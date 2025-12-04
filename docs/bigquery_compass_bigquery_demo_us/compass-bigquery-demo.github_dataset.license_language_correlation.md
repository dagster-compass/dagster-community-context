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
# Comprehensive Table Summary: license_language_correlation

## Overall Dataset Characteristics

**Total Rows:** 1,502

**General Description:** This table captures the relationships between open-source software licenses and programming languages in GitHub repositories, enriched with various project metrics bucketed into categorical ranges. The dataset provides a multidimensional view of how different licenses correlate with language choices, project popularity, team composition, and community engagement.

**Data Quality:** Excellent - all columns show 0% null values, indicating complete data coverage across all records. The data is well-structured with categorical buckets making it suitable for aggregation and pattern analysis.

**Notable Patterns:**
- All metrics are pre-bucketed into categorical ranges (e.g., "Low", "Medium", "High")
- The dataset captures diverse combinations of 15 licenses and 259 programming languages
- Most combinations appear to fall into lower popularity/adoption ranges based on sample data
- "Minimal (<5%)" license share appears frequently in samples, suggesting most language-license combinations represent niche cases

## Column Details

### license (STRING)
- **Data Type:** Categorical identifier
- **Null Values:** None (0%)
- **Unique Values:** 15 distinct open-source licenses
- **Common Values:** apache-2.0, gpl-2.0, bsd-3-clause, bsd-2-clause, gpl-3.0, agpl-3.0, cc0-1.0, epl-1.0, isc, artistic-2.0
- **Characteristics:** Standard SPDX license identifiers for popular open-source licenses
- **Use Case:** Primary dimension for license-based analysis and filtering

### primary_language (STRING)
- **Data Type:** Categorical identifier
- **Null Values:** None (0%)
- **Unique Values:** 259 distinct programming languages
- **Sample Values:** C++, OCaml, Handlebars, C#, Smarty, Stata, GLSL, Jinja
- **Characteristics:** Wide variety from mainstream (C++, C#) to specialized languages (Stata, GLSL, Handlebars)
- **Use Case:** Key dimension for language-based analysis and segmentation

### adoption_level_bucket (STRING)
- **Data Type:** Categorical range
- **Null Values:** None (0%)
- **Unique Values:** 5 buckets
- **Distribution:** Low (10-49), Low-Medium (50-99), Medium (100-999), High (1K-9.9K), Very High (10K+)
- **Characteristics:** Logarithmic scale suggesting repository count or adoption metric
- **Use Case:** Filtering for widely-adopted vs. niche combinations

### popularity_bucket (STRING)
- **Data Type:** Categorical range
- **Null Values:** None (0%)
- **Unique Values:** 4 buckets
- **Distribution:** Minimal (<10), Low (10-99), Moderate (100-999), Popular (1K-9.9K)
- **Sample Pattern:** Predominantly "Low" and "Minimal" in samples
- **Characteristics:** Likely measures stars, forks, or engagement metrics
- **Use Case:** Identifying popular vs. obscure project combinations

### activity_bucket (STRING)
- **Data Type:** Categorical range
- **Null Values:** None (0%)
- **Unique Values:** 5 buckets
- **Distribution:** Low (<50), Low-Medium (50-99), Medium (100-999), High (1K-9.9K), Very High (10K+)
- **Sample Pattern:** Mix of Low, Medium, and High in samples
- **Characteristics:** Likely represents commit count, issue activity, or contribution frequency
- **Use Case:** Analyzing active vs. dormant project patterns

### team_size_bucket (STRING)
- **Data Type:** Categorical range
- **Null Values:** None (0%)
- **Unique Values:** 5 buckets
- **Distribution:** Individual (1), Pair (2-4), Small Team (5-19), Medium Team (20-99), Large Team (100+)
- **Sample Pattern:** Frequently "Small Team" and "Pair" in samples
- **Characteristics:** Represents contributor count per project
- **Use Case:** Understanding collaboration patterns by license/language

### diversity_bucket (STRING)
- **Data Type:** Categorical range
- **Null Values:** None (0%)
- **Unique Values:** 5 buckets
- **Distribution:** Single (1), Dual (2), Mixed (3-4), Diverse (5-9), Very Diverse (10+)
- **Sample Pattern:** Often "Single", "Dual", or "Diverse" in samples
- **Characteristics:** Likely measures number of languages or technologies in projects
- **Use Case:** Analyzing polyglot vs. monolingual projects

### license_share_bucket (STRING)
- **Data Type:** Categorical range
- **Null Values:** None (0%)
- **Unique Values:** 4 buckets
- **Distribution:** Trace (5-9%), Minimal (<5%), Minor (10-24%), Major (25-49%)
- **Sample Pattern:** Predominantly "Minimal (<5%)" in samples
- **Characteristics:** Percentage share of license usage within the language ecosystem
- **Use Case:** Identifying dominant vs. rare license-language pairings

## Potential Query Considerations

### Excellent for Filtering:
- **license**: Perfect for license-specific analysis (e.g., "apache-2.0 vs. gpl-3.0 adoption")
- **primary_language**: Great for language-specific queries (e.g., "Java projects" or "C++ licenses")
- **popularity_bucket**: Ideal for filtering high-visibility projects
- **adoption_level_bucket**: Useful for finding mainstream vs. niche combinations

### Excellent for Grouping/Aggregation:
- All bucket columns are pre-categorized for aggregation
- **license + primary_language**: Core combination for correlation analysis
- **license_share_bucket**: Understanding license dominance patterns
- **team_size_bucket + activity_bucket**: Analyzing community health

### Potential Join Keys:
- **license**: Could join with license details tables (restrictions, permissions, conditions)
- **primary_language**: Could join with language characteristics tables (paradigm, popularity trends)
- No obvious numeric IDs present; this appears to be a summary/aggregation table

### Query Patterns to Consider:

**Comparative Analysis:**
```sql
-- Compare Apache vs GPL adoption across languages
WHERE license IN ('apache-2.0', 'gpl-3.0')
GROUP BY primary_language, license
```

**Popularity Filtering:**
```sql
-- Find highly adopted, popular combinations
WHERE adoption_level_bucket IN ('High (1K-9.9K)', 'Very High (10K+)')
  AND popularity_bucket IN ('Moderate (100-999)', 'Popular (1K-9.9K)')
```

**Team Size Analysis:**
```sql
-- Large team projects by license
WHERE team_size_bucket IN ('Medium Team (20-99)', 'Large Team (100+)')
GROUP BY license
```

### Data Quality Considerations:
- **Bucketed Data:** All metrics are pre-aggregated; no raw numbers available for precise calculations
- **Range Overlaps:** Need to parse bucket strings carefully for ordering (e.g., "Low (10-49)" vs "Very High (10K+)")
- **Sample Bias:** "Minimal (<5%)" license share dominance suggests many rare combinations
- **No Timestamps:** Unable to track trends over time
- **No Repository IDs:** Cannot drill down to individual projects

## Keywords

open source, licenses, SPDX, Apache, GPL, BSD, programming languages, GitHub, repository analysis, license adoption, language correlation, software metrics, team size, project popularity, code activity, contributor diversity, license distribution, polyglot projects, open source metrics, software licensing patterns, language ecosystems, project categorization, community metrics, collaboration patterns

## Table and Column Documentation

**Table Comment:** Not provided in the analysis report.

**Column Comments:** No individual column comments were provided in the analysis report.