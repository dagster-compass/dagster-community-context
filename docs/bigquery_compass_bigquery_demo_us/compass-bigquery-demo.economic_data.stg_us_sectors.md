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
# Table Summary: stg_us_sectors

## Overview

This table contains **28,011 rows** of historical market data for US sector ETFs (Exchange-Traded Funds), tracking daily trading information including prices, volumes, dividends, and stock splits. The data spans **3,512 unique dates** and covers **11 different sector symbols** traded on the ARCX (NYSE ARCA) exchange.

### Data Quality Observations
- **High-quality price data**: Core trading metrics (open, high, low, close, volume) have 0% nulls
- **Metadata sparsity**: Descriptive fields (name, exchange_code, asset_type, price_currency) have 90-91% null values
- **Adjusted metrics**: About 6.93% of adjusted price fields (adj_high, adj_low, adj_open, adj_volume) contain nulls
- **Date range**: Data appears to span from at least 2012 to 2024 based on sample dates

### Notable Patterns
- **Volume distribution**: Extremely wide range (34 to 233M), suggesting different liquidity levels across sectors or time periods
- **Split activity**: Minimal split activity (only values of 1.0 and 2.0)
- **Dividend payments**: Most records show 0.0 dividends, with occasional payments ranging up to 1.79121
- **Price ranges**: Vary significantly by sector, from ~$20 to ~$305

---

## Column Details

### Price Metrics (FLOAT64)

**open, high, low, close**
- All have 0% nulls and represent daily OHLC prices
- Ranges: $22-$305 across all price fields
- High cardinality (10,000-14,000 unique values each)
- Standard stock market price data format

**adj_open, adj_high, adj_low, adj_close**
- Adjusted prices accounting for splits and dividends
- 6.93% null rate for adj_open, adj_high, adj_low
- 0% nulls for adj_close (most commonly used adjusted metric)
- Similar ranges to unadjusted prices

### Volume Metrics (FLOAT64)

**volume**
- 0% nulls, 27,891 unique values
- Range: 34 to 233,067,911 shares
- Extremely high cardinality indicates daily granularity

**adj_volume**
- 6.93% null rate
- Range: 351,425 to 233,067,911 shares
- Adjusted for corporate actions

### Corporate Actions (FLOAT64)

**split_factor**
- 0% nulls, only 2 unique values (1.0, 2.0)
- Predominantly 1.0 (no split)
- Binary indicator of stock splits

**dividend**
- 0% nulls, 356 unique values
- Range: 0.0 to 1.79121
- Most values are 0.0, with occasional dividend payments

### Identifiers & Metadata (STRING)

**symbol**
- 0% nulls, 11 unique values
- Sector ETF tickers: XLB, XLC, XLE, XLF, XLI, XLK, XLP, XLRE, XLU, XLV, XLY
- Primary identifier for sector classification
- **Key for grouping and filtering**

**date** (DATE)
- 0% nulls, 3,512 unique dates
- Sample dates from 2012 to 2024
- **Primary time dimension for analysis**

**exchange**
- 0% nulls, only 1 value: "ARCX"
- All data from NYSE ARCA exchange
- Not useful for filtering (constant value)

**name**
- 90.18% nulls, 16 unique values when present
- Full fund names (e.g., "Energy Select Sector SPDR Fund")
- Sparse but descriptive when available

**exchange_code**
- 91.19% nulls, only "NYSE ARCA" when present
- Highly redundant with exchange field

**asset_type**
- 90.18% nulls, only "ETF" when present
- Consistent but sparse metadata

**price_currency**
- 90.18% nulls, 3 values: MXN, USD, usd
- Inconsistent capitalization (USD vs usd)
- Predominantly USD when populated

---

## Query Considerations

### Optimal Filtering Columns
1. **symbol**: Primary sector identifier (11 ETFs) - excellent for sector-specific queries
2. **date**: Time-based filtering and range queries
3. **dividend**: Filter for dividend payment events (WHERE dividend > 0)
4. **split_factor**: Identify stock split events (WHERE split_factor != 1.0)

### Grouping & Aggregation
1. **symbol**: Group by sector for comparative analysis
2. **date**: Time-series aggregations (daily, monthly, yearly)
3. Combine symbol + date for sector performance over time
4. Volume-weighted calculations using volume or adj_volume

### Key Relationships & Join Keys
- **symbol + date**: Natural composite key for uniqueness
- Potential joins with other sector/market tables on symbol
- Date-based joins with economic indicators or benchmark indices

### Data Quality Considerations

**For Queries:**
1. **Use adj_close over close** for accurate historical comparisons (accounts for splits/dividends)
2. **Metadata fields**: Expect 90%+ nulls in name, exchange_code, asset_type, price_currency
3. **Adjusted metrics nulls**: 6.93% of adj_high, adj_low, adj_open, adj_volume are null - use COALESCE or filter as needed
4. **Volume outliers**: Extremely wide range suggests potential data quality issues or legitimate low-volume days
5. **Currency consistency**: Check price_currency when present due to MXN/USD/usd variations

**Best Practices:**
- Always include symbol in WHERE clause for sector-specific analysis
- Use date ranges to manage result sizes (3,512 days × 11 symbols)
- Prefer adj_close for price calculations
- Handle nulls in adjusted metrics appropriately
- Be aware metadata fields are mostly unpopulated

---

## Keywords

sector ETFs, SPDR funds, stock market data, OHLC prices, trading volume, adjusted prices, dividends, stock splits, NYSE ARCA, ARCX, XLB, XLC, XLE, XLF, XLI, XLK, XLP, XLRE, XLU, XLV, XLY, time series, daily trading data, financial markets, equity sectors, economic data, market sectors, consumer discretionary, consumer staples, energy sector, financials, industrials, technology, healthcare, utilities, real estate, materials, communication services

---

## Table and Column Documentation

**Table Comment:** Not provided

**Column Comments:** Not provided