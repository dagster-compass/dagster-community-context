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

### Scale and Quality
- **Total Rows**: 48,628,328 companies
- **Dataset Version**: 31.2 (uniform across all records)
- **Primary Key**: `company_id` (100% unique, no nulls)
- **Data Completeness**: Highly variable by field, ranging from 0% null (core identifiers) to 99.98% null (specialized fields like ticker symbols)

### Key Observations
- **Core Company Data**: All records have basic identifiers (company_id, company_name, LinkedIn data), but enrichment data varies significantly
- **Funding Data Sparsity**: 99.61% of companies have no funding information, indicating this is a comprehensive business directory rather than just funded startups
- **Employee Data Coverage**: Only 32.94% of companies have current employee counts
- **Geographic Focus**: Global dataset with location data for all companies (locations_count ranges 1-10)
- **Industry Classification**: Multiple classification systems (industry, industry_v2, SIC codes, NAICS codes) with varying completeness

### Data Quality Patterns
- Strong consistency in identifier fields (0% nulls)
- High null rates in premium/enrichment fields (funding, financial, corporate structure)
- Nested array structures for multi-valued attributes (locations, subsidiaries, codes)

---

## Column-by-Column Analysis

### **Core Identifiers**

#### `company_id` (STRING)
- **Nulls**: 0.00%
- **Uniqueness**: 100% unique (48,628,328 distinct values)
- **Format**: Alphanumeric hash (e.g., "vrgVPYcYm5jgebgm0x5jXgBZI6IU")
- **Usage**: Primary key for the table

#### `company_name` (STRING)
- **Nulls**: 0.00%
- **Uniqueness**: 98.84% unique (48,063,385 distinct values)
- **Format**: Lowercase company names
- **Examples**: "sci zatca", "national service & investigations"
- **Notes**: Some duplication indicates companies with same names but different entities

#### `display_name` (STRING)
- **Nulls**: 0.00%
- **Uniqueness**: 99.19% unique
- **Format**: Proper case/formatted company names
- **Examples**: "TRINH, TIEN DINH", "B & Z LOGISTICS INC", "iOSBFree"
- **Notes**: More human-readable than company_name

### **LinkedIn Data (100% Coverage)**

#### `linkedin_id` (STRING)
- **Nulls**: 0.00%
- **Uniqueness**: 100% unique
- **Format**: Numeric string (e.g., "44786191")

#### `linkedin_url` (STRING)
- **Nulls**: 0.00%
- **Format**: Full LinkedIn URL with company path

#### `linkedin_slug` (STRING)
- **Nulls**: 0.00%
- **Format**: URL-friendly slug identifier

#### `linkedin_followers` (INT64)
- **Nulls**: 61.14%
- **Range**: 1 to 35,128,123
- **Distribution**: Heavily right-skewed (most companies have low follower counts)

### **Company Descriptions**

#### `company_summary` (STRING)
- **Nulls**: 0.00%
- **Uniqueness**: 99.996% unique
- **Content**: Structured summary including company name, industry, size, employee count
- **Format**: Often truncated with "(truncated)" indicator

#### `company_description_full` (STRING)
- **Nulls**: 0.00%
- **Content**: Extended description with location and industry details
- **Pattern**: Many contain ". . . Industry: Unknown. " for companies without classified industries

#### `summary` (STRING)
- **Nulls**: 69.45%
- **Content**: Free-text company descriptions when available

#### `headline` (STRING)
- **Nulls**: 86.10%
- **Content**: Short tagline or description

### **Company Classification**

#### `company_type` (STRING)
- **Nulls**: 0.00%
- **Values**: private, public, nonprofit, government, educational, public_subsidiary
- **Distribution**: Heavily skewed toward "private"

#### `company_size` (STRING)
- **Nulls**: 0.00%
- **Values**: 1-10, 11-50, 51-200, 201-500, 501-1000, 1001-5000, 5001-10000, 10001+
- **Pattern**: Categorical size ranges

#### `company_maturity` (STRING)
- **Nulls**: 0.00%
- **Values**: Unknown, Startup, Early stage, Growth stage, Established
- **Distribution**: Dominated by "Unknown"

#### `funding_status` (STRING)
- **Nulls**: 0.00%
- **Values**: "Not funded/Unknown" (dominant), "Funded"

### **Industry Classifications**

#### `industry` (STRING)
- **Nulls**: 25.41%
- **Unique Values**: 147 distinct industries
- **Examples**: accounting, airlines/aviation, automotive, architecture & planning

#### `industry_v2` (STRING)
- **Nulls**: 28.49%
- **Unique Values**: 434 distinct industries
- **Format**: More granular classification than `industry`
- **Examples**: "it services and it consulting", "facilities services"

### **Employee Metrics**

#### `current_employee_count` (INT64)
- **Nulls**: 67.06%
- **Range**: 0 to 503,423
- **Distribution**: Includes zero-employee companies

#### `average_employee_tenure` (FLOAT64)
- **Nulls**: 67.06%
- **Range**: 0.0 to 95.667 years
- **Precision**: Three decimal places

### **Financial Data**

#### `inferred_revenue` (STRING)
- **Nulls**: 67.06%
- **Values**: Revenue ranges from "$0-$1M" to "$10B+"
- **Format**: Categorical revenue buckets

#### `founded_year` (INT64)
- **Nulls**: 80.89%
- **Range**: 1001 to 2025
- **Notes**: Some historical anomalies (year 1001) suggest data quality issues

### **Funding Information (Sparse)**

#### `total_funding_raised` (FLOAT64)
- **Nulls**: 99.61%
- **Range**: 0.0 to 74,015,950,500
- **Notes**: Only 0.39% of companies have funding data

#### `latest_funding_stage` (STRING)
- **Nulls**: 99.61%
- **Values**: angel, seed, series_a through series_unknown, corporate_round, debt_financing, etc.

#### `last_funding_date` (STRING)
- **Nulls**: 99.61%
- **Format**: Date string (e.g., "1900-01-01")
- **Range**: Some anomalous early dates (1900-1970)

#### `count_funding_rounds` (INT64)
- **Nulls**: 99.61%
- **Range**: 1 to 50

#### `funding_stages_count` (INT64)
- **Nulls**: 99.61%
- **Range**: 1 to 18

### **Corporate Structure**

#### `immediate_parent` (STRING)
- **Nulls**: 99.78%
- **Format**: Company ID hash
- **Usage**: Links to parent company record

#### `ultimate_parent` (STRING)
- **Nulls**: 99.78%
- **Format**: Company ID hash
- **Usage**: Links to top-level parent

#### `ticker` (STRING)
- **Nulls**: 99.98%
- **Unique Values**: 10,216 tickers
- **Format**: Stock exchange ticker symbols (e.g., "000040.KS")

#### `ultimate_parent_ticker` (STRING)
- **Nulls**: 99.93%
- **Unique Values**: 4,472 tickers

#### `mic_exchange` (STRING)
- **Nulls**: 99.98%
- **Values**: 59 stock exchange codes (e.g., "xams", "xasx")

#### `direct_subsidiaries_count` (INT64)
- **Nulls**: 99.92%
- **Range**: 1 to 271

#### `all_subsidiaries_count` (INT64)
- **Nulls**: 99.92%
- **Range**: 1 to 633

### **Web Presence**

#### `website` (STRING)
- **Nulls**: 56.14%
- **Unique Values**: 21,328,540
- **Format**: Domain names without protocol

#### `facebook_url` (STRING)
- **Nulls**: 96.84%
- **Format**: Facebook URLs (various subdomains)

#### `twitter_url` (STRING)
- **Nulls**: 97.26%
- **Format**: Twitter/X URLs

### **Count Fields**

#### `locations_count` (INT64)
- **Nulls**: 0.00%
- **Range**: 1 to 10
- **Distribution**: All companies have at least one location

#### `tags_count` (INT64)
- **Nulls**: 88.29%
- **Range**: 1 to 10

#### `alternative_names_count` (INT64)
- **Nulls**: 97.95%
- **Range**: 1 to 10

#### `alternative_domains_count` (INT64)
- **Nulls**: 92.86%
- **Range**: 1 to 10

#### `sic_codes_count` (INT64)
- **Nulls**: 0.00%
- **Range**: 1 to 1000
- **Notes**: All companies have at least one SIC code

#### `naics_codes_count` (INT64)
- **Nulls**: 0.00%
- **Range**: 1 to 1000
- **Notes**: All companies have at least one NAICS code

### **Text Aggregations**

#### `tags_text` (STRING)
- **Nulls**: 88.29%
- **Content**: Comma or delimiter-separated tag values

#### `alternative_names_text` (STRING)
- **Nulls**: 97.95%
- **Content**: Delimited alternative company names

#### `funding_stages_text` (STRING)
- **Nulls**: 99.61%
- **Content**: Comma-separated funding stages

### **Array/Nested Structures**

#### `tags` (ARRAY<STRING>)
- **Nulls**: 0.00%
- **Content**: Empty arrays common for companies without tags
- **Structure**: Simple string array

#### `alternative_names` (ARRAY<STRING>)
- **Nulls**: 0.00%
- **Content**: Alternative company name variations

#### `alternative_domains` (ARRAY<STRING>)
- **Nulls**: 0.00%
- **Content**: Alternative website domains

#### `funding_stages` (ARRAY<STRING>)
- **Nulls**: 0.00%
- **Content**: List of funding stages company has gone through

#### `direct_subsidiaries` (ARRAY<STRING>)
- **Nulls**: 0.00%
- **Content**: Company IDs of direct subsidiaries

#### `all_subsidiaries` (ARRAY<STRING>)
- **Nulls**: 0.00%
- **Content**: Company IDs of all subsidiaries (recursive)

#### `locations` (ARRAY<STRUCT>)
- **Nulls**: 0.00%
- **Structure**: Contains street_address, postal_code, region, locality, metro, country, name, geo, continent, address_line_2
- **Notes**: At least one location per company; geo coordinates provided

#### `sic_codes` (ARRAY<STRUCT>)
- **Nulls**: 0.00%
- **Structure**: sic_code, industry_sector, major_group, industry_group
- **Notes**: Often contains null values within struct for unclassified companies

#### `naics_codes` (ARRAY<STRUCT>)
- **Nulls**: 0.00%
- **Structure**: naics_code, sector, sub_sector, industry_group, naics_industry, national_industry
- **Notes**: Often contains null values within struct for unclassified companies

#### `top_us_employee_metros` (ARRAY<STRUCT>)
- **Nulls**: 0.00%
- **Structure**: metro, headcount, growth_rate_12_month
- **Notes**: Often contains single null struct for non-US or untracked companies

---

## Query Considerations

### **Best Columns for Filtering**

1. **Company Classification**:
   - `company_type` (6 distinct values, 0% null)
   - `company_size` (8 distinct values, 0% null)
   - `company_maturity` (5 distinct values, 0% null)
   - `funding_status` (2 distinct values, 0% null)

2. **Industry**:
   - `industry` (147 values, 25% null)
   - `industry_v2` (434 values, 28% null)

3. **Geographic** (via `locations` array):
   - country, region, locality fields
   - continent field

4. **Financial**:
   - `inferred_revenue` (revenue range buckets)
   - `ticker` IS NOT NULL for public companies

5. **Funding**:
   - `latest_funding_stage`
   - `funding_status`

### **Best Columns for Aggregation/Grouping**

1. **Categorical Aggregations**:
   - `company_size`, `company_type`, `company_maturity`
   - `industry`, `industry_v2`
   - `inferred_revenue`
   - `founded_year` (for temporal analysis, despite nulls)

2. **Numeric Aggregations**:
   - `current_employee_count`
   - `average_employee_tenure`
   - `linkedin_followers`
   - `total_funding_raised`
   - Various count fields

3. **Geographic Aggregations**:
   - Extract from `locations` array: country, region, continent

### **Potential Join Keys**

1. **Corporate Relationships**:
   - `company_id` ↔ `immediate_parent` (self-join)
   - `company_id` ↔ `ultimate_parent` (self-join)
   - `company_id` ↔ subsidiaries arrays (self-join)

2. **Stock Market Data**:
   - `ticker` ↔ external stock price data
   - `mic_exchange` ↔ exchange information

3. **LinkedIn Data**:
   - `linkedin_id`, `linkedin_url` ↔ external LinkedIn datasets

### **Data Quality Considerations**

1. **High Null Rates**:
   - Funding data (99.61% null): Filter early if needed
   - Employee metrics (67% null): Use COALESCE or handle nulls
   - Founded year (81% null): Limited temporal analysis
   - Websites (56% null): Cannot rely on for all companies

2. **Data Anomalies**:
   - `founded_year` includes years < 1800 (data quality issues)
   - `current_employee_count` includes 0 (defunct companies?)
   - Funding dates with 1900-1970 values may be placeholders

3. **Array Field Handling**:
   - Most arrays default to empty `[]` rather than NULL
   - Nested structs within arrays often contain all NULL fields
   - Use `UNNEST()` for querying array contents
   - Check array length before accessing elements

4. **Text Field Considerations**:
   - Many descriptions contain "(truncated)" indicating incomplete data
   - "Unknown" is common placeholder value
   - Case sensitivity varies (company_name lowercase, display_name mixed)

5. **Performance Considerations**:
   - 48.6M rows is large; use partitioning/clustering if available
   - Filter on indexed fields (company_id, linkedin_id) when possible
   - Aggregate before joining when possible
   - Consider materialized views for common aggregations

---

## Keywords

company data, business intelligence, company profiles, LinkedIn data, corporate structure, funding information, employee metrics, industry classification, SIC codes, NAICS codes, company size, revenue data, startup funding, corporate hierarchy, subsidiaries, parent companies, company locations, business directory, company enrichment, firmographics, B2B data, company database, business entities, private companies, public companies, stock tickers, funding rounds, venture capital, company financials, employee count, company age, founding year, company maturity, business categories, company websites, social media presence, corporate relationships, business taxonomy, company metadata

---

## Table and Column Documentation

### Table Comment
No table-level comment or description was provided in the analysis report.

### Column Comments
No column-level comments or descriptions were provided in the analysis report. All documentation is derived from data analysis patterns, value distributions, and sample data observation.