---
columns:
- cand_contrib (FLOAT64)
- cand_ici (STRING)
- cand_id (STRING)
- cand_loan_repay (FLOAT64)
- cand_loans (FLOAT64)
- cand_name (STRING)
- cand_office_district (INT64)
- cand_office_st (STRING)
- cand_pty_affiliation (STRING)
- cmte_refunds (FLOAT64)
- coh_bop (FLOAT64)
- coh_cop (FLOAT64)
- cvg_end_dt (DATE)
- debts_owed_by (FLOAT64)
- gen_election (STRING)
- gen_election_precent (FLOAT64)
- indiv_refunds (FLOAT64)
- other_loan_repay (FLOAT64)
- other_loans (FLOAT64)
- other_pol_cmte_contrib (FLOAT64)
- pol_pty_contrib (FLOAT64)
- prim_election (STRING)
- pty_cd (INT64)
- run_election (STRING)
- source_file (STRING)
- spec_election (STRING)
- trans_from_auth (FLOAT64)
- trans_to_auth (FLOAT64)
- ttl_disb (FLOAT64)
- ttl_indiv_contrib (FLOAT64)
- ttl_receipts (FLOAT64)
- year (INT64)
schema_hash: d38593c04ee29d00dc4293c1e582aff8d127ad64d764673a6fff2ff5844400bd

---
# Data Summary: US Political Contributions Table

## Overall Dataset Characteristics

**Total Rows:** 68,666

**Data Quality:**
- High quality core identifiers (cand_id, cand_name, year, cvg_end_dt) with minimal to no nulls
- Significant null percentages in financial metrics (ranging from 12% to 96%)
- Election outcome fields are predominantly null (>99% for special/runoff elections, ~77% for general elections)
- Data spans from 1980 to 2026 across 24 election cycles

**Notable Patterns:**
- Dataset tracks political campaign finance data at the candidate level
- Financial data becomes sparser for certain contribution categories (e.g., other_loans at 96% null)
- Source files correspond to election years (weball00.txt through weball24.txt)
- Geographic coverage includes all 50 states plus territories (57 unique state codes)

## Column Details

### Identification & Demographics

**cand_id** (STRING)
- Primary candidate identifier
- No nulls, 28,356 unique values
- Format: Alphanumeric (e.g., H6OH05063, S4MD00020)
- Appears to encode office type (H=House, S=Senate) in prefix

**cand_name** (STRING)
- Candidate full name
- No nulls, 29,986 unique values
- Format: LAST, FIRST MIDDLE pattern
- More unique names than IDs suggests name variations or multiple candidacies

**cand_ici** (STRING)
- Incumbent/Challenger/Open seat indicator
- 18% null
- Values: C (Challenger), I (Incumbent), O (Open)
- Key for competitive analysis

**pty_cd** (INT64)
- Numeric party code
- No nulls, 3 unique values (1, 2, 3)
- Likely maps to major parties

**cand_pty_affiliation** (STRING)
- Party affiliation abbreviation
- 0.13% null, 80 unique values
- Common: DEM, REP, plus many third parties
- Provides detailed party information beyond pty_cd

### Financial Metrics - Core

**ttl_receipts** (FLOAT64)
- Total campaign receipts
- 19% null
- Range: -$1.3M to $4.8B
- Negative values indicate adjustments/corrections

**ttl_disb** (FLOAT64)
- Total disbursements
- 13% null
- Range: -$674K to $3.8B
- Lower null rate than receipts

**coh_cop** (FLOAT64)
- Cash on hand at close of period
- 38% null
- Range: -$2.4M to $9.8B
- Useful for financial health analysis

**coh_bop** (FLOAT64)
- Cash on hand at beginning of period
- 49% null
- Range: -$430K to $776M
- Higher null rate suggests reporting gaps

### Financial Metrics - Contribution Sources

**ttl_indiv_contrib** (FLOAT64)
- Total individual contributions
- 38% null
- Range: -$1.3M to $18.9B
- Major funding source metric

**cand_contrib** (FLOAT64)
- Candidate self-contributions
- 74% null (many candidates don't self-fund)
- Range: -$35K to $2.8B

**cand_loans** (FLOAT64)
- Loans from candidate
- 74% null
- Range: -$1.7M to $62.9M

**other_pol_cmte_contrib** (FLOAT64)
- Contributions from other political committees
- 62% null
- Range: -$36K to $1.9B

**pol_pty_contrib** (FLOAT64)
- Political party contributions
- 80% null
- Range: -$11K to $9.6M

### Financial Metrics - Transfers & Loans

**trans_from_auth** (FLOAT64)
- Transfers from authorized committees
- 90% null (rare transaction type)
- Range: -$600K to $534M

**trans_to_auth** (FLOAT64)
- Transfers to authorized committees
- 92% null
- Range: -$18K to $47.5M

**other_loans** (FLOAT64)
- Loans from other sources
- 96% null (very rare)
- Range: -$14K to $21M

**cand_loan_repay** (FLOAT64)
- Candidate loan repayments
- 79% null
- Range: -$35.5K to $1.9B

**other_loan_repay** (FLOAT64)
- Other loan repayments
- 97% null
- Range: -$3K to $50M

### Financial Metrics - Refunds & Debts

**indiv_refunds** (FLOAT64)
- Individual contribution refunds
- 68% null
- Range: -$555K to $1.9B

**cmte_refunds** (FLOAT64)
- Committee refunds
- 86% null
- Range: -$132K to $48.4M

**debts_owed_by** (FLOAT64)
- Debts owed by campaign
- 59% null
- Range: -$346K to $73.7M
- Important for financial health assessment

### Geographic & Office Information

**cand_office_st** (STRING)
- State/territory code
- No nulls, 57 unique values
- Includes all states plus territories (AS, GU, etc.) and "00" for presidential

**cand_office_district** (INT64)
- Congressional district number
- 0.09% null
- Range: 0-53
- 0 indicates statewide office (Senate, Governor)

### Election Results

**prim_election** (STRING)
- Primary election outcome
- 72% null
- Values: W (Win), L (Loss), R, P, X, l, w (case variations)

**spec_election** (STRING)
- Special election outcome
- 99% null (rare events)
- Values: W, L, R, l

**run_election** (STRING)
- Runoff election outcome
- 99% null (rare events)
- Values: W, L, R

**gen_election** (STRING)
- General election outcome
- 77% null
- Values: W, L, R, l, w

**gen_election_precent** (FLOAT64)
- General election vote percentage
- 78% null
- Range: 1.0 to 100.0
- Integer percentages only

### Temporal & Source

**year** (INT64)
- Election cycle year
- No nulls, 24 unique values
- Range: 1980-2026
- Even years (election cycles)

**cvg_end_dt** (DATE)
- Coverage end date
- No nulls, 6,398 unique values
- Typically year-end dates (12-31)
- Useful for time-series analysis

**source_file** (STRING)
- Original data file name
- No nulls, 24 unique values
- Format: weball[YY].txt
- Maps directly to election year

## Query Considerations

### Excellent Filtering Columns:
- **year**: Time-based analysis, no nulls
- **cand_office_st**: Geographic filtering, no nulls
- **cand_pty_affiliation**: Party analysis, minimal nulls
- **cand_ici**: Incumbent advantage studies
- **gen_election**: Election outcomes (when not null)

### Good Grouping/Aggregation Columns:
- **year**: Trend analysis over time
- **cand_office_st**: State-level aggregation
- **cand_pty_affiliation**: Party comparisons
- **cand_office_district**: District-level analysis
- **source_file**: Data vintage grouping

### Potential Join Keys:
- **cand_id**: Primary key for candidate-level joins
- **cand_office_st + year**: Geographic time-series
- **cand_name**: Text matching (with caution due to variations)

### Data Quality Considerations:

1. **High Null Percentages**: Many financial fields have 60-90%+ nulls. Queries should:
   - Use `IS NOT NULL` filters when requiring complete financial data
   - Consider null handling in aggregations (SUM, AVG may need COALESCE)
   - Expect result sets to shrink significantly with financial field requirements

2. **Negative Values**: Present in many financial fields, likely indicating:
   - Corrections/adjustments
   - Refunds
   - Should be handled explicitly in business logic

3. **Case Sensitivity**: Election outcome fields show case variations (W vs w)
   - Recommend UPPER() or LOWER() for consistent comparisons

4. **Date Ranges**: Data spans 46 years (1980-2026)
   - Consider filtering by relevant date ranges for performance
   - Future dates (2026) may represent preliminary/planned data

5. **Large Value Ranges**: Some fields show extreme outliers (billions)
   - May warrant outlier detection or filtering
   - Consider using SAFE_DIVIDE for ratio calculations

6. **District 0**: Special meaning (statewide offices)
   - Filter appropriately when analyzing House races specifically

## Keywords

political contributions, campaign finance, FEC data, election data, candidate fundraising, receipts, disbursements, political committees, PAC contributions, individual contributions, campaign loans, election outcomes, congressional districts, primary elections, general elections, incumbent challenger, party affiliation, cash on hand, political party, democratic, republican, congressional campaigns, senate campaigns, house campaigns, federal elections, campaign debts, vote percentage, election cycles, political donations, campaign expenditures, self-funding, committee transfers

## Table and Column Documentation

**Table Comment:** Not provided

**Column Comments:** Not provided