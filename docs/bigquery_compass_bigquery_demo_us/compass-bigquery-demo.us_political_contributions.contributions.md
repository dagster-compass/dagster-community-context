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
# Comprehensive Data Summary: US Political Contributions Table

## Overall Dataset Characteristics

**Total Rows:** 68,666

**General Description:** This table contains US political campaign contribution and financial data spanning from 1980 to 2026. Each row represents a candidate's financial summary for a specific election cycle, including receipts, disbursements, contributions, and election results.

**Data Quality Observations:**
- High quality for core identification fields (cand_id, cand_name, year) with 0% nulls
- Significant null percentages in financial detail columns (ranging from 12% to 96%)
- Very high null rates in transfer-related fields (trans_from_auth: 89.64%, trans_to_auth: 92.46%)
- Election-specific fields show high null rates (spec_election: 99.16%, run_election: 99.41%)
- Financial data shows some negative values, likely representing refunds or corrections

**Notable Patterns:**
- Data is organized by year (1980-2026) and sourced from annual text files
- Covers federal candidates across all US states and territories
- Includes various party affiliations (80 unique values) with Democratic and Republican being predominant
- Financial ranges span from negative values to billions of dollars

## Column-by-Column Analysis

### **Identification Columns**

#### cand_id (STRING)
- **Purpose:** Unique candidate identifier
- **Characteristics:** 28,356 unique values, 0% null
- **Format Pattern:** Alphanumeric code (e.g., H6MD04258, H2AR02087)
- **Usage:** Primary key for candidate identification, ideal for joins

#### cand_name (STRING)
- **Purpose:** Candidate's full name
- **Characteristics:** 29,986 unique values, 0% null
- **Format:** Last name first, often with titles (e.g., "CARTWRIGHT, NICHOLAS", "HOFFMAN, DOUGLAS L. MR.")
- **Usage:** Human-readable identifier, searchable field

### **Candidate Status & Affiliation**

#### cand_ici (STRING)
- **Purpose:** Candidate incumbent/challenger/open seat status
- **Null Rate:** 17.98%
- **Values:** 'C' (Challenger), 'I' (Incumbent), 'O' (Open seat)
- **Usage:** Filter for competitive race analysis

#### pty_cd (INT64)
- **Purpose:** Party code (numeric)
- **Characteristics:** 0% null, values 1-3
- **Usage:** Simple numeric party classification

#### cand_pty_affiliation (STRING)
- **Purpose:** Party affiliation abbreviation
- **Null Rate:** 0.13%
- **Unique Values:** 80 different parties
- **Common Values:** DEM, REP, GRE, (I)
- **Usage:** Detailed party analysis and filtering

### **Major Financial Metrics**

#### ttl_receipts (FLOAT64)
- **Purpose:** Total campaign receipts
- **Null Rate:** 18.76%
- **Range:** -$1.3M to $4.8B
- **Characteristics:** 47,984 unique values showing high variance
- **Comment:** Negative values likely represent corrections/adjustments
- **Usage:** Key metric for campaign finance analysis, aggregation candidate

#### ttl_disb (FLOAT64)
- **Purpose:** Total disbursements
- **Null Rate:** 12.80%
- **Range:** -$674K to $3.8B
- **Characteristics:** 52,253 unique values
- **Usage:** Spending analysis, comparison with receipts

#### coh_bop (FLOAT64)
- **Purpose:** Cash on hand at beginning of period
- **Null Rate:** 49.41%
- **Range:** -$430K to $775M
- **Usage:** Starting financial position analysis

#### coh_cop (FLOAT64)
- **Purpose:** Cash on hand at close of period
- **Null Rate:** 37.75%
- **Range:** -$2.3M to $9.7B
- **Usage:** Ending financial position, campaign viability indicator

### **Contribution Sources**

#### ttl_indiv_contrib (FLOAT64)
- **Purpose:** Total individual contributions
- **Null Rate:** 38.21%
- **Range:** -$1.2M to $18.8B
- **Characteristics:** 35,215 unique values
- **Usage:** Analysis of grassroots support, major aggregation target

#### other_pol_cmte_contrib (FLOAT64)
- **Purpose:** Contributions from other political committees
- **Null Rate:** 61.83%
- **Range:** -$35K to $1.9B
- **Usage:** PAC and committee support analysis

#### pol_pty_contrib (FLOAT64)
- **Purpose:** Political party contributions
- **Null Rate:** 79.77%
- **Range:** -$11K to $9.6M
- **Usage:** Party support analysis

### **Candidate Self-Financing**

#### cand_contrib (FLOAT64)
- **Purpose:** Candidate's own contributions
- **Null Rate:** 74.07%
- **Range:** -$35K to $2.8B
- **Usage:** Self-funding analysis

#### cand_loans (FLOAT64)
- **Purpose:** Loans from candidate
- **Null Rate:** 73.83%
- **Range:** -$1.6M to $62.8M
- **Usage:** Candidate investment analysis

#### cand_loan_repay (FLOAT64)
- **Purpose:** Repayment of candidate loans
- **Null Rate:** 79.33%
- **Range:** -$35K to $1.9B
- **Usage:** Loan repayment tracking

### **Other Loans**

#### other_loans (FLOAT64)
- **Null Rate:** 96.34% (rarely used)
- **Range:** -$13K to $20.9M
- **Usage:** Non-candidate loan analysis

#### other_loan_repay (FLOAT64)
- **Null Rate:** 96.79% (rarely used)
- **Range:** -$3K to $49.9M
- **Usage:** Loan repayment tracking

### **Transfer Fields**

#### trans_from_auth (FLOAT64)
- **Null Rate:** 89.64% (rarely populated)
- **Range:** -$600K to $533M
- **Usage:** Transfers from authorized committees

#### trans_to_auth (FLOAT64)
- **Null Rate:** 92.46% (rarely populated)
- **Range:** -$17K to $47.5M
- **Usage:** Transfers to authorized committees

### **Debts & Refunds**

#### debts_owed_by (FLOAT64)
- **Null Rate:** 59.32%
- **Range:** -$346K to $73.6M
- **Usage:** Outstanding debt analysis

#### indiv_refunds (FLOAT64)
- **Null Rate:** 68.05%
- **Range:** -$555K to $1.9B
- **Usage:** Individual contribution refunds

#### cmte_refunds (FLOAT64)
- **Null Rate:** 86.14%
- **Range:** -$131K to $48.4M
- **Usage:** Committee contribution refunds

### **Geographic & Office Information**

#### cand_office_st (STRING)
- **Characteristics:** 0% null, 57 unique values
- **Values:** US state codes plus '00' (likely for federal/at-large)
- **Usage:** Critical for geographic filtering and analysis

#### cand_office_district (INT64)
- **Null Rate:** 0.09%
- **Range:** 0-53
- **Note:** 0 likely indicates Senate or statewide races
- **Usage:** District-level analysis, combined with state for specific races

### **Election Results**

#### spec_election (STRING)
- **Null Rate:** 99.16% (rarely populated)
- **Values:** L (Loss), R (Runoff), W (Win)
- **Usage:** Special election outcomes

#### prim_election (STRING)
- **Null Rate:** 72.04%
- **Values:** L, P, R, W, X (various case formats)
- **Usage:** Primary election results

#### run_election (STRING)
- **Null Rate:** 99.41% (rarely populated)
- **Values:** L, R, W
- **Usage:** Runoff election results

#### gen_election (STRING)
- **Null Rate:** 77.30%
- **Values:** L, R, W (various case formats)
- **Usage:** General election results, important for winner analysis

#### gen_election_precent (FLOAT64)
- **Null Rate:** 77.77%
- **Range:** 1-100
- **Usage:** Vote percentage in general election

### **Temporal Fields**

#### cvg_end_dt (DATE)
- **Characteristics:** 0% null, 6,398 unique values
- **Range:** Covers dates from 1993 to 2024
- **Usage:** Reporting period end date, temporal analysis

#### year (INT64)
- **Characteristics:** 0% null, 24 unique values
- **Range:** 1980-2026
- **Usage:** Primary temporal dimension for queries, excellent for grouping

#### source_file (STRING)
- **Characteristics:** 0% null, 24 unique values
- **Format:** weballYY.txt pattern
- **Usage:** Data lineage tracking, quality verification

## Query Considerations

### **Best Columns for Filtering:**
- `year` - Temporal filtering (election cycles)
- `cand_office_st` - Geographic filtering
- `cand_pty_affiliation` - Party analysis
- `cand_ici` - Incumbent status filtering
- `gen_election` - Winner/loser filtering (when not null)
- `cand_office_district` - District-specific queries

### **Best Columns for Grouping/Aggregation:**
- `year` - Time series analysis
- `cand_office_st` - State-level aggregations
- `cand_pty_affiliation` - Party comparisons
- `cand_ici` - Incumbent vs. challenger analysis
- `cand_office_district` - District rollups
- Financial columns (ttl_receipts, ttl_disb, ttl_indiv_contrib) - Sum, average calculations

### **Potential Join Keys:**
- `cand_id` - Primary candidate identifier
- `cand_office_st` + `cand_office_district` + `year` - Race-level joins
- `year` - Temporal joins with other political datasets

### **Data Quality Considerations:**

1. **High Null Rates:** Many financial detail columns have >60% nulls. Queries should use COALESCE or handle nulls explicitly.

2. **Negative Values:** Financial fields contain negative values (likely corrections/refunds). Consider ABS() functions or filtering for analysis.

3. **Inconsistent Case:** Election result fields show mixed case ('W' vs 'w'). Use UPPER() or LOWER() for consistent comparisons.

4. **Missing Values:** Election result fields are mostly null - only populated when results are available.

5. **Date Ranges:** The `cvg_end_dt` field may not align perfectly with `year` due to reporting periods.

6. **Outliers:** Extreme values in financial fields (billions) may represent cumulative totals or data quality issues.

## Keywords

political contributions, campaign finance, FEC data, election data, campaign receipts, campaign disbursements, political candidates, incumbent challenger, party affiliation, individual contributions, PAC contributions, candidate loans, election results, congressional districts, US states, political parties, Democratic, Republican, primary elections, general elections, campaign spending, cash on hand, political committees, federal elections, election cycles, fundraising, vote percentage, special elections, runoff elections, debt, refunds, 1980-2026

## Table and Column Docs

**Table Comment:** Not provided in the analysis report.

**Column Comments:** No column-level comments or documentation were provided in the analysis report. The column meanings have been inferred from naming conventions and data patterns.