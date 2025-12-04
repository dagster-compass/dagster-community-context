---
columns:
- value_domestic (FLOAT64)
- value_foreign (FLOAT64)
- year (INT64)
schema_hash: bf051adb696724a3f6c09cedf6daa16ee61f58a77fc45c85560eb273f21750cc

---
# Table Analysis Summary: annual_us_tonnage_great_lakes

## Overall Dataset Characteristics

- **Total Rows**: 69
- **Time Period**: 1952 to 2020 (69 consecutive years of annual data)
- **Data Quality**: Excellent - no null values in any column
- **Dataset Purpose**: Tracks annual tonnage (likely in millions of tons) of cargo transported on the Great Lakes, split between domestic and foreign trade
- **Notable Pattern**: Foreign tonnage includes negative values, suggesting net exports or data adjustments
- **Historical Context**: The table name references the Edmund Fitzgerald, the famous Great Lakes freighter that sank in 1975

## Column Details

### year (INT64)
- **Data Type**: Integer (INT64)
- **Null Pattern**: No nulls (0.00%)
- **Range**: 1952-2020 (69 consecutive years)
- **Characteristics**: 
  - Primary temporal dimension
  - One row per year
  - Covers nearly 7 decades of Great Lakes shipping history
  - Includes the Edmund Fitzgerald era (1958-1975)

### value_domestic (FLOAT64)
- **Data Type**: Decimal (FLOAT64)
- **Null Pattern**: No nulls (0.00%)
- **Range**: 40.47 to 162.29 (likely millions of tons)
- **Distribution Pattern**:
  - Peak appears in late 1950s (162.29 in 1958)
  - General declining trend evident from sample values
  - Modern era (2010s) shows values in 50-60 range
- **Characteristics**: Represents domestic cargo tonnage on Great Lakes
- **Query Consideration**: Key metric for analyzing domestic shipping trends

### value_foreign (FLOAT64)
- **Data Type**: Decimal (FLOAT64)
- **Null Pattern**: No nulls (0.00%)
- **Range**: -8.92 to 41.62
- **Distribution Pattern**:
  - Includes negative values (minimum: -8.92)
  - Peak around 32-41 range
  - Generally lower volumes than domestic
- **Unusual Characteristic**: Negative values may indicate:
  - Net trade balance calculations
  - Data adjustments or corrections
  - Specific accounting methodology
- **Query Consideration**: Need to understand meaning of negative values for accurate analysis

## Potential Query Considerations

### Filtering Columns
- **year**: Excellent for time-based filtering
  - Decade analysis (1950s, 1960s, etc.)
  - Historical periods (pre/post Edmund Fitzgerald 1975)
  - Recent vs. historical comparisons
  - Economic event periods (recessions, etc.)

### Aggregation Opportunities
- **Time-based aggregations**: 
  - Decade averages
  - Multi-year moving averages
  - Year-over-year changes
- **Calculated metrics**:
  - Total tonnage (domestic + foreign)
  - Domestic/foreign ratio
  - Percentage changes over time
  - Trend analysis

### Join Considerations
- **Potential join keys**: 
  - `year` can join with economic indicators, weather data, or other time-series datasets
  - Could correlate with shipping incidents, vessel counts, or port statistics
  - Historical events or policy changes

### Data Quality Considerations
1. **Negative values in value_foreign**: 
   - Queries should account for this or filter appropriately
   - May need clarification on business meaning
   
2. **Units unclear**: 
   - Values appear to be in millions of tons based on magnitude
   - Should confirm units for accurate interpretation

3. **Completeness**: 
   - No gaps in annual data (consecutive years)
   - Reliable for time-series analysis

4. **Trend analysis**: 
   - Declining domestic tonnage suggests industry changes
   - Foreign trade volatility (including negatives) suggests different dynamics

## Keywords

Great Lakes, shipping tonnage, domestic cargo, foreign trade, annual statistics, maritime commerce, Edmund Fitzgerald, time series data, US Great Lakes, cargo volume, 1952-2020, historical shipping data, waterborne commerce, inland shipping, bulk cargo, lake freight, tonnage statistics, trade volume, shipping trends, maritime history

## Table and Column Documentation

**Table Comment**: Not provided

**Column Comments**: 
- `year`: No comment provided
- `value_domestic`: No comment provided
- `value_foreign`: No comment provided

*Note: No explicit table or column documentation was included in the source data. The analysis above is based on observed data patterns and naming conventions.*