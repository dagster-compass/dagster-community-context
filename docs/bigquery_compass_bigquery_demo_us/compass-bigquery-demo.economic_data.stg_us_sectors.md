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
# Table Summary: compass-bigquery-demo.economic_data.stg_us_sectors

## Overall Dataset Characteristics

This table contains **28,353 rows** of historical stock market data for US sector-specific ETFs (Exchange-Traded Funds). The dataset tracks daily trading information including prices, volumes, and adjustments across 11 different sector symbols over approximately 3,544 unique trading dates.

**Data Quality Observations:**
- Core trading metrics (open, high, low, close, volume) have 0% null values
- Adjusted price columns (adj_high, adj_low, adj_open, adj_volume) have ~6.85% null values
- Metadata columns (name, price_currency, asset_type, exchange_code) have very high null percentages (89-90%)
- The dataset shows clean financial data with consistent formatting
- Exchange is consistently "ARCX" (NYSE Arca)

**Notable Patterns:**
- Data spans multiple years of trading history (at least 2013-2025 based on sample dates)
- Split factor is almost exclusively 1.0 (only 2 unique values: 1.0 and 2.0)
- Most dividend values are 0.0, with occasional dividend payments up to 1.79121
- Volume ranges dramatically from 34 to over 233 million, indicating varying liquidity across time periods

## Column Details

### Trading Price Columns

**open (FLOAT64)**
- Opening price of the trading day
- No null values (0.00%)
- Range: $22.67 to $304.70
- 10,923 unique values
- Good for: Price analysis, calculating daily returns

**high (FLOAT64)**
- Highest price during the trading day
- No null values (0.00%)
- Range: $22.98 to $305.99
- 14,088 unique values
- Good for: Volatility analysis, resistance levels

**low (FLOAT64)**
- Lowest price during the trading day
- No null values (0.00%)
- Range: $22.50 to $301.87
- 14,007 unique values
- Good for: Volatility analysis, support levels

**close (FLOAT64)**
- Closing price of the trading day
- No null values (0.00%)
- Range: $22.58 to $304.13
- 11,048 unique values
- Good for: End-of-day analysis, primary price metric

### Adjusted Price Columns

**adj_open (FLOAT64)**
- Split and dividend-adjusted opening price
- 6.85% null values
- Range: $20.87 to $304.70
- 22,403 unique values
- Good for: Historical comparisons accounting for corporate actions

**adj_high (FLOAT64)**
- Split and dividend-adjusted high price
- 6.85% null values
- Range: $22.02 to $305.99
- 23,538 unique values

**adj_low (FLOAT64)**
- Split and dividend-adjusted low price
- 6.85% null values
- Range: $19.62 to $301.87
- 23,626 unique values

**adj_close (FLOAT64)**
- Split and dividend-adjusted closing price
- No null values (0.00%)
- Range: $20.61 to $304.13
- 23,137 unique values
- Primary metric for long-term analysis

### Volume Columns

**volume (FLOAT64)**
- Raw trading volume
- No null values (0.00%)
- Range: 34 to 233,067,911 shares
- 28,227 unique values (highly unique)
- Good for: Liquidity analysis, trading activity patterns

**adj_volume (FLOAT64)**
- Split-adjusted trading volume
- 6.85% null values
- Range: 351,425 to 233,067,911 shares
- 26,324 unique values
- Good for: Historical volume comparisons

### Corporate Action Columns

**split_factor (FLOAT64)**
- Stock split multiplier
- No null values (0.00%)
- Only 2 unique values: 1.0 (most common) and 2.0
- Indicates when stock splits occurred
- Good for: Identifying split events

**dividend (FLOAT64)**
- Dividend payment amount
- No null values (0.00%)
- 356 unique values
- Range: $0.00 to $1.79121
- Predominantly 0.0 with occasional dividend payments
- Good for: Dividend analysis, ex-dividend date identification

### Security Identification Columns

**symbol (STRING)**
- Ticker symbol for the sector ETF
- No null values (0.00%)
- 11 unique values: XLB, XLC, XLE, XLF, XLI, XLK, XLP, XLRE, XLU, XLV, XLY
- **Primary key component** (along with date)
- Good for: Filtering by sector, grouping operations

**exchange (STRING)**
- Exchange code
- No null values (0.00%)
- Single value: "ARCX" (NYSE Arca)
- Consistent across all records
- Limited filtering utility due to uniformity

**date (DATE)**
- Trading date
- No null values (0.00%)
- 3,544 unique dates
- **Primary key component** (along with symbol)
- Good for: Time-series analysis, date range filtering

### Metadata Columns (High Null Percentage)

**name (STRING)**
- Full name of the ETF
- 89.09% null values
- 16 unique values when present
- Examples: "Consumer Staples Select Sector SPDR Fund", "Energy Select Sector SPDR Fund"
- Limited utility due to high null percentage

**price_currency (STRING)**
- Currency denomination
- 89.09% null values
- 3 unique values: MXN, USD, usd (case inconsistency)
- Primarily USD when populated

**asset_type (STRING)**
- Type of security
- 89.09% null values
- Single value when present: "ETF"
- Redundant information

**exchange_code (STRING)**
- Full exchange name
- 90.41% null values
- Single value when present: "NYSE ARCA"
- Mostly redundant with exchange column

## Table and Column Documentation

No table comment or column comments are present in this dataset.

## Potential Query Considerations

### Good Filtering Columns
- **symbol**: Filter by specific sector ETFs (11 sectors available)
- **date**: Filter by date ranges, specific dates, or date patterns (year, month, quarter)
- **volume**: Filter for high/low liquidity periods
- **dividend**: Filter for dividend-paying periods (dividend > 0)
- **split_factor**: Identify split events (split_factor != 1.0)

### Good Grouping/Aggregation Columns
- **symbol**: Group by sector for comparative analysis
- **date** (with date functions): Group by year, month, quarter, week
- **EXTRACT(YEAR FROM date)**: Annual aggregations
- **EXTRACT(MONTH FROM date)**: Monthly patterns

### Potential Join Keys
- **(symbol, date)**: Composite primary key for joining with other market data
- **symbol**: Join with sector metadata tables
- **date**: Join with economic indicators, market indices

### Data Quality Considerations

1. **Null Handling**: 
   - Adjusted price columns have ~6.85% nulls - likely early data before adjustments were calculated
   - Metadata columns have 89-90% nulls - avoid using in critical queries
   - Use `adj_close` instead of adjusted price columns with nulls when consistency is needed

2. **Price Calculations**:
   - Use adjusted prices (adj_*) for long-term analysis to account for splits and dividends
   - Use raw prices (open, high, low, close) for intraday analysis
   - Calculate daily returns: `(close - open) / open`

3. **Volume Analysis**:
   - Extreme volume range (34 to 233M) suggests early/late trading days or special events
   - Consider filtering outliers for typical volume analysis
   - Use adj_volume for historical consistency

4. **Time Series Considerations**:
   - 3,544 unique dates over 28,353 rows = average ~8 rows per date (aligns with 11 symbols)
   - May have missing dates (weekends, holidays, early/late data periods)
   - Use `DATE_TRUNC` or `GENERATE_DATE_ARRAY` for complete time series

5. **Sector Coverage**:
   - 11 ETF symbols represent different market sectors
   - Data completeness may vary by symbol and date
   - Check for balanced data when comparing sectors

## Keywords

ETF, sector, stock market, SPDR, trading data, NYSE Arca, time series, financial data, daily prices, volume, dividends, stock splits, adjusted prices, XLB, XLC, XLE, XLF, XLI, XLK, XLP, XLRE, XLU, XLV, XLY, materials, communication services, energy, financials, industrials, technology, consumer staples, real estate, utilities, healthcare, consumer discretionary, OHLC, open high low close, market data, securities, historical prices