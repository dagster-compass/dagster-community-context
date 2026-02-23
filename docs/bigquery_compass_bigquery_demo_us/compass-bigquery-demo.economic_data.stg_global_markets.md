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
# Table Documentation Summary: stg_global_markets

## Overall Dataset Characteristics

**Total Rows:** 46,044

**General Description:** This table contains daily stock market data for global market ETFs, primarily tracking various country-specific and regional market indices. The data includes standard OHLCV (Open, High, Low, Close, Volume) metrics along with adjusted values that account for corporate actions like splits and dividends.

**Data Quality Observations:**
- Core trading metrics (open, high, low, close, volume) have 0% null values
- Adjusted metrics (adj_open, adj_high, adj_low, adj_volume) have 10.94% null values
- Metadata columns (name, exchange_code, asset_type, price_currency) have 92.06% null values
- Date range spans from approximately 2013 to 2025, covering over a decade of market data

**Notable Patterns:**
- Most records represent ETF trading data across two exchanges (ARCX and XNAS)
- 13 different ETF symbols are tracked, representing various global markets
- Split factors are rare (mostly 1.0, with only 4 unique values)
- Dividends are present but sparse (333 unique values with most being 0.0)

## Column Details

### Trading Price Metrics

**open (FLOAT64)**
- Opening price for the trading day
- Range: $8.74 to $147.39
- No null values - complete data
- 8,522 unique values indicating diverse price points

**high (FLOAT64)**
- Highest price reached during trading day
- Range: $8.75 to $147.43
- No null values - complete data
- 12,756 unique values

**low (FLOAT64)**
- Lowest price reached during trading day
- Range: $8.64 to $146.44
- No null values - complete data
- 12,801 unique values

**close (FLOAT64)**
- Closing price for the trading day
- Range: $8.65 to $147.06
- No null values - complete data
- 8,526 unique values

### Adjusted Price Metrics

**adj_open (FLOAT64)**
- Dividend and split-adjusted opening price
- Range: $12.07 to $147.39
- 10.94% null values
- 29,792 unique values - more granular due to adjustment calculations

**adj_high (FLOAT64)**
- Adjusted highest price
- Range: $12.54 to $147.43
- 10.94% null values
- 32,483 unique values

**adj_low (FLOAT64)**
- Adjusted lowest price
- Range: $12.05 to $146.44
- 10.94% null values
- 32,719 unique values

**adj_close (FLOAT64)**
- Adjusted closing price (most commonly used for analysis)
- Range: $12.34 to $147.06
- No null values - complete data
- 30,480 unique values

### Volume Metrics

**volume (FLOAT64)**
- Raw trading volume
- Range: 15 to 322,620,100 shares
- No null values - complete data
- 45,363 unique values indicating high variability
- Examples: 538,382 / 32,694,247 / 5,036,600

**adj_volume (FLOAT64)**
- Split-adjusted trading volume
- Range: 11,400 to 322,806,886 shares
- 10.94% null values
- 40,891 unique values

### Corporate Actions

**dividend (FLOAT64)**
- Dividend amount paid
- Range: 0.0 to $4.705
- No null values but mostly zeros
- 333 unique values
- Most common value: 0.0 (indicating no dividend)

**split_factor (FLOAT64)**
- Stock split multiplier
- Only 4 unique values: 0.25, 0.5, 1.0, 60.0
- No null values
- Predominantly 1.0 (no split)

### Asset Identification

**symbol (STRING)**
- ETF ticker symbol
- 13 unique symbols: ACWI, EEM, EPI, EWA, EWG, EWJ, EWQ, EWU, EWW, EWY, EZA, EWZ, FXI
- No null values - complete data
- Primary key component for filtering

**exchange (STRING)**
- Exchange where traded
- 2 values: ARCX (NYSE Arca), XNAS (NASDAQ)
- No null values - complete data

**date (DATE)**
- Trading date
- 3,544 unique dates
- No null values - complete data
- Spans multiple years of trading data

### Metadata (Sparse Coverage)

**name (STRING)**
- Full ETF name (e.g., "ISHARES MSCI JAPAN ETF")
- 13 unique values
- 92.06% null values - only populated for ~8% of records

**exchange_code (STRING)**
- Alternative exchange identifier
- 2 unique values: NASDAQ, NYSE ARCA
- 92.06% null values

**asset_type (STRING)**
- Type of financial instrument
- Only 1 unique value: "ETF"
- 92.06% null values

**price_currency (STRING)**
- Currency denomination
- 2 unique values: USD, usd
- 92.06% null values

## Query Considerations

### Excellent for Filtering:
- **symbol**: Primary identifier for specific ETF selection
- **date**: Time-based filtering and range queries
- **exchange**: Filter by trading venue
- **dividend**: Filter dividend-paying periods (WHERE dividend > 0)

### Excellent for Grouping/Aggregation:
- **symbol**: Calculate metrics per ETF
- **date** (or date functions): Time-series analysis, daily/monthly/yearly aggregations
- **exchange**: Compare performance across exchanges
- **split_factor**: Identify corporate action periods

### Potential Join Keys:
- **(symbol, date)**: Composite primary key for joins with other market data
- **symbol**: Join with ETF metadata tables
- **exchange**: Join with exchange information tables

### Data Quality Considerations:

1. **Adjusted vs Raw Values**: Query choice depends on use case:
   - Use adjusted values for historical price comparisons
   - Use raw values for actual trading day analysis
   - Note 10.94% nulls in some adjusted columns

2. **Metadata Sparsity**: 92% null rate in descriptive fields means:
   - Cannot rely on name, exchange_code, asset_type for filtering
   - Use symbol + external lookup table for enrichment

3. **Volume Interpretation**: 
   - High variability suggests different liquidity profiles
   - Consider filtering outliers for meaningful averages

4. **Date Coverage**: 
   - 3,544 unique dates across 13 symbols suggests ~273 trading days per symbol
   - Check for gaps in time series if continuity is important

5. **Price Ranges**: 
   - Wide range ($8-$147) suggests different ETF types
   - Consider normalization for cross-symbol comparisons

## Keywords

ETF, exchange-traded fund, stock market, OHLCV, open high low close volume, adjusted prices, dividends, stock splits, NYSE Arca, NASDAQ, iShares, MSCI, international markets, emerging markets, country ETFs, daily trading data, financial time series, market data, equity data, price history, trading volume, corporate actions, ARCX, XNAS, ACWI, EEM, EWA, EWG, EWJ, EWU, Brazil, Japan, Germany, France, Australia, China, Mexico, Korea, global markets, split factor, dividend yield

## Table and Column Documentation

**Table Comment:** Not provided

**Column Comments:** None provided for any columns