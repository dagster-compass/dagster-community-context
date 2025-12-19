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
# Documentation Summary: stg_major_indices Table

## Overall Dataset Characteristics

**Total Rows:** 17,543

**General Description:** This table contains historical daily trading data for major market indices and ETFs, including the S&P 500 (SPY), Russell 2000 (IWM), NASDAQ-100 (QQQ), Dow Jones (DIA), and VIX volatility index. The data represents approximately 3,545 unique trading dates with multiple securities tracked across each date.

**Data Quality Observations:**
- Core price data (open, high, low, close) has 100% completeness with no nulls
- Significant null patterns exist for adjusted price columns (~27% nulls) and metadata fields (~94% nulls)
- Volume data has moderate null percentage (6.88%)
- All records have a consistent split_factor of 1.0, indicating no stock splits in this dataset
- Date range spans multiple years of market data (2013-2024 visible in samples)

**Notable Patterns:**
- The dataset appears to transition between two data formats: older records lack metadata (name, exchange_code, asset_type) while newer records have adjusted price columns
- Price ranges vary significantly by security (9.01 to 689.7), reflecting different index/ETF price levels
- Dividend values are predominantly 0.0 with occasional dividend payments up to 1.966

## Column Details

### Price Columns

**open (FLOAT64)**
- Opening price for the trading day
- 100% complete, no nulls
- Range: 9.01 to 688.72
- 13,236 unique values indicating high granularity
- Used for: Daily price analysis, gap detection, trend analysis

**high (FLOAT64)**
- Highest price reached during the trading day
- 100% complete, no nulls
- Range: 9.31 to 689.7
- 13,617 unique values (highest among price columns)
- Used for: Price range analysis, volatility calculations, resistance levels

**low (FLOAT64)**
- Lowest price reached during the trading day
- 100% complete, no nulls
- Range: 8.56 to 684.83
- 13,437 unique values
- Used for: Price range analysis, support levels, volatility calculations

**close (FLOAT64)**
- Closing price for the trading day
- 100% complete, no nulls
- Range: 9.14 to 689.17
- 13,298 unique values
- Used for: Time series analysis, returns calculation, end-of-day valuations

### Adjusted Price Columns

**adj_open (FLOAT64)**
- Split and dividend-adjusted opening price
- 26.63% null values (4,671 records)
- Range: 51.99 to 688.72
- Nulls indicate older records or specific data collection periods

**adj_high (FLOAT64)**
- Split and dividend-adjusted high price
- 26.63% null values
- Range: 52.35 to 689.7
- 12,575 unique values
- Used for: Long-term historical comparisons accounting for corporate actions

**adj_low (FLOAT64)**
- Split and dividend-adjusted low price
- 26.63% null values
- Range: 51.77 to 684.83
- 12,582 unique values

**adj_close (FLOAT64)**
- Split and dividend-adjusted closing price
- 100% complete, no nulls
- Range: 9.14 to 689.17
- 15,103 unique values (highest unique count, indicating decimal precision)
- Most important for historical returns analysis

### Volume Columns

**volume (FLOAT64)**
- Raw trading volume
- 6.88% null values (1,207 records)
- Range: 0.0 to 507,244,281
- Includes zero-volume days
- Used for: Liquidity analysis, trading activity patterns

**adj_volume (FLOAT64)**
- Split-adjusted volume
- 26.63% null values (same pattern as adjusted prices)
- Range: 611,600 to 507,244,300
- 12,840 unique values

### Corporate Action Columns

**dividend (FLOAT64)**
- Dividend amount paid
- 100% complete
- 329 unique values
- Range: 0.0 to 1.966
- Predominantly 0.0 (most days have no dividend)
- Common non-zero values include: 0.07958, 0.08588, 0.11195, 0.11283, etc.
- Used for: Total return calculations, income analysis

**split_factor (FLOAT64)**
- Stock split multiplier
- 100% complete
- Only 1 unique value: 1.0
- Indicates no stock splits occurred in this dataset period

### Identifier Columns

**symbol (STRING)**
- Trading ticker symbol
- 100% complete, no nulls
- 5 unique values: DIA, IWM, QQQ, SPY, VIX.INDX
- Primary key component (along with date)
- Used for: Filtering specific indices, grouping by security

**exchange (STRING)**
- Exchange abbreviation code
- 100% complete, no nulls
- 3 unique values: ARCX (NYSE Arca), INDX (Index), XNAS (NASDAQ)
- Used for: Exchange-based analysis, data validation

**date (DATE)**
- Trading date
- 100% complete, no nulls
- 3,545 unique dates
- Primary key component (along with symbol)
- Used for: Time series queries, date range filtering, trend analysis

### Metadata Columns (Sparse)

**name (STRING)**
- Full name of the security
- 94.30% null values (16,542 nulls)
- 4 unique non-null values:
  - ISHARES RUSSELL 2000 ETF
  - Invesco QQQ Trust Series 1
  - SPDR Dow Jones Industrial Average ETF
  - SPDR S&P 500 ETF Trust
- Metadata appears only for recent records

**exchange_code (STRING)**
- Detailed exchange name
- 94.30% null values
- 2 unique values: NASDAQ, NYSE ARCA
- Limited utility due to high null percentage

**asset_type (STRING)**
- Type of security
- 94.30% null values
- Only 1 unique value: ETF
- All non-null records are ETFs

**price_currency (STRING)**
- Currency denomination
- 94.30% null values
- 2 unique values: USD, usd (inconsistent casing)
- All are USD-denominated when present

## Potential Query Considerations

### Good Filtering Columns:
- **symbol**: Most common filter (5 distinct securities)
- **date**: Essential for time-based queries (range filters, specific dates)
- **exchange**: Useful for exchange-specific analysis
- **dividend > 0**: To find dividend payment dates

### Good Grouping/Aggregation Columns:
- **symbol**: For per-security analysis
- **DATE_TRUNC(date, MONTH/YEAR)**: For monthly/yearly aggregations
- **exchange**: For exchange-level statistics
- **EXTRACT(YEAR FROM date)**: For year-over-year comparisons

### Potential Join Keys:
- **(symbol, date)**: Composite primary key for joining with other market data
- **symbol**: For joining with security master tables
- **date**: For joining with economic indicators or calendar tables

### Data Quality Considerations:

1. **Null Handling Strategy**: 
   - Use `close` instead of `adj_close` for recent data completeness
   - Prefer `volume` over `adj_volume` for broader coverage
   - Avoid metadata columns (name, exchange_code, etc.) unless recent data only

2. **Date Range Awareness**:
   - Adjusted price columns became available at a specific point in time
   - Consider using COALESCE(adj_close, close) for queries spanning both periods

3. **Volume Anomalies**:
   - Zero-volume records exist (possibly for indices vs ETFs)
   - VIX.INDX may have different volume characteristics as an index

4. **Price Scale Differences**:
   - VIX ranges much lower (9-30 typical) vs ETFs (100-600+)
   - Apply security-specific filters when doing cross-security analysis

5. **Consistency Issues**:
   - price_currency has inconsistent casing (USD vs usd)
   - Consider uppercasing for comparisons

## Keywords

Market data, stock prices, ETF data, S&P 500, SPY, Russell 2000, IWM, NASDAQ-100, QQQ, Dow Jones, DIA, VIX, volatility index, daily prices, OHLC data, open high low close, trading volume, adjusted prices, dividends, split factor, time series data, financial data, market indices, NYSE Arca, NASDAQ exchange, historical prices, stock market analysis, technical analysis, price history, trading data, securities data

## Table and Column Documentation

**Table Comment**: Not provided in the analysis report.

**Column Comments**: No column-level comments were provided in the analysis report. The column names follow standard financial data conventions where OHLC represents Open-High-Low-Close pricing, and "adj_" prefix indicates corporate action adjustments.