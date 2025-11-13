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
# Comprehensive Summary: people_labs_data.companies_enhanced

## Overall Dataset Characteristics

**Total Rows:** 48,628,328 (approximately 48.6 million companies)

**General Data Quality:** This is a large-scale company information dataset with variable completeness across fields. Core identification fields (company_id, company_name, LinkedIn data) are complete, while enrichment fields show significant null percentages. The dataset appears to be sourced primarily from LinkedIn and enhanced with additional business intelligence.

**Notable Patterns:**
- High null percentages in funding-related fields (~99.6%), indicating most companies are not venture-backed
- Moderate null percentages in employee/financial data (60-80%), suggesting limited availability of this information
- Parent company relationships are sparse (~99.8% null), indicating most companies are independent entities
- Website availability is moderate (56% null)
- Industry classification is reasonably complete (25-28% null)
- All companies have at least one location and classification code

**Dataset Version:** 31.2 (consistent across all records)

## Column-by-Column Analysis

### Identification & Core Fields

**company_id (STRING)**
- Unique identifier for each company (100% unique)
- Format: Alphanumeric hash (e.g., "ozeh6ifbR9vhfvg2jjIsBwYq0S9F")
- No nulls, perfect for primary key/filtering

**company_name (STRING)**
- Legal or common company name
- 98.8% unique (some duplicates likely due to common names)
- Format: Lowercase text (e.g., "bigeargeal madeleine")
- No nulls, excellent for text search

**display_name (STRING)**
- Formatted display version of company name
- 99.2% unique
- Format: Mixed case with proper formatting (e.g., "Tepper & Eyster, PLLC")
- No nulls, preferred for display purposes

**linkedin_id (STRING)**
- LinkedIn's internal company ID
- 100% unique, numeric string format
- No nulls, reliable for LinkedIn integration

**linkedin_url / linkedin_slug (STRING)**
- Full LinkedIn URL and slug component
- 100% unique, no nulls
- Format: "linkedin.com/company/{slug}"

### Business Classification

**industry (STRING)**
- 147 distinct values
- 25.41% null
- Broader industry categories (e.g., "computer software", "higher education")
- Good for high-level filtering

**industry_v2 (STRING)**
- 434 distinct values (more granular than industry)
- 28.49% null
- More detailed classifications (e.g., "accessible hardware manufacturing")
- Better for precise industry analysis

**company_type (STRING)**
- 6 values: educational, government, nonprofit, private, public, public_subsidiary
- No nulls
- Excellent for filtering by ownership structure

**company_size (STRING)**
- 8 buckets: 1-10, 11-50, 51-200, 201-500, 501-1000, 1001-5000, 5001-10000, 10001+
- No nulls
- Categorical size ranges, good for segmentation

**company_maturity (STRING)**
- 5 categories: Early stage, Established, Growth stage, Startup, Unknown
- No nulls
- Derived field for lifecycle stage

### Web & Social Presence

**website (STRING)**
- 21.3M unique values
- 56.14% null (over half lack website data)
- Various formats (domains without protocol)

**twitter_url (STRING)**
- 1.3M unique values
- 97.26% null (small minority have Twitter presence)
- Multiple domain formats (mobile.twitter.com, twitter.com)

**facebook_url (STRING)**
- 1.5M unique values
- 96.84% null
- Various Facebook domain formats

### Employee & Financial Metrics

**current_employee_count (INT64)**
- Range: 0 to 503,423
- 67.06% null
- 6,537 unique values
- Point-in-time employee count

**average_employee_tenure (FLOAT64)**
- Range: 0.0 to 95.667 years
- 67.06% null
- 22,481 unique values
- Useful for company stability analysis

**inferred_revenue (STRING)**
- 10 revenue buckets: $0-$1M, $1M-$10M, $10M-$25M, $25M-$50M, $50M-$100M, $100M-$250M, $250M-$500M, $500M-$1B, $1B-$10B, $10B+
- 67.06% null
- Categorical revenue estimates

**linkedin_followers (INT64)**
- Range: 1 to 35,128,123
- 61.14% null
- 54,602 unique values
- Proxy for company visibility/brand strength

### Funding Information

**funding_status (STRING)**
- 2 values: "Funded" or "Not funded/Unknown"
- No nulls
- Derived field for quick funding filter

**latest_funding_stage (STRING)**
- 27 distinct stages (angel, seed, series_a through series_unknown, IPO stages, etc.)
- 99.61% null (only 0.39% have funding data)

**last_funding_date (STRING)**
- 7,898 unique dates
- 99.61% null
- Date format string
- Range: 1900-01-01 to recent dates (some data quality issues with historical dates)

**total_funding_raised (FLOAT64)**
- Range: 0.0 to 74,015,950,500 (74B)
- 99.61% null
- 71,533 unique values

**count_funding_rounds (INT64)**
- Range: 1 to 50 rounds
- 99.61% null
- 40 unique values

**funding_stages_count (INT64)**
- Range: 1 to 18
- 99.61% null
- Count of distinct funding stages

**funding_stages (ARRAY<STRING>)**
- Array of funding stage names
- Empty arrays for unfunded companies

**funding_stages_text (STRING)**
- Concatenated string of funding stages
- 4,318 unique combinations
- 99.61% null

### Corporate Structure

**ticker (STRING)**
- Stock ticker symbol
- 10,216 unique values
- 99.98% null (only public companies)
- Various exchange suffixes (.KS, .SZ, .HK, etc.)

**mic_exchange (STRING)**
- Market Identifier Code for exchange
- 59 unique exchanges
- 99.98% null

**immediate_parent / ultimate_parent (STRING)**
- Company IDs for parent entities
- 40,086 / 33,245 unique values respectively
- 99.78% null (vast majority are independent)

**ultimate_parent_ticker (STRING)**
- Ticker of ultimate parent company
- 4,472 unique values
- 99.93% null

**direct_subsidiaries_count (INT64)**
- Range: 1 to 271
- 99.92% null
- 97 unique values

**all_subsidiaries_count (INT64)**
- Range: 1 to 633
- 99.92% null
- 130 unique values

**direct_subsidiaries / all_subsidiaries (ARRAY<STRING>)**
- Arrays of subsidiary company IDs
- Empty for non-parent companies

### Temporal Information

**founded_year (INT64)**
- Range: 1001 to 2025
- 80.89% null
- 963 unique values
- Note: Historical dates (1001-1900s) may indicate data quality issues

### Descriptive Fields

**company_summary (STRING)**
- 48.6M unique values (nearly unique per company)
- No nulls
- Format: Brief description with industry and size (e.g., "cherrystones to-go (Cherrystones To-Go). Industry: restaurants. Size: 11-50")

**company_description_full (STRING)**
- 48.6M unique values
- No nulls
- Extended description with additional details
- Often truncated in samples

**headline (STRING)**
- 6.6M unique values
- 86.10% null
- Short tagline or headline

**summary (STRING)**
- 14.6M unique values
- 69.45% null
- More detailed summary than company_summary

### Classification Codes

**naics_codes (ARRAY<STRUCT>)**
- North American Industry Classification System codes
- No nulls (empty arrays for unclassified)
- Struct fields: naics_code, sector, sub_sector, industry_group, naics_industry, national_industry
- All struct fields can be null

**naics_codes_count (INT64)**
- Range: 1 to 1,000
- No nulls
- 113 unique values

**sic_codes (ARRAY<STRUCT>)**
- Standard Industrial Classification codes
- No nulls (empty arrays for unclassified)
- Struct fields: sic_code, industry_sector, major_group, industry_group
- All struct fields can be null

**sic_codes_count (INT64)**
- Range: 1 to 1,000
- No nulls
- 113 unique values

### Geographic Information

**locations (ARRAY<STRUCT>)**
- No nulls (every company has at least 1 location)
- Struct fields: street_address, postal_code, region, locality, metro, country, name, geo, continent, address_line_2
- Fields within struct can be null

**locations_count (INT64)**
- Range: 1 to 10
- No nulls
- 10 unique values (capped at 10 locations)

**top_us_employee_metros (ARRAY<STRUCT>)**
- US-specific employee distribution by metro area
- Struct fields: metro, headcount, growth_rate_12_month
- Often contains single null struct element

### Alternative Identifiers

**tags (ARRAY<STRING>)**
- Descriptive tags/keywords
- No nulls (empty arrays when no tags)

**tags_text (STRING)**
- Concatenated string of tags
- 5.5M unique values
- 88.29% null

**tags_count (INT64)**
- Range: 1 to 10
- 88.29% null

**alternative_names (ARRAY<STRING>)**
- Other names for the company
- No nulls (empty arrays when none)

**alternative_names_text (STRING)**
- Concatenated alternative names
- 990,572 unique values
- 97.95% null

**alternative_names_count (INT64)**
- Range: 1 to 10
- 97.95% null

**alternative_domains (ARRAY<STRING>)**
- Additional web domains
- No nulls (empty arrays when none)

**alternative_domains_count (INT64)**
- Range: 1 to 10
- 92.86% null

## Query Considerations

### Excellent for Filtering:
- **company_type**: Clean categorical values, no nulls
- **company_size**: Standardized buckets, no nulls
- **company_maturity**: Lifecycle stage, no nulls
- **funding_status**: Binary funded/unfunded, no nulls
- **industry / industry_v2**: Reasonable coverage (70-75%)
- **country** (from locations array): Geographic filtering
- **dataset_version**: Version control

### Good for Grouping/Aggregation:
- **industry / industry_v2**: Category analysis
- **company_size**: Size distribution
- **company_type**: Ownership analysis
- **company_maturity**: Lifecycle analysis
- **inferred_revenue**: Revenue segmentation
- **founded_year**: Temporal trends (where available)
- **country/region** (from locations): Geographic analysis

### Potential Join Keys:
- **company_id**: Primary key
- **linkedin_id**: LinkedIn integration
- **immediate_parent / ultimate_parent**: Corporate hierarchy
- **ticker / ultimate_parent_ticker**: Stock market data
- Direct/all subsidiaries arrays: Relationship mapping

### Data Quality Considerations:

**High Completeness (good for queries):**
- Core identifiers (company_id, names, LinkedIn fields)
- Classification fields (type, size, maturity)
- Location data (all have at least 1)
- Industry codes structures (NAICS/SIC arrays present)

**Limited Completeness (use with caution):**
- Funding data (~99.6% null) - only for funded companies
- Parent relationships (~99.8% null) - only for subsidiaries
- Website (~56% null)
- Employee/financial metrics (~67% null)
- Founded year (~81% null)
- Social media URLs (~97% null)

**Data Quality Issues:**
- Founded_year has implausible historical dates (1001)
- Last_funding_date has dates from 1900
- Some text fields may be truncated
- Industry classification has nulls in 25-28% of records
- NAICS/SIC code structs often have all null fields despite array being non-null

### Performance Tips:
- Use company_id for point lookups (unique, indexed)
- Filter on non-null categorical fields first (type, size, maturity)
- Be aware of array operations on locations, subsidiaries, funding_stages
- Consider null percentages when joining or filtering on enrichment fields
- Website field useful but only available for ~44% of records

## Keywords

company data, business intelligence, LinkedIn companies, corporate database, company profiles, funding data, venture capital, employee data, industry classification, NAICS codes, SIC codes, company size, revenue data, corporate hierarchy, subsidiaries, parent companies, stock tickers, company locations, business metadata, company enrichment, B2B data, firmographics, company maturity, startup data, private companies, public companies, company website, social media presence, company founding date, employee count, employee tenure, company growth

## Table and Column Docs

**Table Comment:** Not provided

**Column Comments:** No column-level comments are present in this dataset. All columns lack explicit documentation within the schema.