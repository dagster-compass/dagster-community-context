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
# Comprehensive Summary: companies_funding_details Table

## Overall Dataset Characteristics

**Total Rows:** 436,869 funding records

**General Data Quality:**
- High-quality primary identifiers with 0% null values for core fields (company_id, funding_detail_id, funding_round_type, funding_round_date)
- Significant missing data in financial details: 28.16% of records lack funding amount and currency information
- Complex nested data structures using ARRAY types for investor information
- Unique funding_detail_id for each record suggests this is a fact table tracking individual funding events

**Notable Patterns:**
- Dataset spans from 1900 to at least 2023, with historical dates likely representing legacy or founding dates
- 191,921 unique companies across 436,869 funding rounds (average ~2.3 funding rounds per company)
- Many funding rounds have empty investor arrays, suggesting incomplete investor tracking or self-funded rounds
- All funding amounts appear to be normalized to USD when currency is specified

**Table Purpose:** This appears to be a comprehensive funding transaction table linking companies to their funding rounds, with details about timing, amount, type, and participating investors.

## Column Details

### funding_round_type (STRING)
- **Data Type:** Categorical string
- **Null Values:** 0% - Required field
- **Cardinality:** 28 distinct types
- **Common Values:** angel, convertible_note, corporate_round, debt_financing, equity_crowdfunding, grant, initial_coin_offering, non_equity_assistance, post_ipo_debt, post_ipo_equity, pre_seed, seed, series_unknown
- **Patterns:** Includes traditional VC stages (seed, series rounds), alternative funding (crowdfunding, ICO), and post-IPO activities
- **Query Considerations:** Excellent for filtering and grouping by funding stage; useful for analyzing funding patterns

### company_id (STRING)
- **Data Type:** Unique identifier (hash-like string)
- **Null Values:** 0% - Required field
- **Cardinality:** 191,921 unique companies
- **Format:** Alphanumeric string (e.g., "UvElqrVrYBxihlcaQF72xw3ofKAW")
- **Patterns:** Fixed-length encoded identifier, likely an internal system ID
- **Query Considerations:** Primary join key to company master table; use for aggregating funding by company

### funding_round_date (STRING)
- **Data Type:** Date stored as STRING
- **Null Values:** 0% - Required field
- **Cardinality:** 9,152 unique dates
- **Format:** ISO 8601 date format (YYYY-MM-DD)
- **Range:** 1900-01-01 to at least 2023-12-18
- **Patterns:** Some very old dates (1900-1917) likely represent placeholder or legacy data
- **Query Considerations:** Cast to DATE type for temporal analysis; excellent for time-series queries, trend analysis, and date range filtering

### funding_detail_id (STRING)
- **Data Type:** Unique identifier (numeric as string)
- **Null Values:** 0% - Required field
- **Cardinality:** 436,869 unique values (100% unique)
- **Format:** Numeric string (e.g., "127591", "358088")
- **Patterns:** Primary key for the table; each funding event has unique ID
- **Query Considerations:** Use for deduplication and ensuring row-level uniqueness; can be used for pagination or ordering

### investing_companies (ARRAY<STRING>)
- **Data Type:** Array of strings
- **Null Values:** 0% for array (but many contain empty arrays [])
- **Cardinality:** 436,869 unique combinations
- **Format:** Array of company names (e.g., ['HV Capital', 'Unbound'], ['Galaxy'])
- **Patterns:** Many records have empty arrays; some have single investors, others have multiple
- **Query Considerations:** Requires array operations (UNNEST, ARRAY_LENGTH) for analysis; use to identify co-investment patterns or specific investor participation

### investing_individuals (ARRAY<STRING>)
- **Data Type:** Array of strings
- **Null Values:** 0% for array (but predominantly empty arrays)
- **Cardinality:** 436,869 unique combinations
- **Format:** Array of individual investor names
- **Patterns:** Sample data shows mostly empty arrays; individual investor data appears sparse
- **Query Considerations:** Similar to investing_companies; may have limited analytical value due to sparsity

### funding_amount (STRING)
- **Data Type:** Numeric value stored as STRING
- **Null Values:** 28.16% - Significant missing data
- **Cardinality:** 106,753 unique values
- **Format:** Floating point number as string (e.g., "72000.0", "3.4881343E7" in scientific notation)
- **Patterns:** Mix of standard decimal notation and scientific notation; values vary from thousands to tens of millions
- **Query Considerations:** Must cast to FLOAT/NUMERIC for calculations; handle nulls appropriately; scientific notation requires proper parsing

### funding_currency (STRING)
- **Data Type:** Currency code
- **Null Values:** 28.16% - Matches funding_amount null pattern
- **Cardinality:** 1 unique value (excluding nulls)
- **Values:** "usd" only (when present)
- **Patterns:** When funding_amount exists, currency is always USD; nulls are perfectly correlated with funding_amount nulls
- **Query Considerations:** Limited analytical value as all non-null values are USD; use null check to identify records with/without financial data

## Query Considerations

### Good Filtering Columns:
- **funding_round_type:** Categorical with reasonable cardinality (28 values) - excellent for stage analysis
- **funding_round_date:** Temporal filtering for trend analysis, year-over-year comparisons
- **company_id:** Filtering for specific company funding history
- **funding_amount IS NOT NULL:** Distinguishing records with/without financial data

### Good Grouping/Aggregation Columns:
- **funding_round_type:** Analyze funding by stage
- **EXTRACT(YEAR FROM funding_round_date):** Time-based aggregations
- **company_id:** Calculate total funding per company, count rounds per company
- **investing_companies (with UNNEST):** Investor activity analysis

### Potential Join Keys:
- **company_id:** Primary join key to companies master table
- **investing_companies elements:** Could join to investor/VC firm tables (requires UNNEST operation)

### Data Quality Considerations:

1. **Missing Financial Data:** 28.16% of records lack funding amounts - queries calculating total funding should handle nulls appropriately
2. **Date Range Anomalies:** Very old dates (1900-1920) may need filtering for realistic analysis
3. **Type Conversions Required:** 
   - funding_round_date needs DATE casting
   - funding_amount needs FLOAT/NUMERIC casting with scientific notation handling
4. **Array Operations:** Investor analysis requires UNNEST and array function expertise
5. **Empty vs Null Arrays:** Distinguish between no data (empty array) and missing data (though arrays are never null)
6. **Currency Normalization:** All amounts already in USD simplifies cross-border analysis

### Recommended Query Patterns:
- Aggregate funding by company: `GROUP BY company_id`
- Time-series analysis: `GROUP BY EXTRACT(YEAR FROM CAST(funding_round_date AS DATE))`
- Stage analysis: `GROUP BY funding_round_type`
- Investor participation: `CROSS JOIN UNNEST(investing_companies)`
- Filter valid financial data: `WHERE funding_amount IS NOT NULL`

## Keywords
funding rounds, venture capital, investment data, startup funding, series funding, seed funding, angel investment, IPO, company financing, investor data, funding stage, convertible notes, equity crowdfunding, debt financing, corporate venture capital, funding amount, USD, investment timeline, co-investors, funding history, VC deals, pre-seed, series A/B/C, post-IPO, ICO, grant funding, funding transactions

## Table and Column Documentation

**Table Comment:** Not provided in the analysis report.

**Column Comments:** 
- No specific column-level comments were provided in the analysis report. The column descriptions above are derived from data analysis and inference from the data patterns and values.