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
# Comprehensive Data Summary: stg_global_markets

## Overall Dataset Characteristics

**Total Records:** 45,628 rows

**General Description:** This table contains historical market data for global ETFs (Exchange-Traded Funds), tracking daily price movements, trading volumes, and corporate actions (dividends and stock splits). The dataset appears to be a staging table for financial market data analysis.

**Data Quality Observations:**
- Core price and volume data is complete (0% nulls)
- Significant metadata sparsity: 92.88% null values in descriptive fields (name, exchange_code, asset_type, price_currency)
- Adjusted price fields show 11.02% null values
- All records contain essential trading data (date, symbol, exchange, OHLC prices)

**Notable Patterns:**
- Covers 13 distinct ETF symbols tracking various global markets
- Date range spans 3,512 unique trading dates
- Volume ranges from minimal (15.0) to extremely high (322.6M), indicating varied liquidity
- Most stock splits are standard 1:1 (no split), with rare events (0.25, 0.5, 60.0 splits)
- Dividends present but mostly zero (340 unique values suggest regular dividend payments)

## Column Details

### Price Columns

**open (FLOAT64)**
- Opening price for the trading day
- Complete data (0% nulls)
- Range: $8.74 to $143.14
- 8,445 unique values
- Good for: Daily price analysis, gap detection, opening range strategies

**high (FLOAT64)**
- Highest price during the trading day
- Complete data (0% nulls)
- Range: $8.75 to $143.235
- 12,653 unique values
- Good for: Volatility analysis, resistance levels, range calculations

**low (FLOAT64)**
- Lowest price during the trading day
- Complete data (0% nulls)
- Range: $8.64 to $142.2
- 12,701 unique values
- Good for: Support levels, risk assessment, range calculations

**close (FLOAT64)**
- Closing price for the trading day
- Complete data (0% nulls)
- Range: $8.65 to $143.18
- 8,435 unique values
- Good for: End-of-day analysis, trend calculations, performance metrics

### Adjusted Price Columns

**adj_close (FLOAT64)**
- Split and dividend-adjusted closing price
- Complete data (0% nulls)
- Range: $12.34 to $143.18
- 30,369 unique values (highest uniqueness among price columns)
- **Primary use:** Long-term performance analysis, historical comparisons

**adj_open (FLOAT64)**
- Adjusted opening price
- 11.02% null values
- Range: $12.07 to $143.14
- 29,654 unique values

**adj_high (FLOAT64)**
- Adjusted high price
- 11.02% null values
- Range: $12.54 to $143.235
- 32,280 unique values

**adj_low (FLOAT64)**
- Adjusted low price
- 11.02% null values
- Range: $12.05 to $142.195
- 32,508 unique values (highest uniqueness)

### Volume Columns

**volume (FLOAT64)**
- Raw trading volume
- Complete data (0% nulls)
- Range: 15.0 to 322,620,100.0 shares
- 44,982 unique values (extremely high uniqueness)
- Good for: Liquidity analysis, volume trends, unusual activity detection

**adj_volume (FLOAT64)**
- Split-adjusted trading volume
- 11.02% null values
- Range: 11,400.0 to 322,806,886.0 shares
- 40,486 unique values
- Good for: Historical volume comparisons

### Corporate Action Columns

**dividend (FLOAT64)**
- Dividend amount paid
- Complete data (0% nulls)
- Range: $0.0 to $4.705
- 340 unique values
- Mostly zero (no dividend), with periodic payments
- Good for: Income analysis, ex-dividend date identification

**split_factor (FLOAT64)**
- Stock split multiplier
- Complete data (0% nulls)
- Only 4 unique values: 0.25, 0.5, 1.0, 60.0
- Predominantly 1.0 (no split)
- Good for: Identifying split events, data adjustment validation

### Identifier Columns

**symbol (STRING)**
- ETF ticker symbol
- Complete data (0% nulls)
- 13 unique symbols
- Values include: ACWI, EEM, EPI, EWA, EWG, EWJ, EWQ, EWU, EWW, EWY, EWZ, FXI
- **Primary key component** (with date)
- Good for: Filtering specific ETFs, grouping by security

**exchange (STRING)**
- Trading exchange code
- Complete data (0% nulls)
- 2 unique values: ARCX (NYSE Arca), XNAS (Nasdaq)
- Good for: Exchange-based analysis

**date (DATE)**
- Trading date
- Complete data (0% nulls)
- 3,512 unique dates
- **Primary key component** (with symbol)
- Good for: Time-series analysis, date filtering, trend analysis

### Metadata Columns (High Null Percentage)

**name (STRING)**
- Full ETF name
- 92.88% null values
- 13 unique values when present
- Examples: "ISHARES MSCI JAPAN ETF", "ISHARES CHINA LARGE-CAP ETF"
- Limited utility for queries due to sparsity

**exchange_code (STRING)**
- Full exchange name
- 92.88% null values
- 2 unique values: NASDAQ, NYSE ARCA
- Redundant with 'exchange' column

**asset_type (STRING)**
- Type of security
- 92.88% null values
- Only value: "ETF"
- All securities are ETFs when data is present

**price_currency (STRING)**
- Currency denomination
- 92.88% null values
- 2 unique values: USD, usd (inconsistent casing)
- All prices appear to be in USD

## Potential Query Considerations

### Excellent for Filtering:
- **symbol**: Filter by specific ETF (13 options)
- **date**: Time-range queries (date ranges, specific dates)
- **exchange**: Filter by trading venue (2 options)
- **dividend > 0**: Identify dividend payment dates
- **split_factor != 1.0**: Identify stock split events

### Good for Grouping/Aggregation:
- **symbol**: Aggregate metrics by ETF
- **date**: Time-series aggregations (daily, monthly, yearly)
- **exchange**: Compare performance across exchanges
- Date functions: EXTRACT(YEAR), EXTRACT(MONTH) for temporal grouping

### Potential Join Keys:
- **(symbol, date)**: Composite primary key for joining with other market data
- **symbol**: Join with ETF metadata tables
- **date**: Join with economic indicators, market indices

### Data Quality Considerations for Queries:

1. **Adjusted vs Unadjusted Prices**: Use adjusted prices (adj_close, etc.) for historical analysis to account for splits and dividends; use unadjusted for intraday or recent analysis

2. **Null Handling**: 
   - Adjusted volume/price fields have 11.02% nulls - queries should use COALESCE or filter these out
   - Metadata fields (name, exchange_code, etc.) are 92.88% null - avoid relying on these unless necessary

3. **Volume Outliers**: Extreme volume range (15 to 322M) may require outlier handling or logarithmic scaling for analysis

4. **Date Continuity**: Not all trading days may be present for all symbols (holidays, trading halts) - use date series joins carefully

5. **Price Precision**: Prices stored as FLOAT64 may have floating-point precision issues - consider rounding for comparisons

6. **Currency Consistency**: While price_currency shows USD/usd, the sparsity and inconsistent casing suggest all prices are USD - queries can assume USD denomination

## Keywords

Financial data, stock market, ETF data, iShares, global markets, trading data, OHLC prices, open high low close, volume analysis, dividend history, stock splits, adjusted prices, NYSE Arca, Nasdaq, market data warehouse, time series data, international ETFs, emerging markets, MSCI indices, daily trading data, exchange-traded funds, market analysis, quantitative finance, price history, trading volume, corporate actions

## Table and Column Documentation

**Table Comment:** None provided

**Column Comments:** None provided for any columns

The absence of formal documentation suggests this is a staging table where data transformations or validations may occur before moving to production analytical tables. The "stg_" prefix (staging) in the table name confirms this pattern.