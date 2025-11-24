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
# Table Summary: people_labs_data.companies_funding_details

## Overall Dataset Characteristics

**Total Rows:** 436,869 funding records

**Data Quality:** Generally high quality with complete coverage for core identifying fields. The dataset shows:
- No null values in primary identifiers (company_id, funding_detail_id, funding_round_type, funding_round_date)
- Moderate null rate (28.16%) in funding amount fields, which is expected as not all funding rounds disclose amounts
- Well-structured array fields for investor tracking

**Notable Patterns:**
- 191,921 unique companies across 436,869 funding events (average ~2.3 funding rounds per company)
- Dataset spans from early 1900s to present day (historical dates likely represent backdated records)
- All disclosed funding amounts are denominated in USD
- Many funding rounds (~28%) do not have disclosed amounts or investor information

## Column Details

### company_id (STRING)
- **Type:** Identifier string (alphanumeric hash)
- **Completeness:** 100% populated
- **Purpose:** Primary foreign key linking to companies table
- **Pattern:** Fixed-length alphanumeric strings (e.g., "afv3fGmBb4uyMFm6f5LVbgcDBRGu")
- **Usage:** Essential for joining with company master data

### funding_detail_id (STRING)
- **Type:** Unique identifier (numeric string)
- **Completeness:** 100% populated, fully unique (436,869 unique values)
- **Purpose:** Primary key for funding events
- **Pattern:** Numeric values as strings (e.g., "73027", "18932")
- **Usage:** Unique identifier for each funding round record

### funding_round_type (STRING)
- **Type:** Categorical
- **Completeness:** 100% populated
- **Categories:** 28 distinct types including:
  - Traditional equity: angel, seed, series_a through series_unknown
  - Alternative financing: convertible_note, debt_financing, equity_crowdfunding
  - Non-traditional: grant, non_equity_assistance, initial_coin_offering
  - Post-IPO: post_ipo_debt, post_ipo_equity
  - Corporate: corporate_round
- **Usage:** Critical for filtering and analyzing funding stage patterns

### funding_round_date (STRING)
- **Type:** Date stored as string (ISO format: YYYY-MM-DD)
- **Completeness:** 100% populated
- **Range:** 9,152 unique dates from 1900-01-01 to recent dates
- **Pattern:** Historical records start from early 1900s (likely backdated or historical company formations)
- **Usage:** Time-series analysis, trend identification, temporal filtering

### funding_amount (STRING)
- **Type:** Numeric value stored as string with decimal
- **Null Percentage:** 28.16% (123,024 null records)
- **Range:** 106,753 unique values from small grants ($5,000) to large rounds ($8.8M+ in samples)
- **Pattern:** Float values with ".0" suffix (e.g., "5000000.0")
- **Usage:** Financial analysis, aggregations, funding size comparisons
- **Consideration:** Nulls represent undisclosed amounts - exclude or handle separately in aggregations

### funding_currency (STRING)
- **Type:** Currency code
- **Null Percentage:** 28.16% (matches funding_amount nulls exactly)
- **Values:** Only "usd" when populated
- **Pattern:** Always null when funding_amount is null, always "usd" when populated
- **Usage:** Currently redundant (all values are USD), but important for future multi-currency support

### investing_companies (ARRAY<STRING>)
- **Type:** Array of company names
- **Completeness:** 100% populated (empty arrays for no investors)
- **Pattern:** Contains 0 to multiple investor company names
- **Examples:** ['Accel', 'Shrug Capital', 'Sound Ventures'], ['Bayern Kapital GmbH', 'Bloomhaus Ventures AG']
- **Usage:** Investor analysis, network effects, co-investment patterns
- **Note:** Requires array unnesting for individual investor analysis

### investing_individuals (ARRAY<STRING>)
- **Type:** Array of individual investor names
- **Completeness:** 100% populated (mostly empty arrays in samples)
- **Pattern:** Contains 0 to multiple individual investor names
- **Usage:** Angel investor tracking, individual investor network analysis
- **Consideration:** Appears less frequently populated than investing_companies

## Query Considerations

### Optimal Filtering Columns:
- **company_id**: For company-specific funding history
- **funding_round_type**: For stage-specific analysis (seed, series_a, etc.)
- **funding_round_date**: For temporal analysis and trends (requires PARSE_DATE/CAST)
- **funding_amount**: For size-based filtering (handle nulls appropriately)

### Aggregation Opportunities:
- **GROUP BY company_id**: Total funding per company, funding round count
- **GROUP BY funding_round_type**: Average/total funding by stage
- **GROUP BY DATE_TRUNC(funding_round_date)**: Monthly/yearly funding trends
- **UNNEST investing_companies/individuals**: Most active investors, investment patterns

### Join Keys:
- **company_id**: Primary foreign key to join with companies master table
- **investing_companies** (after UNNEST): Could join with investor/company databases
- **investing_individuals** (after UNNEST): Could join with people/investor databases

### Data Quality Considerations:
1. **Null Handling**: 28.16% of records lack funding amounts - decide whether to exclude or include with nulls in financial aggregations
2. **Date Parsing**: funding_round_date is stored as STRING; convert to DATE type for proper temporal operations
3. **Amount Conversion**: funding_amount is STRING; cast to FLOAT64 for mathematical operations
4. **Historical Data**: Very old dates (1900s) may require filtering for modern analysis
5. **Array Processing**: Use UNNEST() to flatten investing_companies/individuals for investor-level analysis
6. **Currency Assumption**: All amounts in USD currently, but schema supports future multi-currency data

### Common Query Patterns:
- Total/average funding by company or stage
- Time-series funding trends
- Investor co-occurrence analysis (requires array unnesting)
- Companies by number of funding rounds
- Funding velocity (time between rounds)

## Keywords
funding rounds, venture capital, investment data, company financing, seed funding, series funding, investors, funding amount, equity crowdfunding, angel investment, IPO, debt financing, grants, investment trends, startup funding, financial data, temporal analysis, investor networks, corporate rounds, convertible notes

## Table and Column Documentation
No table-level or column-level comments were provided in the source data.