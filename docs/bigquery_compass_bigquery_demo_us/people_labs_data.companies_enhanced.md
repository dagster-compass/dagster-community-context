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

**Total Rows:** 48,628,328 companies

**General Data Quality:**
- Very large-scale business directory dataset with nearly 49 million company records
- High data completeness for core identifiers (company_id, company_name, linkedin_id all 100% populated)
- Significant sparsity in optional fields like funding data (99.61% null), social media URLs (96-97% null), and financial metrics
- Mixed data quality with some fields having structured data (arrays, nested objects) while others are free text
- Contains both individual professionals and traditional companies based on naming patterns

**Notable Patterns:**
- Predominantly small companies (1-10 employees is most common size)
- Private companies vastly outnumber public ones
- Most companies are unfunded (funding_status = "Not funded/Unknown")
- Geographic data heavily weighted toward certain regions
- Single dataset version (31.2) indicates versioned data management

## Column Details

### Core Identifiers
- **company_id** (STRING): Unique identifier, 100% populated, appears to be encoded hash
- **company_name** (STRING): Company names, 100% populated, includes individual names and business entities
- **linkedin_id** (STRING): LinkedIn company ID, 100% populated, numeric values
- **linkedin_url/linkedin_slug** (STRING): LinkedIn profile information, 100% populated

### Basic Company Information
- **display_name** (STRING): Formatted company name, 100% populated
- **website** (STRING): Company websites, 56.14% null - significant missing data
- **company_summary/company_description_full** (STRING): Descriptive text, 100% populated but varying quality
- **headline** (STRING): Short company tagline, 86.10% null

### Classification & Industry
- **industry** (STRING): 147 categories, 25.41% null - older classification system
- **industry_v2** (STRING): 434 categories, 28.49% null - newer, more granular classification
- **company_type** (STRING): 6 types (private, public, nonprofit, etc.), 100% populated
- **company_size** (STRING): 8 standardized ranges from "1-10" to "10001+", 100% populated
- **company_maturity** (STRING): 5 stages from Startup to Established, 100% populated

### Financial & Business Metrics
- **founded_year** (INT64): Range 1001-2025, 80.89% null
- **current_employee_count** (INT64): Range 0-503,423, 67.06% null
- **average_employee_tenure** (FLOAT64): Range 0.0-95.667 years, 67.06% null
- **linkedin_followers** (INT64): Range 1-35,128,123, 61.14% null
- **inferred_revenue** (STRING): 10 revenue bands, 67.06% null

### Funding Information (Very Sparse)
- **total_funding_raised** (FLOAT64): 99.61% null, when present ranges to $74B+
- **latest_funding_stage** (STRING): 27 stages, 99.61% null
- **last_funding_date** (STRING): Date strings, 99.61% null
- **count_funding_rounds** (INT64): 1-50 rounds, 99.61% null
- **funding_status** (STRING): Binary classification, 100% populated

### Corporate Structure
- **immediate_parent/ultimate_parent** (STRING): Parent company IDs, 99.78% null
- **ticker/ultimate_parent_ticker** (STRING): Stock symbols, 99.93-99.98% null
- **mic_exchange** (STRING): Exchange codes, 99.98% null

### Social Media & Web Presence
- **facebook_url** (STRING): 96.84% null
- **twitter_url** (STRING): 97.26% null

### Structured Data Arrays
- **locations** (ARRAY): Geographic information with address components, 100% populated
- **naics_codes/sic_codes** (ARRAY): Industry classification codes with hierarchical structure
- **tags** (ARRAY): Keyword tags, mostly empty arrays
- **alternative_names/alternative_domains** (ARRAY): Aliases and additional domains
- **subsidiaries** (ARRAY): Corporate relationship data
- **funding_stages** (ARRAY): Historical funding information

### Metadata
- **dataset_version** (STRING): Version "31.2", 100% populated

## Query Considerations

### Good for Filtering
- **company_size**: Well-structured categorical data
- **company_type**: Limited, clean categories
- **industry/industry_v2**: Industry-based filtering
- **company_maturity**: Business stage filtering
- **funding_status**: Funded vs unfunded companies
- **locations**: Geographic filtering via nested location data
- **founded_year**: Time-based filtering (where not null)

### Good for Grouping/Aggregation
- **company_size**: Size distribution analysis
- **industry/industry_v2**: Industry analysis
- **company_type**: Organizational type breakdowns
- **company_maturity**: Maturity stage analysis
- **locations.country/region**: Geographic aggregations
- **founded_year**: Temporal analysis

### Potential Join Keys
- **company_id**: Primary key for joins
- **immediate_parent/ultimate_parent**: Corporate hierarchy joins
- **linkedin_id**: LinkedIn data integration

### Data Quality Considerations
- High null rates in financial/funding data limit analysis scope
- Website field has 56% nulls, affecting web presence analysis
- Founded year has 81% nulls, limiting historical analysis
- Employee metrics have 67% nulls
- Social media URLs are largely missing
- Location data is nested and requires UNNEST operations
- Industry classifications have significant nulls requiring careful handling

## Keywords
company data, business directory, LinkedIn companies, startup funding, corporate structure, industry classification, employee data, geographic business data, company size, business maturity, NAICS codes, SIC codes, venture capital, private equity, corporate hierarchy, business intelligence

## Table and Column Docs
No table comment or column comments were provided in the analysis.