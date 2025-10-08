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

- **Total Rows**: 68,666
- **Time Span**: 46 years (1980-2026) of US political contribution data
- **Data Quality**: Mixed quality with significant null values in many financial columns (ranging from 12% to 96% null)
- **Coverage**: Comprehensive candidate information with complete identifiers but sparse financial detail data
- **Data Sources**: 24 different source files (weball*.txt format) indicating regular data imports

## Column Details

### Candidate Identification
- **cand_id** (STRING): Complete candidate identifier, no nulls, 28,356 unique values
- **cand_name** (STRING): Complete candidate names, no nulls, 29,986 unique values
- **cand_ici** (STRING): Incumbent/Challenger/Open status, 18% null, values: I/C/O
- **cand_pty_affiliation** (STRING): Party affiliation, minimal nulls (0.13%), 80 parties including major parties (DEM/REP)
- **pty_cd** (INT64): Party code, complete data, values 1-3 (likely DEM=1, REP=2, Other=3)

### Geographic Information
- **cand_office_st** (STRING): State codes, complete data, 57 unique values including territories
- **cand_office_district** (INT64): District numbers, nearly complete (0.09% null), range 0-53

### Financial Data (High Null Percentages)
- **ttl_receipts** (FLOAT64): Total receipts, 19% null, wide range including negative values
- **ttl_disb** (FLOAT64): Total disbursements, 13% null, similar range pattern
- **ttl_indiv_contrib** (FLOAT64): Individual contributions, 38% null
- **trans_from_auth/trans_to_auth** (FLOAT64): Authorization transfers, 90%+ null (rarely used)
- **coh_bop/coh_cop** (FLOAT64): Cash on hand beginning/closing, 37-49% null
- **cand_contrib/cand_loans** (FLOAT64): Candidate contributions/loans, 73-74% null
- **other_loans/other_loan_repay** (FLOAT64): Other loans, 96%+ null (very sparse)
- **debts_owed_by** (FLOAT64): Debts owed, 59% null
- **pol_pty_contrib/other_pol_cmte_contrib** (FLOAT64): Political contributions, 62-80% null
- **indiv_refunds/cmte_refunds** (FLOAT64): Refunds, 68-86% null

### Election Information (Mostly Sparse)
- **spec_election** (STRING): Special election status, 99% null
- **prim_election** (STRING): Primary election results, 72% null, values: L/P/R/W/X
- **run_election** (STRING): Runoff election results, 99% null
- **gen_election** (STRING): General election results, 77% null, values: L/R/W
- **gen_election_precent** (FLOAT64): General election percentage, 78% null, range 1-100

### Temporal Information
- **cvg_end_dt** (DATE): Coverage end date, complete data, spans 1980-2025
- **year** (INT64): Election year, complete data, 24 unique years (1980-2026)
- **source_file** (STRING): Source file name, complete data, 24 unique files

## Potential Query Considerations

### Good for Filtering
- **year**: Complete temporal filtering capability
- **cand_office_st**: Complete state-based filtering
- **cand_pty_affiliation**: Near-complete party filtering
- **pty_cd**: Complete numeric party filtering
- **cand_ici**: Incumbent status filtering (consider 18% nulls)

### Good for Grouping/Aggregation
- **year**: Temporal analysis and trends
- **cand_office_st**: Geographic analysis by state
- **cand_pty_affiliation/pty_cd**: Party-based analysis
- **cand_office_district**: District-level analysis
- **source_file**: Data source analysis

### Potential Join Keys
- **cand_id**: Primary candidate identifier for joining with other candidate tables
- **cand_office_st**: State-based joins with geographic data
- **year**: Temporal joins with election or economic data

### Data Quality Considerations
- **Financial columns**: High null percentages require careful handling in aggregations
- **Election results**: Very sparse data limits election outcome analysis
- **Negative values**: Financial columns contain negative values (refunds, corrections)
- **Data completeness varies by year**: Newer data may have different completion rates
- **Missing value patterns**: Consider using COALESCE or IFNULL for financial calculations

## Keywords
political contributions, campaign finance, FEC data, election data, candidate contributions, political donations, campaign receipts, disbursements, political parties, congressional districts, incumbent challenger open, DEM REP, state elections, federal elections

## Table and Column Docs
No table comment or column comments were provided in the analysis.