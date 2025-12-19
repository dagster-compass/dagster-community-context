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
# Table Summary: compass-bigquery-demo.economic_data.stg_currency

## Overall Dataset Characteristics

This table contains **23,178 rows** of currency-related financial market data, primarily consisting of Exchange-Traded Funds (ETFs) tracking various currencies. The dataset spans from approximately 2012 to 2025 with **3,511 unique dates**. 

**Key Observations:**
- The data represents 8 different currency symbols (FXA, FXB, FXC, FXE, FXY, FXC, CEW, ETHE, IBIT.INDX)
- Most rows (91-92%) lack detailed metadata (name, exchange_code, asset_type, price_currency)
- The dataset contains both raw and adjusted OHLC (Open, High, Low, Close) data
- Volume data is complete for raw values but has 13.49% nulls for adjusted values
- Data quality is generally high for core price metrics (0% nulls)

## Column Details

### Price Metrics (Core Trading Data)

**open** (FLOAT64)
- Complete data (0% nulls)
- Range: 4.71 to 610.0
- 10,540 unique values
- Represents opening price for each trading period

**high** (FLOAT64)
- Complete data (0% nulls)
- Range: 4.84 to 610.0
- 12,520 unique values
- Represents highest price during trading period

**low** (FLOAT64)
- Complete data (0% nulls)
- Range: 4.62 to 369.95
- 12,377 unique values
- Represents lowest price during trading period

**close** (FLOAT64)
- Complete data (0% nulls)
- Range: 4.72 to 580.0
- 11,565 unique values
- Represents closing price for trading period

### Adjusted Price Metrics

**adj_open** (FLOAT64)
- 13.49% nulls
- Range: 4.71 to 168.89
- 13,108 unique values
- Adjusted opening price accounting for corporate actions

**adj_high** (FLOAT64)
- 13.49% nulls
- Range: 4.84 to 169.06
- 14,500 unique values
- Adjusted high price

**adj_low** (FLOAT64)
- 13.49% nulls
- Range: 4.62 to 168.76
- 14,379 unique values
- Adjusted low price

**adj_close** (FLOAT64)
- Complete data (0% nulls)
- Range: 4.72 to 580.0
- 14,893 unique values
- Adjusted closing price (most complete adjusted metric)

### Volume Metrics

**volume** (FLOAT64)
- Complete data (0% nulls)
- Range: 0.0 to 168,213,523.0
- 18,998 unique values
- Raw trading volume

**adj_volume** (FLOAT64)
- 13.49% nulls
- Range: 0.0 to 168,213,523.0
- 18,612 unique values
- Adjusted trading volume

### Corporate Actions

**dividend** (FLOAT64)
- Complete data (0% nulls)
- 170 unique values
- Range: 0.0 to 0.917
- Predominantly 0.0, with occasional small dividend values
- Tracks dividend distributions

**split_factor** (FLOAT64)
- Complete data (0% nulls)
- Only 2 unique values: 1.0 and 9.0
- Predominantly 1.0 (no split)
- Tracks stock/ETF split events

### Identifiers and Metadata

**symbol** (STRING)
- Complete data (0% nulls)
- 8 unique values: CEW, ETHE, FXA, FXB, FXC, FXE, FXY, IBIT.INDX
- Primary identifier for currency/asset
- Essential for filtering and grouping

**exchange** (STRING)
- Complete data (0% nulls)
- 3 unique values: ARCX (NYSE Arca), INDX, OTCM (OTC Markets)
- Indicates trading venue

**date** (DATE)
- Complete data (0% nulls)
- 3,511 unique dates
- Time dimension for analysis

**name** (STRING)
- 91.37% nulls
- 9 unique values when present
- Includes names like "Invesco CurrencyShares Euro Trust", "iShares Bitcoin Trust", "Grayscale Investments LLC"

**exchange_code** (STRING)
- 92.20% nulls
- 4 unique values: NASDAQ, NYSE ARCA, OTCMKTS, OTCQX

**price_currency** (STRING)
- 92.20% nulls
- 2 unique values: USD, usd (case inconsistency)

**asset_type** (STRING)
- 91.37% nulls
- 2 unique values: ETF, Stock

## Query Considerations

### Recommended Filtering Columns
- **symbol**: Primary filter for specific currency ETFs (complete data)
- **date**: Time-based filtering (complete data)
- **exchange**: Filter by trading venue (complete data)
- **asset_type**: Filter by type when metadata exists (~8% coverage)

### Recommended Grouping/Aggregation Columns
- **symbol**: Group by currency instrument
- **date**: Time-series aggregations (daily, monthly, yearly)
- **exchange**: Compare across trading venues
- Use DATE_TRUNC on date for period-based groupings

### Potential Join Keys
- **symbol**: Join with other currency/ETF reference tables
- **date**: Join with other time-series data
- Composite key: (symbol, date) for unique daily records

### Data Quality Considerations
1. **Adjusted metrics missing**: ~13.49% of adj_open, adj_high, adj_low, adj_volume are null
   - Use adj_close which is complete, or fallback to raw values
2. **Metadata sparsity**: 91-92% missing for name, exchange_code, asset_type, price_currency
   - Rely on symbol/exchange for identification
   - May need to join with reference table for complete metadata
3. **Case inconsistency**: price_currency has "USD" and "usd"
   - Use UPPER() or LOWER() for consistency
4. **Volume zeros**: Some records have 0.0 volume (low/no trading activity)
5. **Split factor**: Mostly 1.0, check for 9.0 values when analyzing historical trends

### Analysis Recommendations
- For price analysis, prefer adjusted values where available, fallback to raw
- Use symbol + date as composite unique identifier
- Be aware of ~13% data completeness issues in adjusted metrics
- Filter out zero-volume records for liquidity analysis
- Time-series queries work well due to complete date coverage

## Keywords

currency, ETF, exchange-traded fund, forex, foreign exchange, OHLC, open high low close, trading data, financial markets, adjusted prices, volume, dividends, stock splits, time series, daily prices, Invesco CurrencyShares, iShares, Bitcoin, Grayscale, Australian Dollar, British Pound, Canadian Dollar, Euro, Japanese Yen, emerging currency, FXA, FXB, FXC, FXE, FXY, ARCX, NYSE Arca, OTC Markets, cryptocurrency, ETHE, IBIT

## Table and Column Documentation

**Table Comment**: Not provided

**Column Comments**: No column-level comments or descriptions were provided in the source data.