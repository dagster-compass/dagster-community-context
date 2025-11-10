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
# Summary: companies_funding_details Table

## Overall Dataset Characteristics

This table contains **436,869 rows** of company funding round details, representing a comprehensive dataset of investment activities across 191,921 unique companies. The data spans from 1900 to recent years (2021 visible in samples), with 9,152 distinct funding dates recorded.

**Data Quality Observations:**
- High data completeness for core identifiers (0% nulls in IDs, dates, and types)
- Significant missing data (28.16%) in funding amounts and currency fields
- All funding amounts appear to be in USD when present (single currency value)
- Array fields (investors) are never null but can be empty arrays

**Notable Patterns:**
- Wide date range suggests some historical or placeholder dates (1900-1917)
- 28 different funding round types with standard venture capital nomenclature
- Funding amounts range from small grants to multi-million dollar rounds

## Column Details

### funding_detail_id (STRING)
- **Type:** Unique identifier, appears to be numeric stored as string
- **Nulls:** None (0%)
- **Pattern:** Completely unique across all rows (436,869 unique values)
- **Purpose:** Primary key for individual funding events
- **Sample values:** 564255, 568437, 132439

### funding_round_date (STRING)
- **Type:** Date stored as string in YYYY-MM-DD format
- **Nulls:** None (0%)
- **Pattern:** 9,152 unique dates suggesting multiple companies can have funding on same date
- **Distribution:** Ranges from 1900-01-01 to 2021+ (historical outliers present)
- **Sample values:** 2021-09-21, 2014-07-21, 2021-11-28

### company_id (STRING)
- **Type:** Unique company identifier (appears to be hash/encoded)
- **Nulls:** None (0%)
- **Pattern:** 191,921 unique companies (2.28 funding rounds per company average)
- **Purpose:** Foreign key linking to company records
- **Sample values:** EUpt6QBZn7IIz51BSNoTagehXBhz, QO1Nt7d4eKQFS7MCU4ygBQoEG6nl

### funding_round_type (STRING)
- **Type:** Categorical/enumerated funding stage
- **Nulls:** None (0%)
- **Values:** 28 distinct types including:
  - Standard rounds: angel, seed, pre_seed, series_unknown, series_a/b/c (implied)
  - Alternative funding: grant, convertible_note, equity_crowdfunding, initial_coin_offering
  - Corporate: corporate_round, post_ipo_debt, post_ipo_equity
  - Other: debt_financing, non_equity_assistance
- **Sample values:** seed, grant, series_unknown

### investing_companies (ARRAY<STRING>)
- **Type:** Array of company investor names
- **Nulls:** None (0% - empty arrays instead of nulls)
- **Pattern:** Can contain 0 to multiple investor names
- **Common patterns:** 
  - Government entities: 'U.S. Department of Education', 'National Science Foundation (NSF)'
  - VC firms: 'Bpifrance', 'Weinberg Capital Partners', 'Rite Ventures'
  - Corporate investors: 'Fashion Zone'
- **Note:** Many rounds have empty arrays (no institutional investors)

### investing_individuals (ARRAY<STRING>)
- **Type:** Array of individual investor names
- **Nulls:** None (0% - empty arrays instead of nulls)
- **Pattern:** Predominantly empty arrays; individual investors less commonly tracked
- **Sample value:** ['Terell Sterling']
- **Note:** Appears to be much sparser than company investors

### funding_amount (STRING)
- **Type:** Numeric value stored as string with decimal precision
- **Nulls:** 28.16% (123,035 rows)
- **Pattern:** Appears to be float values (e.g., "100000.0", "8000000.0")
- **Range:** From small amounts (100,000) to millions (5,238,633 visible)
- **Note:** High null rate suggests many undisclosed funding amounts

### funding_currency (STRING)
- **Type:** Currency code
- **Nulls:** 28.16% (matches funding_amount null pattern exactly)
- **Values:** Only "usd" when present; nulls when amount is null
- **Pattern:** Currency is null if and only if funding_amount is null
- **Note:** Single currency suggests amounts may be normalized to USD

## Table and Column Documentation

**Table Comment:** Not provided

**Column Comments:** Not provided

## Potential Query Considerations

### Good for Filtering:
- **funding_round_type**: Excellent for filtering by investment stage (e.g., "WHERE funding_round_type = 'seed'")
- **funding_round_date**: Time-based filtering and trend analysis (consider date range filters to exclude historical outliers)
- **company_id**: Finding all funding rounds for specific companies
- **funding_amount IS NOT NULL**: Filtering to only disclosed funding amounts

### Good for Grouping/Aggregation:
- **company_id**: Count funding rounds per company, total funding raised
- **funding_round_type**: Distribution of funding by stage
- **funding_round_date**: Time-series analysis (by year, month, quarter)
- **investing_companies/individuals**: Investor activity analysis (requires array unnesting)

### Potential Join Keys:
- **company_id**: Primary foreign key to join with company master table
- **funding_detail_id**: Unique key for this table (could be referenced by other detail tables)

### Data Quality Considerations:

1. **Date Anomalies**: Filter out dates before realistic founding dates (e.g., pre-1950) to avoid historical placeholders
2. **Missing Amounts**: 28% of records lack funding amounts - queries calculating totals should account for this
3. **Currency Normalization**: All amounts appear in USD; verify if foreign currency rounds are converted or excluded
4. **Empty Arrays**: ARRAY fields use empty arrays rather than nulls - use `ARRAY_LENGTH() > 0` or similar checks
5. **Multiple Rounds**: Companies can have multiple funding rounds - aggregations need appropriate grouping
6. **Investor Data Sparseness**: Individual investors and even company investors may be incomplete

### Recommended Query Patterns:

```sql
-- Time-based analysis (filter out historical outliers)
WHERE funding_round_date >= '2000-01-01'

-- Known funding amounts only
WHERE funding_amount IS NOT NULL

-- Specific round types
WHERE funding_round_type IN ('seed', 'series_a', 'series_b')

-- Rounds with institutional investors
WHERE ARRAY_LENGTH(investing_companies) > 0

-- Unnesting investors for analysis
CROSS JOIN UNNEST(investing_companies) AS investor_name
```

## Keywords

funding rounds, venture capital, investment data, seed funding, series funding, company financing, investor data, funding amount, equity financing, grants, angel investment, ICO, crowdfunding, debt financing, post-IPO, corporate round, investment stage, funding history, company investments, investor tracking, financial data, startup funding, VC data, investment rounds, capital raises, funding timeline