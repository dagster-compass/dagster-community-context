---
columns:
- adj_close (FLOAT64)
- adj_high (FLOAT64)
- adj_low (FLOAT64)
- adj_open (FLOAT64)
- adj_volume (FLOAT64)
- asset_type (STRING)
- close (FLOAT64)
- date (DATE)
- dividend (FLOAT64)
- exchange (STRING)
- exchange_code (STRING)
- high (FLOAT64)
- low (FLOAT64)
- name (STRING)
- open (FLOAT64)
- price_currency (STRING)
- split_factor (FLOAT64)
- symbol (STRING)
- volume (FLOAT64)
schema_hash: 942ae01f6861b9b9f63e3b0c99a821c2db446de299de149a365410555a5ba07e

---
# Table Documentation: stg_major_indices

## Overview

This table contains historical trading data for major market indices and ETFs, with **17,691 rows** of time-series financial data. The dataset appears to track daily price movements, volumes, and dividend information across 5 different securities (DIA, IWM, QQQ, SPY, and VIX.INDX) over approximately 3,577 unique trading days.

### General Data Quality
- **High quality price data**: Core price fields (open, high, low, close) have 0% null values
- **Inconsistent metadata**: Descriptive fields (name, exchange_code, asset_type, price_currency) are 93.63% null
- **Adjusted values present significant nulls**: All adj_* fields show 26.52% null values
- **Volume data**: 6.94% null in base volume field

The data appears to be from two different source systems or time periods, with older records lacking metadata fields.

---

## Column Details

### Price Fields (Core Trading Data)

**open** (FLOAT64)
- Opening price for the trading period
- Range: $9.01 to $697.05
- No nulls, excellent data quality
- 13,355 unique values indicating granular price movements

**high** (FLOAT64)
- Highest price during the trading period
- Range: $9.31 to $697.84
- No nulls, complete coverage
- 13,729 unique values

**low** (FLOAT64)
- Lowest price during the trading period
- Range: $8.56 to $693.94
- No nulls, complete coverage
- 13,551 unique values

**close** (FLOAT64)
- Closing price for the trading period
- Range: $9.14 to $695.49
- No nulls, critical field for analysis
- 13,417 unique values

### Volume and Trading Activity

**volume** (FLOAT64)
- Trading volume for the period
- Range: 0 to 507.2 million
- 6.94% nulls (1,228 records)
- High variability suggests different securities with varying liquidity

**adj_volume** (FLOAT64)
- Split-adjusted trading volume
- Range: 611,600 to 507.2 million
- 26.52% nulls (4,693 records)
- Available for more recent data

### Adjusted Price Fields

**adj_open**, **adj_high**, **adj_low**, **adj_close** (FLOAT64)
- Split and dividend-adjusted prices
- All show 26.52% null values (4,693 records)
- Ranges similar to unadjusted prices
- Critical for long-term price comparisons and returns analysis

### Corporate Actions

**dividend** (FLOAT64)
- Dividend payments per share
- Range: $0.00 to $1.993
- 331 unique values, predominantly $0.00
- No nulls, indicating explicit tracking of dividend events

**split_factor** (FLOAT64)
- Stock split multiplier
- **Single value**: 1.0 across all records
- No stock splits recorded in this dataset
- No nulls

### Security Identifiers

**symbol** (STRING)
- Ticker symbol for the security
- 5 unique values: **DIA, IWM, QQQ, SPY, VIX.INDX**
- No nulls, primary identifier
- VIX.INDX represents volatility index, others are ETFs

**exchange** (STRING)
- Exchange where security trades
- 3 unique values: **ARCX** (NYSE Arca), **INDX** (Index), **XNAS** (NASDAQ)
- No nulls
- Maps to security types

### Security Metadata (Sparse)

**name** (STRING)
- Full name of the security
- 93.63% nulls
- 4 known values:
  - "ISHARES RUSSELL 2000 ETF"
  - "Invesco QQQ Trust Series 1"
  - "SPDR Dow Jones Industrial Average ETF"
  - "SPDR S&P 500 ETF Trust"

**exchange_code** (STRING)
- Detailed exchange identifier
- 93.63% nulls
- Values: "NASDAQ", "NYSE ARCA"

**price_currency** (STRING)
- Currency denomination
- 93.63% nulls
- Values: "USD", "usd" (inconsistent casing)

**asset_type** (STRING)
- Type of financial instrument
- 93.63% nulls
- Single known value: "ETF"

### Temporal

**date** (DATE)
- Trading date
- 3,577 unique dates
- No nulls, complete time coverage
- Spans multiple years based on sample data (2012-2025)

---

## Query Considerations

### Recommended for Filtering
- **date**: Time-range queries, trend analysis
- **symbol**: Security-specific analysis (5 distinct values)
- **exchange**: Group by market venue
- **dividend** > 0: Identify dividend payment dates

### Recommended for Grouping/Aggregation
- **symbol**: Compare performance across indices/ETFs
- **date** (by month/quarter/year): Time-series aggregations
- **exchange**: Market venue analysis

### Potential Join Keys
- **(symbol, date)**: Composite key for joining with other financial data
- **symbol**: Join with security master tables
- **date**: Join with economic indicators, market events

### Data Quality Considerations for Queries

1. **Use adjusted prices for historical analysis**: The adj_* fields account for splits/dividends but have 26.52% nulls. Consider filtering WHERE adj_close IS NOT NULL for accurate returns.

2. **Metadata fields unreliable**: The 93.63% null rate for name, exchange_code, asset_type means these should only be used for recent data or expect nulls in results.

3. **Volume considerations**: 6.94% null volume may affect liquidity analysis. VIX.INDX (volatility index) may not have traditional volume data.

4. **Split factor constant**: Since split_factor = 1.0 for all records, no splits occurred. Don't need to account for split adjustments beyond provided adj_* fields.

5. **Date continuity**: Check for gaps in date series by symbol as weekends/holidays create natural breaks.

6. **Price validation**: Ensure high >= low and close between high/low for data quality checks.

---

## Keywords

Financial data, stock market, ETF, indices, time series, trading data, OHLCV (Open-High-Low-Close-Volume), adjusted prices, dividends, stock splits, DIA, SPY, QQQ, IWM, VIX, volatility index, NASDAQ, NYSE ARCA, daily prices, market data, securities, ticker symbols, historical prices, trading volume, economic data, market indices, S&P 500, Dow Jones, Russell 2000, NASDAQ-100, volatility

---

## Table and Column Documentation

### Table Comment
*No table-level comment provided in the analysis report.*

### Column Comments
*No column-level comments were provided in the analysis report. All column descriptions above are derived from data analysis rather than explicit documentation.*