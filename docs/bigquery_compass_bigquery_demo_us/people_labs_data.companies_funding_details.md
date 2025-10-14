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
- **Data Quality**: Generally good with complete primary identifiers, but significant missing data (28.16%) in funding amounts
- **Coverage**: Spans from 1900 to recent years (2021+) with 9,152 unique funding dates
- **Scope**: Covers 191,921 unique companies with diverse funding activities
- **Notable Patterns**: 
  - Many funding rounds lack disclosed amounts (28.16% null)
  - All currency data is in USD when present
  - Investor information is stored as arrays, allowing multiple investors per round

## Column Details

### **company_id** (STRING)
- **Type**: Primary identifier for companies
- **Completeness**: 100% populated (0% null)
- **Uniqueness**: 191,921 unique companies across 436,869 records
- **Pattern**: Alphanumeric hash-like identifiers (e.g., "sAMuHNVFm3rnNtPKzbGfvAWBwm9n")
- **Usage**: Primary key for joining with other company tables

### **funding_detail_id** (STRING)
- **Type**: Unique identifier for each funding event
- **Completeness**: 100% populated (0% null)
- **Uniqueness**: 436,869 unique values (one per row)
- **Pattern**: Numeric strings (e.g., "490320", "426404")
- **Usage**: Primary key for this table, ensures each funding round is uniquely identified

### **funding_round_date** (STRING)
- **Type**: Date of funding round in YYYY-MM-DD format
- **Completeness**: 100% populated (0% null)
- **Range**: Historical data from 1900-01-01 to 2021+ (9,152 unique dates)
- **Pattern**: ISO date format strings
- **Usage**: Excellent for temporal analysis, filtering by time periods, trend analysis

### **funding_round_type** (STRING)
- **Type**: Categorical funding stage/type
- **Completeness**: 100% populated (0% null)
- **Variety**: 28 distinct funding types
- **Common Types**: seed, pre_seed, series_a, series_b, series_c, angel, convertible_note, corporate_round, debt_financing, equity_crowdfunding, grant, initial_coin_offering, non_equity_assistance, post_ipo_debt, post_ipo_equity, private_equity
- **Usage**: Ideal for grouping and filtering by funding stage

### **funding_amount** (STRING)
- **Type**: Funding amount as string (includes scientific notation)
- **Completeness**: 71.84% populated (28.16% null)
- **Format**: Mix of decimal notation ("3500000.0") and scientific notation ("5.0E7", "1.0E8")
- **Considerations**: Requires parsing for numeric operations; nulls indicate undisclosed amounts
- **Usage**: Key for financial analysis when converted to numeric format

### **funding_currency** (STRING)
- **Type**: Currency code for funding amount
- **Completeness**: 71.84% populated (28.16% null - matches funding_amount nulls)
- **Values**: Only "usd" when populated
- **Pattern**: Null exactly when funding_amount is null
- **Usage**: Currently all USD, but structure supports multi-currency expansion

### **investing_companies** (ARRAY<STRING>)
- **Type**: Array of company investor names
- **Completeness**: 100% populated (0% null, but arrays can be empty [])
- **Content**: Company names as strings within arrays
- **Pattern**: Many empty arrays [], some with multiple company investors
- **Usage**: Enables analysis of investor networks, co-investment patterns

### **investing_individuals** (ARRAY<STRING>)
- **Type**: Array of individual investor names
- **Completeness**: 100% populated (0% null, but arrays can be empty [])
- **Content**: Individual names as strings within arrays
- **Pattern**: Many empty arrays [], some with multiple individual investors
- **Usage**: Tracks angel investors and individual participants in funding rounds

## Potential Query Considerations

### **Excellent for Filtering**:
- `funding_round_date`: Time-based filtering, date ranges, yearly/quarterly analysis
- `funding_round_type`: Stage-based analysis (seed vs. series rounds)
- `company_id`: Company-specific funding history
- `funding_currency`: Currency filtering (though currently only USD)

### **Good for Grouping/Aggregation**:
- `funding_round_type`: Analyze funding patterns by stage
- `funding_round_date`: Temporal aggregations (by year, quarter, month)
- `company_id`: Company-level funding summaries
- Array fields: Investor participation analysis

### **Potential Join Keys**:
- `company_id`: Primary join key to other company tables
- `funding_detail_id`: Unique identifier for funding event details

### **Data Quality Considerations**:
- **Missing Amounts**: 28.16% of records lack funding amounts - consider this in financial analyses
- **Scientific Notation**: Funding amounts require parsing before numeric operations
- **Array Handling**: Investor arrays need special handling for searches and counts
- **Historical Data**: Very old dates (1900s) may need validation
- **Empty Investor Arrays**: Many rounds have no recorded investors

## Keywords

funding, investments, venture capital, startup financing, series rounds, seed funding, investors, companies, funding amounts, funding dates, funding types, angel investment, private equity, convertible notes, grants, ICO, crowdfunding, financial data, investment rounds, funding history

## Table and Column Documentation

*No table comment or column comments were provided in the analysis report.*