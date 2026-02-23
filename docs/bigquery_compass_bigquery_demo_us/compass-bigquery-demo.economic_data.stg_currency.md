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
# Comprehensive Data Summary: stg_currency Table

## Overall Dataset Characteristics

### General Information
- **Total Rows**: 23,424 records
- **Table Purpose**: Currency and currency-related ETF price data staging table
- **Data Quality**: Generally good with complete core price data, but significant missing values in adjusted price columns (~13%) and metadata fields (~90%)

### Notable Patterns
- Primary data consists of daily OHLC (Open, High, Low, Close) price information with volume
- Split between regular price data (100% complete) and adjusted price data (~87% complete)
- Metadata fields (name, asset_type, exchange_code, price_currency) are sparsely populated (only ~10% of rows)
- Data covers 8 distinct currency symbols tracked across 3,543 unique dates
- Most records represent ETF trading data from major exchanges (ARCX, OTCM, INDX)

## Column Details

### Price Columns (Core Trading Data)

**open** (FLOAT64)
- Fully populated (0% nulls)
- 10,616 unique values
- Range: $4.71 to $610.00
- Opening price for the trading period
- Good for filtering on price ranges and trend analysis

**high** (FLOAT64)
- Fully populated (0% nulls)
- 12,597 unique values  
- Range: $4.84 to $610.00
- Daily high price
- Useful for volatility analysis and price ceiling queries

**low** (FLOAT64)
- Fully populated (0% nulls)
- 12,458 unique values
- Range: $4.62 to $369.95
- Daily low price
- Useful for volatility analysis and price floor queries

**close** (FLOAT64)
- Fully populated (0% nulls)
- 11,642 unique values
- Range: $4.72 to $580.00
- Closing price for the trading period
- Primary field for price analysis and historical trends

### Adjusted Price Columns

**adj_open** (FLOAT64)
- 13.35% null values
- 13,214 unique values
- Range: $4.71 to $168.89
- Adjusted opening price (accounts for splits/dividends)
- Use with caution due to missing data

**adj_high** (FLOAT64)
- 13.35% null values
- 14,636 unique values
- Range: $4.84 to $169.06
- Adjusted high price
- Use with caution due to missing data

**adj_low** (FLOAT64)
- 13.35% null values
- 14,521 unique values
- Range: $4.62 to $168.76
- Adjusted low price
- Use with caution due to missing data

**adj_close** (FLOAT64)
- Fully populated (0% nulls)
- 14,978 unique values (highest among all price fields)
- Range: $4.72 to $580.00
- Adjusted closing price - fully populated unlike other adjusted fields
- Best adjusted price field for analysis

### Volume Columns

**volume** (FLOAT64)
- Fully populated (0% nulls)
- 19,104 unique values (high variability)
- Range: 0 to 168,213,523
- Raw trading volume
- Good for liquidity analysis and activity filtering

**adj_volume** (FLOAT64)
- 13.35% null values
- 18,825 unique values
- Range: 0 to 168,213,523
- Adjusted trading volume
- Use volume (non-adjusted) for complete data

### Corporate Actions

**dividend** (FLOAT64)
- Fully populated (0% nulls)
- 171 unique values
- Range: $0.00 to $0.917
- Predominantly $0.00 (most common value)
- Small incremental values when present (0.0003, 0.00049, etc.)
- Important for total return calculations

**split_factor** (FLOAT64)
- Fully populated (0% nulls)
- Only 2 unique values: 1.0 and 9.0
- Overwhelmingly 1.0 (no split)
- Rare split events with factor of 9.0
- Critical for historical price adjustments

### Identifiers and Metadata

**symbol** (STRING)
- Fully populated (0% nulls)
- 8 unique values: CEW, ETHE, FXA, FXB, FXC, FXE, FXY, IBIT.INDX
- Primary identifier for currency/ETF instruments
- Essential for filtering and grouping

**date** (DATE)
- Fully populated (0% nulls)
- 3,543 unique dates
- Spans from historical dates through 2025-09-24 (includes future dates - possible data quality issue)
- Primary time dimension for queries
- Essential for time-series analysis

**exchange** (STRING)
- Fully populated (0% nulls)
- 3 unique values: ARCX (NYSE Arca), INDX (Index), OTCM (OTC Markets)
- Indicates trading venue
- Good for filtering by market type

**name** (STRING)
- 90.41% null values
- Only 9 unique values when present
- Includes: Grayscale Investments LLC, Invesco CurrencyShares trusts, WisdomTree funds, iShares Bitcoin Trust
- Limited utility due to sparseness

**asset_type** (STRING)
- 90.41% null values
- Only 2 unique values: ETF, Stock
- Mostly null, limited analytical value

**price_currency** (STRING)
- 91.36% null values
- Only 2 unique values: USD, usd (case inconsistency)
- When populated, indicates USD denomination

**exchange_code** (STRING)
- 91.36% null values
- 4 unique values: NASDAQ, NYSE ARCA, OTCMKTS, OTCQX
- More detailed exchange information when available
- Overlaps with exchange field but less populated

## Potential Query Considerations

### Strong Filtering Columns
- **symbol**: Complete data, only 8 values - excellent for WHERE clauses
- **date**: Complete data, time-series queries - essential for trend analysis
- **exchange**: Complete data, 3 values - good for market segmentation
- **close/adj_close**: Complete data - price range filtering

### Good Grouping/Aggregation Columns
- **symbol**: Primary grouping dimension (8 instruments)
- **date**: Time-based aggregations (daily, monthly, yearly)
- **exchange**: Market-type analysis
- Combinations: symbol + date for time-series by instrument

### Potential Join Keys
- **symbol**: Primary key for joining with other currency/instrument reference tables
- **date**: Time dimension joins with other date-based datasets
- **symbol + date**: Composite key for unique daily records

### Data Quality Considerations

**Critical Issues:**
1. **Future Dates**: Sample data shows date "2025-09-24" - requires validation
2. **Inconsistent Null Patterns**: Adjusted price columns have ~13% nulls except adj_close (0% nulls)
3. **Metadata Sparseness**: 90%+ nulls in name, asset_type, price_currency, exchange_code
4. **Case Sensitivity**: price_currency has both "USD" and "usd"

**Query Recommendations:**
- Use `close` and `adj_close` for most reliable price analysis (0% nulls)
- Use `volume` over `adj_volume` for complete volume data
- Filter out or validate dates beyond current date
- Use `symbol` and `exchange` for reliable categorization
- Avoid relying on name, asset_type, exchange_code, price_currency unless handling nulls
- When using adjusted OHLC columns, include null handling (13.35% missing)
- Consider split_factor when reconstructing historical prices

**Analytical Use Cases:**
- Daily price trend analysis by currency symbol
- Volume-weighted calculations for liquidity analysis
- Volatility calculations using high-low ranges
- Total return calculations incorporating dividends
- Cross-exchange price comparisons for same symbols
- Time-series forecasting for currency ETF prices

## Keywords

Currency, ETF, Exchange Traded Fund, OHLC, Open High Low Close, Price Data, Trading Volume, Stock Market, Foreign Exchange, FX, Cryptocurrency, Bitcoin, Grayscale, Invesco, CurrencyShares, WisdomTree, iShares, NYSE Arca, NASDAQ, OTC Markets, Dividends, Stock Splits, Adjusted Prices, Market Data, Financial Data, Time Series, Daily Prices, ARCX, INDX, OTCM, FXA, FXB, FXC, FXE, FXY, CEW, ETHE, IBIT

## Table and Column Documentation

**Table Comment**: Not provided

**Column Comments**: Not provided for any columns