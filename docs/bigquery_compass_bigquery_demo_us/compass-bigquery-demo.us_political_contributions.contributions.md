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
# Table Summary: compass-bigquery-demo.us_political_contributions.contributions

## Overall Dataset Characteristics

- **Total Rows**: 68,666 records
- **Data Coverage**: Political contribution data spanning 1980-2026 (24 election cycles)
- **Data Quality**: Generally good completeness for core identifying fields, but significant missingness in financial detail columns
- **Notable Patterns**: 
  - High null percentages in specialized financial columns (70-96% missing)
  - Complete data for candidate identification and basic attributes
  - Time series data with yearly aggregation from multiple source files

## Column Details

### Candidate Identification
- **cand_name** (STRING): Complete candidate names, no nulls, 29,986 unique values
- **cand_id** (STRING): Unique candidate identifiers, no nulls, 28,356 unique values (potential primary key)
- **cand_ici** (STRING): Incumbent/Challenger/Open status (C/I/O), 18% nulls
- **cand_pty_affiliation** (STRING): Party affiliation, minimal nulls (0.13%), 80 different parties

### Political Classification
- **pty_cd** (INT64): Numeric party code (1-3), no nulls, likely maps to major parties
- **cand_office_st** (STRING): State/territory codes, no nulls, 57 unique values including "00" for federal
- **cand_office_district** (INT64): District numbers 0-53, minimal nulls (0.09%)

### Financial Data (High Missingness)
- **ttl_receipts** (FLOAT64): Total receipts, 19% nulls, range -$1.3M to $4.8B
- **ttl_disb** (FLOAT64): Total disbursements, 13% nulls, range -$674K to $3.8B
- **ttl_indiv_contrib** (FLOAT64): Individual contributions, 38% nulls, range -$1.3M to $18.9B
- **coh_cop/coh_bop** (FLOAT64): Cash on hand (38-49% nulls)
- **Specialized columns**: Very high missingness (70-96%) for loans, transfers, refunds

### Election Performance
- **Election columns** (spec_election, prim_election, run_election, gen_election): 72-99% nulls
- **gen_election_precent** (FLOAT64): Election percentage, 78% nulls, range 1-100%

### Temporal Data
- **year** (INT64): Election year, no nulls, complete 1980-2026 coverage
- **cvg_end_dt** (DATE): Coverage end date, no nulls, 6,398 unique dates
- **source_file** (STRING): Source file identifier, no nulls, 24 files (weball*.txt format)

## Potential Query Considerations

### Good for Filtering
- **year**: Complete temporal filtering capability
- **cand_office_st**: Geographic analysis by state
- **cand_pty_affiliation**: Party-based analysis
- **pty_cd**: Simplified party grouping (1-3 codes)

### Good for Grouping/Aggregation
- **year**: Time series analysis
- **cand_office_st**: Geographic aggregation
- **cand_pty_affiliation/pty_cd**: Party analysis
- **cand_office_district**: District-level analysis

### Potential Join Keys
- **cand_id**: Primary candidate identifier for joining with other candidate tables
- **year + cand_office_st + cand_office_district**: Composite key for election-specific joins

### Data Quality Considerations
- **Financial columns**: High missingness requires careful NULL handling in aggregations
- **Election performance data**: Limited availability (70-99% nulls) may restrict analysis scope
- **Negative values**: Present in financial columns, may indicate corrections or refunds
- **Date ranges**: Some future dates (2025-2026) suggest projected or preliminary data

## Keywords
political contributions, campaign finance, FEC data, election data, candidates, receipts, disbursements, contributions, political parties, elections, campaign funding, federal elections, state elections, congressional districts

## Table and Column Documentation
No table comment or column comments were provided in the analysis report.