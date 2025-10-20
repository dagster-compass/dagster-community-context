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
# Table Analysis Summary: compass-bigquery-demo.us_political_contributions.contributions

## Overall Dataset Characteristics

- **Total Rows**: 68,666 records
- **Data Quality**: The dataset has significant missing data patterns, with many financial columns having high null percentages (ranging from 37% to 96%)
- **Time Span**: Data spans from 1980 to 2026, with 24 distinct years represented
- **Geographic Coverage**: Contains data for all US states plus territories (57 unique values in cand_office_st)
- **Data Sources**: 24 different source files, following the pattern "weball[YY].txt"

## Column Details

### Identification Columns
- **cand_id** (STRING): Primary identifier with 28,356 unique candidates, no nulls
- **cand_name** (STRING): 29,986 unique candidate names, no nulls
- **source_file** (STRING): 24 files indicating data source/year, no nulls

### Categorical Columns
- **cand_ici** (STRING): Incumbency status (17.98% null) - C (Challenger), I (Incumbent), O (Open seat)
- **pty_cd** (INT64): Party code (1-3), no nulls
- **cand_pty_affiliation** (STRING): 80 different party affiliations (0.13% null), includes major parties like REP, DEM, and many minor parties
- **cand_office_st** (STRING): State/territory codes (57 unique), no nulls
- **cand_office_district** (INT64): District numbers 0-53 (0.09% null)

### Financial Columns (High Null Rates)
- **ttl_receipts** (FLOAT64): Total receipts (18.76% null), wide range including negative values
- **ttl_disb** (FLOAT64): Total disbursements (12.80% null)
- **ttl_indiv_contrib** (FLOAT64): Individual contributions (38.21% null)
- **coh_cop/coh_bop** (FLOAT64): Cash on hand (37.75% and 49.41% null respectively)
- **trans_from_auth/trans_to_auth** (FLOAT64): Authorization transfers (89.64% and 92.46% null)
- **cand_contrib** (FLOAT64): Candidate contributions (74.07% null)
- **cand_loans** (FLOAT64): Candidate loans (73.83% null)
- **other_loans** (FLOAT64): Other loans (96.34% null)
- **debts_owed_by** (FLOAT64): Outstanding debts (59.32% null)
- **pol_pty_contrib** (FLOAT64): Political party contributions (79.77% null)
- **other_pol_cmte_contrib** (FLOAT64): Other political committee contributions (61.83% null)

### Election Results Columns (Very High Null Rates)
- **spec_election** (STRING): Special election results (99.16% null)
- **run_election** (STRING): Runoff election results (99.41% null)
- **prim_election** (STRING): Primary election results (72.04% null)
- **gen_election** (STRING): General election results (77.30% null)
- **gen_election_precent** (FLOAT64): General election percentage (77.77% null)

### Temporal Column
- **cvg_end_dt** (DATE): Coverage end date, no nulls, spans from 1989 to 2024
- **year** (INT64): Election year (1980-2026), no nulls

## Potential Query Considerations

### Good for Filtering:
- **year**: Complete data, good for time-based analysis
- **cand_office_st**: State-level filtering
- **cand_pty_affiliation**: Party-based analysis
- **cand_ici**: Incumbency analysis
- **source_file**: Data source filtering

### Good for Grouping/Aggregation:
- **year**: Temporal trends
- **cand_office_st**: Geographic analysis
- **cand_pty_affiliation**: Party comparison
- **cand_office_district**: District-level analysis
- **pty_cd**: Simplified party grouping

### Potential Join Keys:
- **cand_id**: Primary key for candidate-level joins
- **cand_office_st + cand_office_district**: Geographic joins
- **year**: Temporal joins

### Data Quality Considerations:
- Financial columns have very high null rates (60-96% for some)
- Election result columns are mostly empty
- Negative values exist in financial columns (may indicate refunds/corrections)
- Some financial ranges are extremely wide, suggesting outliers
- Missing data patterns suggest not all candidates file complete financial reports

## Keywords
US political contributions, campaign finance, FEC data, candidate contributions, election data, political campaigns, financial disclosures, incumbency, party affiliations, state elections, district elections, campaign receipts, disbursements, individual contributions, political action committees, PAC, candidate loans, debt analysis, election results, primary elections, general elections

## Table and Column Documentation
No table comment or column comments were provided in the analysis report.