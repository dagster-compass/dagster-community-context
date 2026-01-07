---
columns:
- current_high (FLOAT64)
- current_low (FLOAT64)
- current_price (FLOAT64)
- current_volume (FLOAT64)
- date (DATE)
- exchange (STRING)
- high_1mo (FLOAT64)
- high_1yr (FLOAT64)
- high_3mo (FLOAT64)
- high_6mo (FLOAT64)
- high_9mo (FLOAT64)
- low_1mo (FLOAT64)
- low_1yr (FLOAT64)
- low_3mo (FLOAT64)
- low_6mo (FLOAT64)
- low_9mo (FLOAT64)
- month_date (DATE)
- monthly_avg_close (FLOAT64)
- monthly_avg_high (FLOAT64)
- monthly_avg_low (FLOAT64)
- monthly_avg_open (FLOAT64)
- monthly_avg_volume (FLOAT64)
- pct_change_1mo (FLOAT64)
- pct_change_1yr (FLOAT64)
- pct_change_3mo (FLOAT64)
- pct_change_6mo (FLOAT64)
- pct_change_9mo (FLOAT64)
- pct_change_q1_forward (FLOAT64)
- pct_change_q2_forward (FLOAT64)
- pct_change_q3_forward (FLOAT64)
- pct_change_q4_forward (FLOAT64)
- quarter_num (INT64)
- quarterly_avg_close (FLOAT64)
- quarterly_avg_high (FLOAT64)
- quarterly_avg_low (FLOAT64)
- quarterly_avg_open (FLOAT64)
- quarterly_avg_volume (FLOAT64)
- std_diff_1mo (FLOAT64)
- std_diff_1yr (FLOAT64)
- std_diff_3mo (FLOAT64)
- std_diff_6mo (FLOAT64)
- std_diff_9mo (FLOAT64)
- symbol (STRING)
- year_month (STRING)
- year_quarter (STRING)
- year_val (INT64)
schema_hash: 91d6707310c607dd4be98ffa932c6e84cbe6494ca58762d292141382235612b2

---
# Table Summary: US Sector Analysis Returns

## Overall Dataset Characteristics

This table contains **1,354 rows** of historical financial performance data for US sector ETFs traded on the ARCX exchange. The dataset spans from **2012 to 2026** (15 years) with **169 unique months** of data across **11 different sector symbols**. 

**Data Quality:** The dataset has excellent quality for core fields (0% nulls) but contains many completely unpopulated columns (100% nulls) that appear to be placeholders for current/recent performance metrics. Forward-looking percentage change columns have modest null percentages (3-11%), likely representing edge cases where future data isn't yet available.

**Notable Patterns:**
- Monthly and quarterly aggregated OHLCV (Open, High, Low, Close, Volume) data
- Forward-looking performance indicators (Q1-Q4 percentage changes)
- Time-series structure with multiple temporal granularities (monthly, quarterly, yearly)
- All 11 sector symbols trade exclusively on ARCX exchange

## Column Details

### Time Dimensions

**month_date** (DATE)
- Primary temporal key at monthly granularity
- 169 unique months from 2012-2026
- No nulls; consistently populated
- Represents the first day of each month

**year_month** (STRING)
- Alternative monthly identifier in YYYY-MM format
- 169 unique values matching month_date cardinality
- Useful for string-based temporal filtering

**year_quarter** (STRING)
- Quarterly identifier in YYYY-QX format (e.g., "2018-Q3")
- 57 unique quarters spanning the dataset
- Enables quarter-over-quarter analysis

**quarter_num** (INT64)
- Quarter number within year (1-4)
- Useful for seasonal analysis and grouping

**year_val** (INT64)
- Year as integer (2012-2026)
- 15 unique years
- Primary year-level aggregation key

### Security Identifiers

**symbol** (STRING)
- 11 unique sector ETF symbols: XLB, XLC, XLE, XLF, XLI, XLK, XLP, XLRE, XLU, XLV
- No nulls; represents major US sector classifications
- Key dimension for sector-level analysis

**exchange** (STRING)
- Single value: "ARCX" (NYSE Arca)
- All securities trade on the same exchange
- Constant field with limited analytical value

### Monthly Aggregated Metrics

**monthly_avg_close** (FLOAT64)
- Range: $23.73 to $289.54
- 1,352 unique values (nearly all distinct)
- Average closing price for the month
- No nulls; primary price metric

**monthly_avg_open** (FLOAT64)
- Range: $23.74 to $289.94
- 1,353 unique values
- Average opening price for the month

**monthly_avg_high** (FLOAT64)
- Range: $23.93 to $291.74
- 1,354 unique values (all rows unique)
- Average high price for the month

**monthly_avg_low** (FLOAT64)
- Range: $23.49 to $287.35
- 1,353 unique values
- Average low price for the month

**monthly_avg_volume** (FLOAT64)
- Range: 2.5M to 93.2M shares
- 1,354 unique values
- Average daily volume for the month
- Wide range indicates varying liquidity across sectors

### Quarterly Aggregated Metrics

**quarterly_avg_open** (FLOAT64)
- Range: $24.12 to $264.94
- 462 unique values
- Quarterly average of opening prices

**quarterly_avg_high** (FLOAT64)
- Range: $24.42 to $266.22
- 462 unique values

**quarterly_avg_low** (FLOAT64)
- Range: $23.74 to $263.10
- 461 unique values

**quarterly_avg_close** (FLOAT64)
- Range: $24.06 to $264.96
- 462 unique values
- Key metric for quarterly performance

**quarterly_avg_volume** (FLOAT64)
- Range: 2.9M to 93.2M shares
- 462 unique values

### Forward-Looking Performance Indicators

**pct_change_q1_forward** (FLOAT64)
- **3.25% nulls** (44 rows)
- Range: -22.34% to +32.94%
- Next quarter performance prediction/actual
- 388 unique values

**pct_change_q2_forward** (FLOAT64)
- **5.69% nulls** (77 rows)
- Range: -37.42% to +50.8%
- Two quarters forward performance
- 397 unique values

**pct_change_q3_forward** (FLOAT64)
- **8.12% nulls** (110 rows)
- Range: -40.22% to +61.82%
- Three quarters forward performance
- 399 unique values

**pct_change_q4_forward** (FLOAT64)
- **10.56% nulls** (143 rows)
- Range: -41.97% to +64.03%
- Four quarters (1 year) forward performance
- 397 unique values
- Increasing null percentage reflects data availability at dataset edges

### Unpopulated Columns (100% Null)

The following columns are completely empty and appear to be placeholders for current/real-time data:
- **date, current_price, current_high, current_low, current_volume**
- **high_1yr, low_1yr, std_diff_1yr, pct_change_1yr**
- **high_9mo, low_9mo, std_diff_9mo, pct_change_9mo**
- **high_6mo, low_6mo, std_diff_6mo, pct_change_6mo**
- **high_3mo, low_3mo, std_diff_3mo, pct_change_3mo**
- **high_1mo, low_1mo, std_diff_1mo, pct_change_1mo**

These fields should be excluded from queries or checked for non-null values in specific use cases.

## Query Considerations

### Excellent Filtering Columns
- **symbol**: Filter by specific sector (11 options)
- **year_val**: Year-based filtering (2012-2026)
- **year_quarter**: Quarter-level filtering
- **quarter_num**: Seasonal analysis (1-4)
- **month_date**: Precise temporal filtering

### Excellent Grouping/Aggregation Columns
- **symbol**: Sector-level aggregations
- **year_val**: Annual trends
- **year_quarter**: Quarterly analysis
- **quarter_num**: Seasonal patterns across years
- **exchange**: Not useful (constant value)

### Join Keys & Relationships
- **Primary Key**: Likely composite of (month_date, symbol)
- **Temporal joins**: month_date, year_month, year_quarter
- **Sector analysis**: symbol as dimension key
- Could join to other sector/economic tables on symbol or temporal keys

### Data Quality Considerations

**For Queries:**
1. **Exclude null columns**: 28 columns have 100% nulls - exclude from SELECT statements
2. **Handle forward-looking nulls**: pct_change_q*_forward columns have 3-11% nulls at dataset boundaries
3. **Time range validation**: Dataset spans 2012-2026; validate date filters fall within range
4. **Sector completeness**: Verify all 11 sectors have consistent temporal coverage
5. **Price consistency**: Validate that monthly_avg_high >= monthly_avg_close >= monthly_avg_low
6. **Exchange constant**: exchange='ARCX' for all rows, can be hardcoded in filters

**Recommended Query Patterns:**
- Time-series analysis using month_date with symbol grouping
- Sector performance comparisons using symbol with temporal aggregation
- Forward return analysis using pct_change_q*_forward metrics
- Seasonal analysis using quarter_num across multiple years
- Trend analysis comparing monthly vs quarterly averages

## Keywords

US sectors, sector ETFs, SPDR sectors, XLB materials, XLC communications, XLE energy, XLF financials, XLI industrials, XLK technology, XLP consumer staples, XLRE real estate, XLU utilities, XLV healthcare, ARCX exchange, NYSE Arca, monthly returns, quarterly returns, sector performance, forward returns, sector analysis, OHLCV data, time series, stock market sectors, ETF performance, sector rotation, percentage change, quarterly forecasts, historical prices, trading volume, sector averages, economic sectors

## Table and Column Documentation

**Table Comment**: Not provided in the analysis report.

**Column Comments**: No column-level comments were provided in the analysis report. The column names are self-descriptive, following common financial data conventions for OHLCV metrics, temporal dimensions, and forward-looking performance indicators.