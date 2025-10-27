---
columns:
- company_id (STRING)
- funding_amount (STRING)
- funding_currency (STRING)
- funding_detail_id (STRING)
- funding_round_date (STRING)
- funding_round_type (STRING)
- investing_companies (ARRAY<STRING>)
- investing_individuals (ARRAY<STRING>)
schema_hash: 207f8196f1fb29d0267d8f7140f74d3a54c010fa272465c0697ef3cac301588a

---
# Table Analysis Summary: people_labs_data.companies_funding_details

## Overall Dataset Characteristics

- **Total Rows**: 436,869 funding records
- **Data Quality**: Generally high quality with no null values in key identifier and date fields
- **Notable Patterns**: 
  - Comprehensive funding data spanning from 1900 to recent years (likely historical and current data)
  - 28.16% of records lack funding amount information, suggesting some rounds have undisclosed amounts
  - All funding amounts appear to be normalized to USD when disclosed
  - Each record represents a unique funding event with detailed investor information

## Column Details

### funding_round_date (STRING)
- **Data Type**: String in YYYY-MM-DD format
- **Completeness**: 100% (no nulls)
- **Range**: 9,152 unique dates from 1900-01-01 to recent dates
- **Pattern**: Standard date format, suitable for temporal analysis
- **Usage**: Primary field for time-series analysis and filtering by date ranges

### company_id (STRING)
- **Data Type**: Alphanumeric identifier string
- **Completeness**: 100% (no nulls) 
- **Uniqueness**: 191,921 unique companies across 436,869 funding rounds
- **Pattern**: Hash-like identifiers (e.g., "h6HP0uZ0oupc9mdAV3obuQcnDjIw")
- **Usage**: Primary key for joining with company information tables

### funding_round_type (STRING)
- **Data Type**: Categorical string
- **Completeness**: 100% (no nulls)
- **Values**: 28 distinct funding types including standard rounds (seed, series_a, etc.) and specialized types (ICO, grants, crowdfunding)
- **Common Types**: angel, convertible_note, corporate_round, debt_financing, equity_crowdfunding, grant, series_a, seed, pre_seed
- **Usage**: Excellent for categorization and filtering by funding stage

### funding_detail_id (STRING)
- **Data Type**: Numeric string identifier
- **Completeness**: 100% (no nulls)
- **Uniqueness**: 436,869 unique values (one per row)
- **Pattern**: Numeric identifiers stored as strings
- **Usage**: Primary key for this table, unique identifier for each funding event

### investing_individuals (ARRAY<STRING>)
- **Data Type**: Array of individual investor names
- **Completeness**: 100% (no nulls, but many empty arrays)
- **Pattern**: Contains individual investor names when available, empty arrays when no individual investors
- **Usage**: Suitable for investor network analysis and filtering by specific angel investors

### investing_companies (ARRAY<STRING>)
- **Data Type**: Array of institutional investor names  
- **Completeness**: 100% (no nulls, but many empty arrays)
- **Pattern**: Contains company/fund names when available, empty arrays when no institutional investors
- **Usage**: Ideal for analyzing VC participation and institutional investor patterns

### funding_amount (STRING)
- **Data Type**: Numeric string (float values)
- **Completeness**: 71.84% (28.16% null)
- **Pattern**: Decimal numbers stored as strings (e.g., "3731136.0", "5000000.0")
- **Range**: 106,753 unique funding amounts
- **Usage**: Key for financial analysis, but requires null handling in queries

### funding_currency (STRING)
- **Data Type**: Currency code string
- **Completeness**: 71.84% (28.16% null, matches funding_amount nulls)
- **Values**: Only "usd" when not null, indicating all disclosed amounts are in USD
- **Usage**: Confirms currency standardization, minimal impact on analysis

## Potential Query Considerations

### Filtering Columns
- **funding_round_date**: Excellent for temporal filtering (by year, quarter, date ranges)
- **funding_round_type**: Perfect for stage-based analysis (seed vs. series rounds)
- **company_id**: Essential for company-specific queries
- **funding_amount**: Useful for size-based filtering (with null handling)

### Grouping/Aggregation Columns
- **funding_round_date**: Group by year, quarter, month for trend analysis
- **funding_round_type**: Analyze funding patterns by stage
- **company_id**: Company-level aggregations (total funding, round count)
- **investing_companies/individuals**: Investor activity analysis

### Join Keys
- **company_id**: Primary join key to company information tables
- **funding_detail_id**: Unique identifier for this funding event

### Data Quality Considerations
- **Missing Amounts**: 28.16% of records lack funding amount - queries should handle nulls appropriately
- **Array Fields**: investing_individuals and investing_companies require array functions for proper analysis
- **Date Range**: Historical data from 1900 may include test/placeholder data
- **Currency Normalization**: All amounts in USD simplifies financial calculations

## Keywords

funding, venture capital, investment, startup, company financing, funding rounds, investors, angel investors, venture capital firms, series a, series b, seed funding, pre-seed, funding amounts, investment data, startup ecosystem, fundraising, financial data, investor relations, funding timeline, investment analysis

## Table and Column Documentation

*Note: No table comment or column comments were provided in the source data.*