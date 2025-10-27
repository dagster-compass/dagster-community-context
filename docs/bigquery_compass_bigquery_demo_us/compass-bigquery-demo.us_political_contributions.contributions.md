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
# US Political Contributions Dataset Summary

## Overall Dataset Characteristics

- **Total Rows**: 68,666 records
- **Time Period**: Spans from 1980 to 2026 (24 years of data)
- **Data Quality**: Generally good with complete candidate identifiers, but significant null percentages in financial detail columns
- **Domain**: Federal Election Commission (FEC) candidate financial data covering House, Senate, and Presidential candidates
- **Notable Patterns**: 
  - Heavy concentration of missing values in specialized financial fields (70-96% nulls)
  - Core identification and summary financial data is well-populated
  - Data appears to be aggregated by candidate and election cycle

## Column Details

### Candidate Identification
- **cand_id** (STRING): Unique candidate identifier, no nulls, 28,356 unique values
- **cand_name** (STRING): Candidate full name, no nulls, 29,986 unique values
- **cand_ici** (STRING): Candidate incumbent/challenger/open seat status (I/C/O), 17.98% nulls
- **cand_pty_affiliation** (STRING): Party affiliation (DEM, REP, etc.), minimal nulls (0.13%), 80 unique parties
- **pty_cd** (INT64): Numeric party code (1-3), no nulls

### Geographic and Office Information
- **cand_office_st** (STRING): State/territory code, no nulls, 57 unique values including territories
- **cand_office_district** (INT64): Congressional district (0-53), minimal nulls (0.09%)

### Core Financial Data (Lower Null Rates)
- **ttl_receipts** (FLOAT64): Total receipts, 18.76% nulls, range -1.3M to 4.8B
- **ttl_disb** (FLOAT64): Total disbursements, 12.80% nulls, range -674K to 3.8B
- **ttl_indiv_contrib** (FLOAT64): Individual contributions, 38.21% nulls, range -1.2M to 18.8B

### Detailed Financial Data (High Null Rates)
- **trans_from_auth** (FLOAT64): Transfers from authorized committees, 89.64% nulls
- **trans_to_auth** (FLOAT64): Transfers to authorized committees, 92.46% nulls
- **cand_contrib** (FLOAT64): Candidate contributions, 74.07% nulls
- **cand_loans** (FLOAT64): Candidate loans, 73.83% nulls
- **other_loans** (FLOAT64): Other loans, 96.34% nulls
- **other_loan_repay** (FLOAT64): Other loan repayments, 96.79% nulls

### Cash Position
- **coh_bop** (FLOAT64): Cash on hand at beginning of period, 49.41% nulls
- **coh_cop** (FLOAT64): Cash on hand at close of period, 37.75% nulls

### Election Results (Very High Null Rates)
- **spec_election** (STRING): Special election result, 99.16% nulls
- **prim_election** (STRING): Primary election result, 72.04% nulls
- **run_election** (STRING): Runoff election result, 99.41% nulls
- **gen_election** (STRING): General election result, 77.30% nulls
- **gen_election_precent** (FLOAT64): General election percentage, 77.77% nulls

### Temporal Data
- **cvg_end_dt** (DATE): Coverage end date, no nulls, 6,398 unique dates
- **year** (INT64): Election year, no nulls, range 1980-2026
- **source_file** (STRING): Source data file, no nulls, 24 unique files

## Potential Query Considerations

### Good for Filtering
- **year**: Election cycles analysis
- **cand_office_st**: State-level analysis
- **cand_pty_affiliation**: Party comparisons
- **cand_office_district**: District-level analysis (House races)
- **source_file**: Data provenance filtering

### Good for Grouping/Aggregation
- **year**: Time series analysis
- **cand_office_st**: Geographic aggregation
- **cand_pty_affiliation**: Party-based analysis
- **cand_ici**: Incumbent vs challenger analysis
- **pty_cd**: Simplified party grouping

### Potential Join Keys
- **cand_id**: Primary key for candidate-level joins
- **cand_office_st + cand_office_district**: Geographic joins
- **year**: Time-based joins with other election data

### Data Quality Considerations
- Many financial detail columns have 70%+ null rates - consider using COALESCE or filtering for non-null values
- Negative values in financial columns may indicate corrections or refunds
- Election result fields are sparsely populated - primarily useful for winners/active candidates
- Some future years (2024-2026) present in data may be placeholders
- Financial amounts can be extremely large (billions) - consider scaling for visualization

## Keywords
political contributions, FEC data, campaign finance, election data, candidates, political parties, congressional districts, financial disclosures, campaign receipts, disbursements, incumbent challenger, primary elections, general elections

## Table and Column Documentation
*No table comment or column comments were provided in the source data.*