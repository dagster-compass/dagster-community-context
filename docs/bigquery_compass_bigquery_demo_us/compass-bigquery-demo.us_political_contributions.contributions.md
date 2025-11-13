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
# Table Analysis Summary: US Political Contributions

## Keywords
political contributions, campaign finance, FEC data, candidate contributions, election data, political parties, campaign receipts, disbursements, donations, federal elections, congressional candidates, Senate, House of Representatives

## Overall Dataset Characteristics

**Total Records:** 68,666 contribution records

**Time Period:** 1980-2026 (46 years of campaign finance data)

**Data Quality Observations:**
- Core identifiers (cand_id, cand_name, year) have 100% completeness
- Financial metrics show high null percentages (30-96%), indicating many candidates report only certain types of transactions
- Election outcome fields (spec_election, run_election, gen_election) are sparse (95%+ null), suggesting most records are interim filings rather than final results
- Data appears to be sourced from Federal Election Commission (FEC) files, organized by election cycle (source_file pattern: weball[YY].txt)

**Notable Patterns:**
- 24 distinct election cycles represented
- Biennial election pattern visible in year distribution
- Three-party system encoding (pty_cd: 1, 2, 3) likely representing Democrat, Republican, Other
- Geographic coverage spans all 50 states plus territories (57 unique state codes including "00" for national races)

## Column Details

### Candidate Identification
- **cand_id** (STRING): Primary identifier, alphanumeric format (e.g., H6ID01144). 28,356 unique candidates. 100% populated. First character likely indicates office type (H=House, S=Senate).
- **cand_name** (STRING): Candidate's name in "LASTNAME, FIRSTNAME" format. 29,986 unique values (more than cand_id suggests name variations). 100% populated.
- **cand_ici** (STRING): Incumbency status. 82% populated. Values: I=Incumbent, C=Challenger, O=Open seat.
- **cand_office_st** (STRING): State abbreviation. 100% populated. 57 unique values including territories and "00" for national.
- **cand_office_district** (INT64): Congressional district number (0-53). 99.91% populated. 0 typically indicates statewide/Senate race.

### Party Affiliation
- **pty_cd** (INT64): Numeric party code (1, 2, 3). 100% populated. Likely: 1=DEM, 2=REP, 3=Other.
- **cand_pty_affiliation** (STRING): Party abbreviation. 99.87% populated. 80 unique parties including DEM, REP, and numerous third parties (AIP, GRE, LIB, etc.).

### Financial Metrics (Receipt Side)
- **ttl_receipts** (FLOAT64): Total receipts. 81.24% populated. Range: -$1.3M to $4.8B. Negative values suggest corrections/amendments.
- **ttl_indiv_contrib** (FLOAT64): Individual contributions. 61.79% populated. Range: -$1.3M to $18.9B.
- **other_pol_cmte_contrib** (FLOAT64): PAC/political committee contributions. 38.17% populated. Range: -$35K to $1.9B.
- **pol_pty_contrib** (FLOAT64): Political party contributions. 20.23% populated. Range: -$11K to $9.6M.
- **cand_contrib** (FLOAT64): Candidate's own contributions. 25.93% populated. Range: -$35K to $2.8B.

### Loan Activity
- **cand_loans** (FLOAT64): Loans from candidate. 26.17% populated. Range: -$1.7M to $62.9M.
- **other_loans** (FLOAT64): Loans from other sources. 3.66% populated. Range: -$14K to $21M.
- **cand_loan_repay** (FLOAT64): Candidate loan repayments. 20.67% populated. Range: -$35.5K to $1.9B.
- **other_loan_repay** (FLOAT64): Other loan repayments. 3.21% populated. Range: -$3K to $50M.

### Financial Metrics (Disbursement Side)
- **ttl_disb** (FLOAT64): Total disbursements. 87.20% populated. Range: -$674K to $3.8B.
- **indiv_refunds** (FLOAT64): Refunds to individuals. 31.95% populated. Range: -$555K to $1.9B.
- **cmte_refunds** (FLOAT64): Refunds to committees. 13.86% populated. Range: -$132K to $48.4M.

### Cash Position
- **coh_bop** (FLOAT64): Cash on hand at beginning of period. 50.59% populated. Range: -$430K to $776M.
- **coh_cop** (FLOAT64): Cash on hand at close of period. 62.25% populated. Range: -$2.4M to $9.8B.
- **debts_owed_by** (FLOAT64): Outstanding debts. 40.68% populated. Range: -$346K to $73.7M.

### Transfer Activity
- **trans_from_auth** (FLOAT64): Transfers from authorized committees. 10.36% populated. Range: -$600K to $534M.
- **trans_to_auth** (FLOAT64): Transfers to authorized committees. 7.54% populated. Range: -$17.8K to $47.5M.

### Election Results
- **spec_election** (STRING): Special election indicator. 0.84% populated. Values: L=Loss, W=Win, R=Runoff.
- **prim_election** (STRING): Primary election result. 27.96% populated. Similar encoding plus additional codes.
- **run_election** (STRING): Runoff election result. 0.59% populated.
- **gen_election** (STRING): General election result. 22.70% populated. L/W/R encoding.
- **gen_election_precent** (FLOAT64): General election percentage. 22.23% populated. Range: 1-100.

### Temporal Data
- **cvg_end_dt** (DATE): Coverage end date. 100% populated. Range: 1980s-2025. Dates align with FEC reporting periods (typically quarter-end).
- **year** (INT64): Election year. 100% populated. Range: 1980-2026. 24 distinct values representing election cycles.
- **source_file** (STRING): Source filename. 100% populated. 24 unique files following "weball[YY].txt" pattern.

## Table and Column Documentation
No table comments or column comments are present in the provided schema.

## Query Considerations

### Ideal Filtering Columns
- **year**: Excellent for time-based queries; fully populated, indexed-friendly
- **cand_office_st**: Perfect for geographic filtering; complete data
- **pty_cd / cand_pty_affiliation**: Party-based analysis; nearly complete
- **cand_office_district**: District-level analysis; 99.91% populated
- **cand_ici**: Incumbency analysis; 82% populated
- **gen_election / prim_election**: Election outcomes (where populated)

### Ideal Grouping/Aggregation Columns
- **year**: Time series analysis by election cycle
- **cand_office_st**: State-level aggregations
- **pty_cd**: Party comparison analysis
- **cand_office_district**: District-level summaries
- **source_file**: Data quality checks by filing period

### Financial Analysis Considerations
- Most financial columns have 20-90% null rates; use COALESCE or NULL-safe functions
- Negative values exist across most financial fields (amendments/corrections)
- Very wide ranges suggest outliers (presidential vs. local races)
- Related columns can be cross-validated (receipts vs. contributions)

### Potential Join Keys
- **cand_id**: Primary key for joining with other FEC candidate tables
- **year + cand_office_st + cand_office_district**: Composite key for race-level analysis
- **source_file**: Could join to filing metadata tables

### Data Quality Considerations
1. **Missing election results**: 95%+ null in special/runoff fields means most records are interim filings
2. **Financial field sparsity**: Candidates file different forms based on activity level
3. **Negative values**: Represent amendments or corrections; should be handled in calculations
4. **Date ranges**: Some future dates present (2025-2026) indicate pre-filed data
5. **Name variations**: More unique names than candidate IDs suggests standardization issues
6. **Scale differences**: Presidential candidates vs. local races create extreme value ranges requiring careful aggregation strategies