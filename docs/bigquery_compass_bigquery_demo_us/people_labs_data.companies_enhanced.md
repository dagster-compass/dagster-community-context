---
columns:
- all_subsidiaries (ARRAY<STRING>)
- all_subsidiaries_count (INT64)
- alternative_domains (ARRAY<STRING>)
- alternative_domains_count (INT64)
- alternative_names (ARRAY<STRING>)
- alternative_names_count (INT64)
- alternative_names_text (STRING)
- average_employee_tenure (FLOAT64)
- company_description_full (STRING)
- company_id (STRING)
- company_maturity (STRING)
- company_name (STRING)
- company_size (STRING)
- company_summary (STRING)
- company_type (STRING)
- count_funding_rounds (INT64)
- current_employee_count (INT64)
- dataset_version (STRING)
- direct_subsidiaries (ARRAY<STRING>)
- direct_subsidiaries_count (INT64)
- display_name (STRING)
- facebook_url (STRING)
- founded_year (INT64)
- funding_stages (ARRAY<STRING>)
- funding_stages_count (INT64)
- funding_stages_text (STRING)
- funding_status (STRING)
- headline (STRING)
- immediate_parent (STRING)
- industry (STRING)
- industry_v2 (STRING)
- inferred_revenue (STRING)
- last_funding_date (STRING)
- latest_funding_stage (STRING)
- linkedin_followers (INT64)
- linkedin_id (STRING)
- linkedin_slug (STRING)
- linkedin_url (STRING)
- locations (ARRAY<STRUCT<street_address STRING, postal_code STRING, region STRING,
  locality STRING, metro STRING, country STRING, name STRING, geo STRING, continent
  STRING, address_line_2 STRING>>)
- locations_count (INT64)
- mic_exchange (STRING)
- naics_codes (ARRAY<STRUCT<naics_code STRING, sector STRING, sub_sector STRING, industry_group
  STRING, naics_industry STRING, national_industry STRING>>)
- naics_codes_count (INT64)
- sic_codes (ARRAY<STRUCT<sic_code STRING, industry_sector STRING, major_group STRING,
  industry_group STRING>>)
- sic_codes_count (INT64)
- summary (STRING)
- tags (ARRAY<STRING>)
- tags_count (INT64)
- tags_text (STRING)
- ticker (STRING)
- top_us_employee_metros (ARRAY<STRUCT<metro STRING, headcount FLOAT64, growth_rate_12_month
  FLOAT64>>)
- total_funding_raised (FLOAT64)
- twitter_url (STRING)
- ultimate_parent (STRING)
- ultimate_parent_mic_exchange (STRING)
- ultimate_parent_ticker (STRING)
- website (STRING)
schema_hash: c94c9391acc98ca6b96da846bde73f8bcd396a71e1ffe6849c50ef44934cc6f5

---
# Companies Enhanced Dataset Summary

## Overall Dataset Characteristics

- **Total Rows**: 48,628,328 companies
- **Data Quality**: Very comprehensive dataset with virtually no null values in key identifier fields (company_id, company_name, linkedin_id)
- **Coverage**: Global dataset with extensive LinkedIn-sourced company information
- **Notable Patterns**: 
  - Heavy skew toward small companies (1-10 employees)
  - Most companies lack funding information (99.61% null)
  - Sparse data for financial metrics and parent company relationships
  - Dataset version 31.2 indicates this is a versioned, maintained dataset

## Column Details

### Core Identifiers
- **company_id** (STRING): Unique identifier for each company, 100% populated, fully unique (48.6M values)
- **company_name** (STRING): Primary company name, 100% populated, nearly unique (48M distinct values)
- **linkedin_id** (STRING): LinkedIn company ID, 100% populated, fully unique
- **linkedin_url** (STRING): LinkedIn company URL, 100% populated, fully unique
- **linkedin_slug** (STRING): LinkedIn URL slug, 100% populated, fully unique

### Company Profile Data
- **display_name** (STRING): Formatted company name for display, 100% populated
- **website** (STRING): Company website, 43.86% populated (21.3M values)
- **company_summary** (STRING): Brief company description, 100% populated
- **company_description_full** (STRING): Detailed company description, 100% populated
- **headline** (STRING): Company tagline/headline, 13.90% populated
- **summary** (STRING): Extended company summary, 30.55% populated

### Company Classification
- **company_type** (STRING): 6 categories - private (dominant), public, nonprofit, government, educational, public_subsidiary
- **company_size** (STRING): 8 size ranges from "1-10" to "10001+", with "1-10" being most common
- **industry** (STRING): 147 industry categories, 74.59% populated
- **industry_v2** (STRING): More detailed industry classification with 434 categories, 71.51% populated
- **founded_year** (INT64): Year founded, 19.11% populated, ranges 1001-2025

### Employee & Financial Metrics
- **current_employee_count** (INT64): Current headcount, 32.94% populated, ranges 0-503,423
- **average_employee_tenure** (FLOAT64): Employee tenure in years, 32.94% populated, ranges 0.0-95.667
- **linkedin_followers** (INT64): LinkedIn follower count, 38.86% populated, ranges 1-35.1M
- **inferred_revenue** (STRING): Revenue estimates in 10 buckets from "$0-$1M" to "$10B+", 32.94% populated

### Funding Information (Very Sparse)
- **latest_funding_stage** (STRING): 27 funding stages, 0.39% populated
- **last_funding_date** (STRING): Last funding date, 0.39% populated
- **total_funding_raised** (FLOAT64): Total funding amount, 0.39% populated
- **count_funding_rounds** (INT64): Number of funding rounds, 0.39% populated
- **funding_status** (STRING): Either "Funded" or "Not funded/Unknown", 100% populated
- **company_maturity** (STRING): 5 categories - Unknown, Startup, Early stage, Growth stage, Established

### Corporate Structure (Very Sparse)
- **immediate_parent** (STRING): Direct parent company ID, 0.22% populated
- **ultimate_parent** (STRING): Ultimate parent company ID, 0.22% populated
- **ticker** (STRING): Stock ticker symbol, 0.02% populated (10K values)
- **ultimate_parent_ticker** (STRING): Parent company ticker, 0.07% populated

### Social Media & External Links
- **facebook_url** (STRING): Facebook URL, 3.16% populated
- **twitter_url** (STRING): Twitter URL, 2.74% populated

### Location & Classification Arrays
- **locations** (ARRAY): Geographic locations with full address details, 100% populated
- **naics_codes** (ARRAY): NAICS classification codes with hierarchical industry data
- **sic_codes** (ARRAY): SIC classification codes with industry groupings
- **tags** (ARRAY): Company tags/keywords, populated for 11.71% of companies

### Alternative Data
- **alternative_names** (ARRAY): Alternative company names, 2.05% populated
- **alternative_domains** (ARRAY): Alternative website domains, 7.14% populated
- **direct_subsidiaries** (ARRAY): Direct subsidiary company IDs, 0.08% populated
- **all_subsidiaries** (ARRAY): All subsidiary company IDs, 0.08% populated

### Count Fields
Multiple count fields track array sizes:
- **locations_count**: Always ≥1, max 10
- **naics_codes_count**: Always ≥1, max 1000
- **sic_codes_count**: Always ≥1, max 1000
- **tags_count**: 11.71% populated, max 10

## Potential Query Considerations

### Good for Filtering
- **company_size**: Well-distributed categorical values
- **company_type**: Good categorical distribution
- **industry/industry_v2**: Industry-based filtering
- **founded_year**: Time-based filtering (though sparse)
- **funding_status**: Binary classification
- **company_maturity**: Company lifecycle filtering
- **locations.country**: Geographic filtering via array

### Good for Grouping/Aggregation
- **company_size**: Size-based analysis
- **industry/industry_v2**: Industry analysis
- **company_type**: Organizational type analysis
- **founded_year**: Temporal analysis
- **locations.country/region**: Geographic analysis
- **inferred_revenue**: Revenue tier analysis
- **company_maturity**: Lifecycle stage analysis

### Potential Join Keys
- **company_id**: Primary key for joins
- **immediate_parent/ultimate_parent**: Corporate hierarchy joins
- **linkedin_id**: LinkedIn-specific joins

### Data Quality Considerations
- High null rates in funding data (99.61%) - filter carefully
- Website field 56% null - verify availability before using
- Financial metrics (revenue, employee count) only 33% populated
- Founded year very sparse (19% populated)
- Industry classifications have different null patterns
- Array fields require UNNEST operations for filtering/grouping
- Geographic data in nested location arrays requires careful handling

## Keywords
Company data, LinkedIn companies, business intelligence, corporate database, company profiles, B2B data, enterprise data, startup data, funding data, employee data, industry classification, NAICS codes, SIC codes, company size, revenue data, corporate hierarchy, business directory

## Table and Column Docs
No table comment or column comments were provided in the analysis.