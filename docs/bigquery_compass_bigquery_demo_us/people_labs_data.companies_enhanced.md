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
# Table Summary: people_labs_data.companies_enhanced

## Overall Dataset Characteristics

- **Total Rows**: 48,628,328 companies
- **Data Quality**: High-quality structured company data with consistent formatting across core fields
- **Notable Patterns**: 
  - Heavy skew toward small companies (majority are 1-10 employees)
  - Most companies lack detailed financial/funding information (99%+ null for funding fields)
  - Geographic diversity with global company coverage
  - Strong LinkedIn integration with complete LinkedIn data for all companies
- **Dataset Version**: 31.2 (consistent across all records)

## Column Details

### Core Identifiers
- **company_id** (STRING): Unique identifier, 0% null, 48M+ unique values
- **linkedin_id** (STRING): LinkedIn company ID, 0% null, always populated
- **linkedin_url** (STRING): Complete LinkedIn URLs, 0% null
- **linkedin_slug** (STRING): URL-friendly company names, 0% null

### Basic Company Information
- **company_name** (STRING): Primary company names, 0% null, mostly unique (48M+ values)
- **display_name** (STRING): Formatted display names, 0% null
- **company_summary** (STRING): Brief company descriptions with size info, 0% null
- **company_description_full** (STRING): Extended descriptions, 0% null
- **website** (STRING): Company websites, 56% null (21M+ unique domains when present)

### Company Classification
- **company_type** (STRING): 6 categories - private (dominant), public, nonprofit, educational, government, public_subsidiary
- **company_size** (STRING): 8 size brackets from "1-10" to "10001+", most companies are "1-10"
- **industry** (STRING): 147 industry categories, 25% null
- **industry_v2** (STRING): More granular 434 industry categories, 28% null
- **company_maturity** (STRING): 5 stages - Unknown (dominant), Startup, Early stage, Growth stage, Established

### Financial & Funding Data (Highly Sparse)
- **founded_year** (INT64): Year founded, 81% null, range 1001-2025
- **current_employee_count** (INT64): Employee count, 67% null, range 0-503,423
- **inferred_revenue** (STRING): Revenue brackets, 67% null, 10 categories from "$0-$1M" to "$10B+"
- **total_funding_raised** (FLOAT64): Funding amounts, 99.6% null
- **funding_status** (STRING): "Funded" vs "Not funded/Unknown" (dominant)
- **latest_funding_stage**, **last_funding_date**, **count_funding_rounds**: All 99.6% null

### Social Media & Online Presence
- **facebook_url** (STRING): 97% null when present
- **twitter_url** (STRING): 97% null when present
- **linkedin_followers** (INT64): 61% null, range 1-35M+ when present

### Corporate Structure (Very Sparse)
- **ticker** (STRING): Stock symbols, 99.98% null
- **immediate_parent**, **ultimate_parent**: Parent company IDs, 99.78% null
- **mic_exchange**, **ultimate_parent_mic_exchange**: Stock exchanges, 99.9%+ null

### Geographic & Structured Data
- **locations** (ARRAY): Geographic data with address components, always populated (1-10 locations)
- **naics_codes**, **sic_codes** (ARRAYS): Industry classification codes, structured but often null values within
- **tags** (ARRAY): Company tags, 88% have no tags
- **alternative_names**, **alternative_domains**: Additional identifiers, mostly empty

### Count Fields
- Multiple "_count" fields tracking array sizes (locations_count, naics_codes_count, etc.)
- Most count fields are heavily null except locations_count and classification code counts

## Query Considerations

### Good for Filtering
- **company_type**: Well-distributed categorical values
- **company_size**: Clear size brackets for filtering
- **industry/industry_v2**: Industry-based filtering (when not null)
- **company_maturity**: Maturity stage filtering
- **funding_status**: Funded vs non-funded companies
- **founded_year**: Date range filtering (when not null)

### Good for Grouping/Aggregation
- **company_size**: Size distribution analysis
- **industry/industry_v2**: Industry analysis
- **company_type**: Organizational type analysis
- **locations.country/region**: Geographic analysis
- **founded_year**: Temporal analysis

### Potential Join Keys
- **company_id**: Primary key for joining with other company tables
- **linkedin_id**: Alternative join key for LinkedIn-based datasets
- **ticker**: For joining with financial/stock data (very limited coverage)
- **website**: For web-based company matching

### Data Quality Considerations
- High null percentages in financial/funding fields limit financial analysis
- Website field has 56% nulls, limiting web presence analysis
- Industry classification has 25-28% nulls
- Founded year has 81% nulls, limiting age-based analysis
- Most valuable for basic company profiling and size/type distribution analysis

## Keywords
company data, business intelligence, LinkedIn companies, company profiles, industry classification, company size, funding data, geographic business data, corporate structure, NAICS codes, SIC codes, business directory

## Table and Column Docs
No table comment or column comments were provided in the analysis.