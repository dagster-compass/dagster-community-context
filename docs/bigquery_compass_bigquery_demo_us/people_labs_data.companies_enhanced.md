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

### Scale and Scope
- **Total Rows**: 48,628,328 (approximately 48.6 million companies)
- **Dataset Version**: 31.2
- **Global Coverage**: Companies from multiple countries and continents
- **Data Freshness**: Current employee counts and funding information suggest regularly updated data

### Data Quality Observations
- **High Completeness**: Core identifiers (company_id, company_name, linkedin_id) have 0% null values
- **Significant Sparsity**: Many enrichment fields have very high null percentages (70-99%)
- **Rich When Present**: When populated, fields contain detailed structured information
- **Dual Classification Systems**: Both industry (147 values) and industry_v2 (434 values) provide categorization options

### Notable Patterns
- **Company Size Distribution**: Dominated by small companies (1-10 employee range most common)
- **Funding Status**: 99.61% of companies are unfunded or funding status unknown
- **Private Companies**: Vast majority are private entities (6 company types total)
- **LinkedIn-Centric**: Strong LinkedIn integration with URLs, slugs, and IDs for all records

## Column Details

### Core Identifiers

**company_id** (STRING)
- Unique identifier for each company (100% unique)
- Format: Alphanumeric hash (e.g., "mbCImzBlTUAXzWqvxHuzrQtrRgQ8")
- 0% null - reliable primary key
- Use for: Primary key, joins, deduplication

**linkedin_id** (STRING)
- LinkedIn's internal company ID
- 0% null, 100% unique
- Numeric format (e.g., "16948610")
- Use for: LinkedIn API integration, alternative identifier

**company_name** (STRING)
- Legal/registered company name
- 0% null, 48,063,385 unique values (some duplicates exist)
- Examples: "santa fe flea market", "b s marketing limited"
- Use for: Primary company identification, text search

**display_name** (STRING)
- Formatted company name for display
- 0% null, 48,236,437 unique values
- May include capitalization/formatting differences from company_name

### Company Profile Information

**company_summary** (STRING)
- Brief company overview including name, industry, size, founding year
- 0% null, 48,626,325 unique values (highly unique)
- Truncated in some cases (indicated by "... (truncated)")
- Use for: Quick company snapshots, search/filtering

**company_description_full** (STRING)
- Extended company description
- 0% null, 48,627,424 unique values
- Can be truncated
- Use for: Detailed company information, text analysis

**headline** (STRING)
- Company tagline or motto
- 86.10% null - only 13.9% of companies have this
- Example: "Pioneers of eLearning."
- Use for: Marketing/branding analysis when available

**summary** (STRING)
- Additional company summary text
- 69.45% null
- Use for: Supplementary company information

### Web Presence

**website** (STRING)
- Company website URL
- 56.14% null - about 44% have websites
- Examples: "autonomie-coach.de"
- Use for: Web scraping, external data enrichment, filtering companies with online presence

**linkedin_url** (STRING)
- Full LinkedIn company page URL
- 0% null, 100% unique
- Format: "linkedin.com/company/[slug]"
- Use for: Direct LinkedIn access

**linkedin_slug** (STRING)
- URL-friendly LinkedIn identifier
- 0% null, 100% unique
- Examples: "pashen-fitness-llc", "crêperie-genia"
- Use for: URL construction, human-readable IDs

**facebook_url** (STRING)
- Facebook page URL
- 96.84% null - only 3.16% have Facebook presence
- Various formats including apps.facebook.com
- Use for: Social media analysis (limited coverage)

**twitter_url** (STRING)
- Twitter/X profile URL
- 97.26% null - only 2.74% have Twitter presence
- Use for: Social media analysis (very limited coverage)

### Company Classification

**company_type** (STRING)
- Organization type
- 0% null
- 6 values: educational, government, nonprofit, private, public, public_subsidiary
- Dominated by "private" companies
- Use for: Filtering by organization type

**company_size** (STRING)
- Employee count range
- 0% null
- 8 categories: 1-10, 11-50, 51-200, 201-500, 501-1000, 1001-5000, 5001-10000, 10001+
- Heavily skewed toward 1-10 range
- Use for: Size-based segmentation, filtering by company scale

**industry** (STRING)
- Primary industry classification
- 25.41% null
- 147 distinct industries
- Examples: "dairy", "medical devices", "accounting"
- Use for: Industry-based analysis, filtering

**industry_v2** (STRING)
- More granular industry classification
- 28.49% null
- 434 distinct industries (more detailed than industry)
- Examples: "real estate", "architecture and planning", "marketing services"
- Use for: Detailed industry segmentation

**company_maturity** (STRING)
- Business lifecycle stage
- 0% null
- 5 values: Early stage, Established, Growth stage, Startup, Unknown
- "Unknown" is very common
- Use for: Maturity-based filtering

**funding_status** (STRING)
- Whether company has received funding
- 0% null
- 2 values: "Funded", "Not funded/Unknown"
- Dominated by "Not funded/Unknown" (99.61%)
- Use for: Identifying funded vs non-funded companies

### Financial & Trading Information

**ticker** (STRING)
- Stock ticker symbol
- 99.98% null - only 0.02% are publicly traded
- 10,216 unique values
- Examples: "000040.KS", "000680.SZ"
- Use for: Public company identification, stock market analysis

**mic_exchange** (STRING)
- Market Identifier Code for exchange
- 99.98% null
- 59 distinct exchanges
- Examples: "xnys" (NYSE), "xnas" (NASDAQ)
- Use for: Exchange-specific analysis

**inferred_revenue** (STRING)
- Estimated revenue range
- 67.06% null
- 10 ranges: $0-$1M, $1M-$10M, $10M-$25M, $25M-$50M, $50M-$100M, $100M-$250M, $250M-$500M, $500M-$1B, $1B-$10B, $10B+
- Use for: Revenue-based segmentation, size analysis

### Funding Information

**total_funding_raised** (FLOAT64)
- Total capital raised
- 99.61% null
- Range: 0.0 to 74,015,950,500.0 (74 billion)
- Use for: Funding analysis on the 0.39% that are funded

**latest_funding_stage** (STRING)
- Most recent funding round type
- 99.61% null
- 27 stages including: angel, seed, series_a through series_unknown, corporate_round, debt_financing, etc.
- Use for: Funding stage analysis

**last_funding_date** (STRING)
- Date of last funding round
- 99.61% null
- Date format appears to be YYYY-MM-DD
- Range: 1900-01-01 to recent dates
- Note: Some dates appear questionable (1900, 1901)
- Use for: Temporal funding analysis

**count_funding_rounds** (INT64)
- Number of funding rounds
- 99.61% null
- Range: 1 to 50
- Use for: Funding activity intensity

**funding_stages** (ARRAY<STRING>)
- List of all funding stages received
- 0% null (empty array when no funding)
- Use for: Detailed funding history analysis

**funding_stages_text** (STRING)
- Comma-separated funding stages
- 99.61% null
- Use for: Text-based funding stage queries

**funding_stages_count** (INT64)
- Count of unique funding stages
- 99.61% null
- Range: 1 to 18
- Use for: Funding diversity analysis

### Employee Metrics

**current_employee_count** (INT64)
- Exact employee count
- 67.06% null
- Range: 0 to 503,423
- Use for: Precise size filtering, growth analysis

**average_employee_tenure** (FLOAT64)
- Mean years employees have worked at company
- 67.06% null
- Range: 0.0 to 95.667 years
- Examples: 2.264, 1.333 years
- Use for: Employee retention analysis, company stability

**linkedin_followers** (INT64)
- Number of LinkedIn page followers
- 61.14% null
- Range: 1 to 35,128,123
- Use for: Social media reach, brand awareness metrics

### Temporal Information

**founded_year** (INT64)
- Year company was established
- 80.89% null
- Range: 1001 to 2025
- 963 unique values
- Note: Some very early dates may be data quality issues
- Use for: Age analysis, cohort studies

### Corporate Hierarchy

**ultimate_parent** (STRING)
- Company ID of top-level parent
- 99.78% null - only 0.22% have parent companies
- 33,245 unique parents
- Use for: Corporate structure analysis, identifying subsidiaries

**immediate_parent** (STRING)
- Company ID of direct parent
- 99.78% null
- 40,086 unique parents
- Use for: Direct ownership relationships

**ultimate_parent_ticker** (STRING)
- Stock ticker of ultimate parent
- 99.93% null
- 4,472 unique values
- Use for: Linking private companies to public parents

**ultimate_parent_mic_exchange** (STRING)
- Parent company's exchange
- 99.93% null
- 54 exchanges
- Use for: Parent company trading information

**direct_subsidiaries** (ARRAY<STRING>)
- List of direct subsidiary company IDs
- 0% null (empty when none)
- Use for: Finding child companies

**all_subsidiaries** (ARRAY<STRING>)
- Complete subsidiary tree
- 0% null (empty when none)
- Use for: Full corporate structure

**direct_subsidiaries_count** (INT64)
- Count of direct subsidiaries
- 99.92% null
- Range: 1 to 271
- Use for: Subsidiary portfolio size

**all_subsidiaries_count** (INT64)
- Total subsidiaries in tree
- 99.92% null
- Range: 1 to 633
- Use for: Corporate complexity metrics

### Alternative Identifiers

**alternative_names** (ARRAY<STRING>)
- Other names company is known by
- 0% null (empty when none)
- Use for: Name matching, finding acquisitions/rebrands

**alternative_names_text** (STRING)
- Comma-separated alternative names
- 97.95% null
- Examples: "ciox health (through acquisition)", "granford"
- Use for: Text-based name searching

**alternative_names_count** (INT64)
- Number of alternative names
- 97.95% null
- Range: 1 to 10
- Use for: Name variation analysis

**alternative_domains** (ARRAY<STRING>)
- Other web domains owned
- 0% null (empty when none)
- Example: ['hebronchurch.org']
- Use for: Web property discovery

**alternative_domains_count** (INT64)
- Count of alternative domains
- 92.86% null
- Range: 1 to 10
- Use for: Web presence breadth

### Location Information

**locations** (ARRAY<STRUCT>)
- Structured location data
- 0% null (always has at least one location)
- Structure includes: street_address, postal_code, region, locality, metro, country, name, geo, continent, address_line_2
- Geographic coordinates in geo field (format: "lat,lon")
- Use for: Geographic analysis, mapping, regional filtering

**locations_count** (INT64)
- Number of company locations
- 0% null
- Range: 1 to 10
- Most common: 1
- Use for: Multi-location analysis

**top_us_employee_metros** (ARRAY<STRUCT>)
- US metro areas with employees
- 0% null (mostly empty structures)
- Structure: metro, headcount, growth_rate_12_month
- Use for: US geographic employment distribution

### Industry Classification Codes

**naics_codes** (ARRAY<STRUCT>)
- North American Industry Classification System codes
- 0% null (mostly empty/null structures)
- Structure: naics_code, sector, sub_sector, industry_group, naics_industry, national_industry
- Use for: Standard industry classification, government compliance

**naics_codes_count** (INT64)
- Count of NAICS codes
- 0% null
- Range: 1 to 1,000
- Most common: 1
- Use for: Industry complexity

**sic_codes** (ARRAY<STRUCT>)
- Standard Industrial Classification codes
- 0% null (mostly empty/null structures)
- Structure: sic_code, industry_sector, major_group, industry_group
- Use for: Legacy industry classification

**sic_codes_count** (INT64)
- Count of SIC codes
- 0% null
- Range: 1 to 1,000
- Most common: 1
- Use for: Classification breadth

### Tags and Categorization

**tags** (ARRAY<STRING>)
- Custom tags/keywords
- 0% null (empty when none)
- Use for: Custom categorization, keyword search

**tags_text** (STRING)
- Comma-separated tags
- 88.29% null
- Examples include service categories, specializations
- Use for: Text-based tag queries

**tags_count** (INT64)
- Number of tags
- 88.29% null
- Range: 1 to 10
- Use for: Tag richness analysis

### System Fields

**dataset_version** (STRING)
- Data snapshot version
- 0% null
- Single value: "31.2"
- Use for: Version tracking, data lineage

## Potential Query Considerations

### Excellent for Filtering
- **company_type**: Clean categorical data (6 values)
- **company_size**: Well-defined ranges (8 categories)
- **company_maturity**: Lifecycle stage (5 values)
- **funding_status**: Simple binary-ish classification
- **industry** / **industry_v2**: Categorical industry data
- **founded_year**: When not null, good for age-based filtering
- **company_name** / **display_name**: Text search capabilities

### Good for Grouping/Aggregation
- **industry** / **industry_v2**: Industry-level analysis
- **company_size**: Size cohort analysis
- **company_type**: Organization type distributions
- **company_maturity**: Lifecycle stage analysis
- **inferred_revenue**: Revenue tier analysis
- **locations.country**: Geographic grouping
- **locations.region**: Regional analysis
- **latest_funding_stage**: Funding stage distribution

### Potential Join Keys
- **company_id**: Primary key for internal joins
- **linkedin_id**: Alternative unique identifier
- **ultimate_parent** / **immediate_parent**: Self-joins for corporate hierarchies
- **ticker**: Join to stock market data
- **website**: Join to web analytics or external sources

### Data Quality Considerations

1. **High Null Percentages**: 
   - Most enrichment fields (funding, financial, social media) have 60-99% nulls
   - Queries should handle nulls gracefully
   - Consider using COALESCE or IS NOT NULL filters

2. **Array Fields**:
   - Empty arrays represent "no data" rather than null
   - Use UNNEST for array analysis
   - Check array length before accessing elements

3. **Date Field Anomalies**:
   - founded_year has some questionable early dates (1001-1010)
   - last_funding_date has dates from 1900s that may be placeholders
   - Consider filtering extreme dates

4. **Text Field Truncation**:
   - company_summary and company_description_full may be truncated
   - Look for "... (truncated)" indicator

5. **Nested Structures**:
   - locations, naics_codes, sic_codes are arrays of structs
   - Many have null values within structures despite non-null arrays
   - Verify struct fields exist before use

6. **Duplicate Company Names**:
   - 48M rows but only 48M unique company_names (small difference)
   - company_id is the true unique identifier
   - Multiple entries might represent branches or data quality issues

7. **Industry Field Choice**:
   - industry has 147 values, 25.41% null
   - industry_v2 has 434 values, 28.49% null
   - Choose based on desired granularity

8. **Employee Count Duality**:
   - company_size provides ranges (8 categories, 0% null)
   - current_employee_count provides exact counts (67% null)
   - Use company_size for broad analysis, current_employee_count when precision matters

## Keywords

LinkedIn companies, company data, business intelligence, firmographics, company profiles, corporate data, business database, company enrichment, funding data, venture capital, private companies, public companies, employee data, company size, industry classification, NAICS codes, SIC codes, corporate hierarchy, subsidiaries, parent companies, company revenue, stock ticker, company founding date, business locations, company websites, social media presence, funding rounds, funding stages, company maturity, startup data, enterprise data, SMB data, small business, company search, business search, B2B data, company demographics, organization data, corporate structure, business entities, company information

## Table and Column Documentation

### Table Comment
No table-level comment provided in the analysis report.

### Column Comments
No column-level comments provided in the analysis report. All column descriptions are derived from data analysis rather than explicit documentation.