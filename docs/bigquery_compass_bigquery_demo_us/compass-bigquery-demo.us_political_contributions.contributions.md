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
# Comprehensive Table Summary: US Political Contributions

## Keywords
political contributions, campaign finance, FEC data, candidate contributions, election data, campaign receipts, political donations, candidate loans, PAC contributions, election results, congressional candidates, presidential candidates, campaign disbursements, political party affiliations, campaign finance reports, federal election data

## Overall Dataset Characteristics

**Total Rows:** 68,666

**General Description:** This table contains comprehensive U.S. political campaign contribution and financial data spanning from 1980 to 2026. It tracks candidate financial activities including receipts, disbursements, loans, contributions, and election outcomes.

**Data Quality Observations:**
- Most columns have significant null values (many >50%), indicating sparse or optional reporting
- Core identification fields (cand_id, cand_name, year, cvg_end_dt) have complete or near-complete data
- Financial fields show high null percentages, suggesting not all candidates report all financial categories
- Some data anomalies exist (e.g., negative values in financial fields, future years up to 2026)
- Wide value ranges in financial columns indicate diverse campaign sizes from local to presidential races

**Notable Patterns:**
- Data sourced from annual batch files (weball[YY].txt format)
- Even-numbered years dominate (election cycle pattern)
- Three-party system encoding (pty_cd: 1, 2, 3 likely representing Democrat, Republican, Other)
- Coverage dates (cvg_end_dt) show 6,398 unique reporting periods

## Table and Column Documentation

**Table Comment:** Not provided in the analysis report.

**Column Comments:** No column-level comments were provided in the analysis report.

## Detailed Column Analysis

### Identification & Candidate Information

**cand_id (STRING)**
- Complete data (0% null)
- 28,356 unique candidate identifiers
- Format appears standardized (e.g., H0TX13012, S6RI00155, P20002184)
- First letter likely indicates office type (H=House, S=Senate, P=Presidential)
- **Query Use:** Primary key for candidate identification, excellent for joins and filtering

**cand_name (STRING)**
- Complete data (0% null)
- 29,986 unique names (more than unique IDs, suggesting name variations)
- Format: LASTNAME, FIRSTNAME MIDDLE/SUFFIX
- **Query Use:** Human-readable candidate identification, text search queries

**cand_ici (STRING)**
- 17.98% null values
- 3 unique values: C (Challenger), I (Incumbent), O (Open seat)
- **Query Use:** Filter by candidate incumbency status for competitive analysis

**cand_office_st (STRING)**
- Complete data (0% null)
- 57 unique values including all 50 states plus territories (AS, DC, GU, etc.) and "00" (likely presidential)
- **Query Use:** Geographic filtering and grouping, state-level analysis

**cand_office_district (INT64)**
- Nearly complete (0.09% null)
- 54 unique values (0-53)
- 0 likely indicates statewide races (Senate, Governor)
- **Query Use:** Congressional district analysis, combined with state for precise geographic filtering

### Party Affiliation

**pty_cd (INT64)**
- Complete data (0% null)
- 3 unique values: 1, 2, 3
- Likely encoding: 1=Democrat, 2=Republican, 3=Other
- **Query Use:** Numeric party filtering and grouping

**cand_pty_affiliation (STRING)**
- Nearly complete (0.13% null)
- 80 unique party codes including REP, DEM, DFL (Minnesota Democratic-Farmer-Labor), and many third parties
- **Query Use:** Detailed party analysis including third parties and state-specific parties

### Financial Metrics - Receipts

**ttl_receipts (FLOAT64)**
- 18.76% null
- Range: -$1.3M to $4.8B (negative values indicate corrections/amendments)
- 47,984 unique values showing granular financial tracking
- **Query Use:** Total fundraising analysis, candidate financial strength comparison

**ttl_indiv_contrib (FLOAT64)**
- 38.21% null
- Range: -$1.3M to $18.9B
- 35,215 unique values
- **Query Use:** Grassroots fundraising analysis, individual donor contribution tracking

**trans_from_auth (FLOAT64)**
- 89.64% null (rarely used)
- Range: -$600K to $533.7M
- **Query Use:** Transfers between authorized committees (limited use cases)

**other_pol_cmte_contrib (FLOAT64)**
- 61.83% null
- Range: -$35.8K to $1.9B
- **Query Use:** PAC and political committee contribution analysis

**pol_pty_contrib (FLOAT64)**
- 79.77% null
- Range: -$11.1K to $9.6M
- **Query Use:** Party support analysis, coordinated expenditure tracking

### Financial Metrics - Disbursements & Cash

**ttl_disb (FLOAT64)**
- 12.80% null (more complete than receipts)
- Range: -$674K to $3.8B
- 52,253 unique values
- **Query Use:** Campaign spending analysis, burn rate calculations

**coh_cop (FLOAT64)** - Cash on Hand, Close of Period
- 37.75% null
- Range: -$2.4M to $9.8B
- **Query Use:** Campaign financial health, remaining resources

**coh_bop (FLOAT64)** - Cash on Hand, Beginning of Period
- 49.41% null
- **Query Use:** Starting financial position analysis

**indiv_refunds (FLOAT64)**
- 68.05% null
- Range: -$555K to $1.9B
- **Query Use:** Contribution return analysis, compliance tracking

**cmte_refunds (FLOAT64)**
- 86.14% null (rare occurrences)
- Range: -$132K to $48.4M
- **Query Use:** Committee refund tracking

### Loan Information

**cand_contrib (FLOAT64)**
- 74.07% null
- Range: -$35.1K to $2.8B
- **Query Use:** Self-funding candidate analysis

**cand_loans (FLOAT64)**
- 73.83% null
- Range: -$1.7M to $62.9M
- **Query Use:** Candidate self-loan tracking

**other_loans (FLOAT64)**
- 96.34% null (very rare)
- Range: -$14K to $21M
- **Query Use:** Third-party loan analysis

**cand_loan_repay (FLOAT64)**
- 79.33% null
- Range: -$35.5K to $1.9B
- **Query Use:** Loan repayment tracking, campaign debt management

**other_loan_repay (FLOAT64)**
- 96.79% null
- Range: -$3K to $50M
- **Query Use:** External loan repayment analysis

**debts_owed_by (FLOAT64)**
- 59.32% null
- Range: -$346K to $73.7M
- **Query Use:** Outstanding debt analysis, financial viability assessment

### Election Results

**spec_election (STRING)**
- 99.16% null (special elections are rare)
- Values: L (Loss), R (Runoff), W (Win), l (lowercase variant)
- **Query Use:** Special election outcome filtering

**run_election (STRING)**
- 99.41% null
- Values: L, R, W
- **Query Use:** Runoff election tracking

**prim_election (STRING)**
- 72.04% null
- Values: 0, L, P, R, W, X, l, w
- **Query Use:** Primary election outcomes

**gen_election (STRING)**
- 77.30% null
- Values: L (Loss), R (Runoff), W (Win), l, w
- **Query Use:** General election outcome analysis

**gen_election_precent (FLOAT64)**
- 77.77% null
- Range: 1.0 to 100.0 (vote percentage)
- **Query Use:** Vote share analysis, competitive race identification

### Administrative Fields

**cvg_end_dt (DATE)**
- Complete data (0% null)
- 6,398 unique dates
- Reporting period end dates (quarterly/annual)
- **Query Use:** Time-series analysis, reporting period filtering

**source_file (STRING)**
- Complete data (0% null)
- 24 unique files (weball[YY].txt format)
- **Query Use:** Data provenance tracking, batch identification

**year (INT64)**
- Complete data (0% null)
- Range: 1980 to 2026
- 24 unique years
- **Query Use:** Primary temporal filtering and grouping dimension

## Query Considerations

### Excellent Filtering Columns:
- **year**: Complete data, clear temporal dimension
- **cand_office_st**: Complete data, geographic filtering
- **pty_cd / cand_pty_affiliation**: Party-based analysis
- **cand_ici**: Incumbency advantage studies
- **gen_election / prim_election**: Winner/loser analysis

### Excellent Grouping/Aggregation Columns:
- **year**: Temporal trends
- **cand_office_st**: State-level summaries
- **pty_cd**: Party comparisons
- **cand_office_district** (with state): District-level analysis
- **source_file**: Batch-level statistics

### Potential Join Keys:
- **cand_id**: Primary key for candidate-related joins
- **cand_office_st + cand_office_district + year**: Geographic-temporal joins
- **year**: Time-series joins with other datasets

### Data Quality Considerations:

1. **High Null Percentages**: Many financial fields have 60-95% nulls. Queries should use COALESCE or handle nulls explicitly. Consider filtering WHERE column IS NOT NULL for meaningful analysis.

2. **Negative Values**: Financial columns contain negative values (corrections/amendments). Consider ABS() or filtering for analytical purposes.

3. **Future Dates**: Year extends to 2026, suggesting forward-looking or placeholder records. Validate date ranges for historical analysis.

4. **Case Sensitivity**: Election result columns have lowercase variants (l, w). Use UPPER() for consistent comparisons.

5. **Sparse Election Data**: 70-99% nulls in election outcome columns. Only filter on these when specifically analyzing election results.

6. **Scale Variations**: Financial values range from dollars to billions. Consider using formatting or scaling in queries for readability.

7. **Name Variations**: More unique names than IDs suggests inconsistent name formatting. Use cand_id for precise matching.

### Recommended Query Patterns:

- **Financial Analysis**: Focus on ttl_receipts, ttl_disb, ttl_indiv_contrib (lower null rates)
- **Temporal Trends**: Group by year with complete date coverage
- **Geographic Analysis**: Combine cand_office_st and cand_office_district
- **Competitive Analysis**: Filter on gen_election_precent for close races (e.g., 45-55%)
- **Party Comparison**: Use pty_cd for broad analysis, cand_pty_affiliation for detailed third-party studies
- **Incumbency Effects**: Filter cand_ici IS NOT NULL for meaningful comparisons