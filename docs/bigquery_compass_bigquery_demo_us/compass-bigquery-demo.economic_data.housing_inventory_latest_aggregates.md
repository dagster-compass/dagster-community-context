---
columns:
- current_value (FLOAT64)
- date_grain (STRING)
- month (DATE)
- pct_change_1y (FLOAT64)
- pct_change_3m (FLOAT64)
- pct_change_6m (FLOAT64)
- series_code (STRING)
- series_name (STRING)
schema_hash: 8097db757443d6e29cddccdf6045baaf6e9b3d955e1ff198652ddedbe4d02d5e

---
# Housing Inventory Latest Aggregates - Table Summary

## Overall Dataset Characteristics

- **Total Rows**: 64
- **Data Quality**: High quality dataset with minimal null values (only 1.56% null in 2 columns)
- **Temporal Coverage**: Quarterly data spanning from 2013 to 2025 (11 unique months)
- **Granularity**: All records are at quarterly grain
- **Content**: Housing market metrics including vacancy rates, ownership rates, and occupied housing units
- **Structure**: Time-series aggregated data with current values and percentage changes over multiple time periods

## Column Details

### series_name (STRING)
- **Type**: Categorical identifier (descriptive names)
- **Null Values**: None (0%)
- **Unique Values**: 18 distinct housing metrics
- **Key Metrics Include**:
  - Occupancy types (Owner/Renter Occupied Units)
  - Vacancy rates (Homeowner/Rental Vacancy Rate)
  - Market status (Held Off Market, Rented or Sold)
  - Seasonal adjusted measures
- **Usage**: Primary dimension for filtering and grouping housing metrics

### month (DATE)
- **Type**: Temporal dimension (quarterly dates)
- **Null Values**: None (0%)
- **Format**: First day of month (YYYY-MM-01)
- **Range**: 2013-10-01 to 2025-04-01
- **Pattern**: Quarterly snapshots (January, April, July, October)
- **Usage**: Time-based filtering, trending, and time-series analysis

### series_code (STRING)
- **Type**: Categorical identifier (abbreviated codes)
- **Null Values**: None (0%)
- **Unique Values**: 18 codes
- **Examples**: HOR, HVR, OCC, OCCUSE, OFFMAR, OTH, OWNOCC, RENT, RNTOCC, RNTSLD, RVR
- **Usage**: Compact alternative to series_name for filtering and joining

### current_value (FLOAT64)
- **Type**: Numeric measure (main metric)
- **Null Values**: None (0%)
- **Range**: 0.8 to 146,888.0 (wide range indicates different measurement scales)
- **Distribution**: Appears to include both:
  - Percentages/rates (0.8 - 65.7, likely vacancy/ownership rates)
  - Absolute counts (803 - 146,888, likely housing unit counts in thousands)
- **Usage**: Primary measure for analysis, aggregation, and comparison

### date_grain (STRING)
- **Type**: Metadata field
- **Null Values**: None (0%)
- **Unique Values**: 1 ("Quarterly")
- **Purpose**: Documents temporal granularity
- **Usage**: Informational; can be used to confirm data frequency in queries

### pct_change_3m (FLOAT64)
- **Type**: Numeric measure (percentage change)
- **Null Values**: None (0%)
- **Range**: -0.42 to 0.08 (-42% to +8%)
- **Distribution**: Mostly small changes (-0.15 to 0.01)
- **Usage**: Quarter-over-quarter trend analysis

### pct_change_1y (FLOAT64)
- **Type**: Numeric measure (percentage change)
- **Null Values**: 1.56% (likely earliest records without prior year data)
- **Range**: -0.42 to 0.08 (-42% to +8%)
- **Distribution**: Similar to 3-month changes
- **Usage**: Year-over-year comparison and trend analysis

### pct_change_6m (FLOAT64)
- **Type**: Numeric measure (percentage change)
- **Null Values**: 1.56% (likely earliest records)
- **Range**: -0.42 to 0.08 (-42% to +8%)
- **Distribution**: Similar to other change metrics
- **Usage**: Semi-annual trend analysis

## Potential Query Considerations

### Good Filtering Columns
- **series_name/series_code**: Filter by specific housing metrics (e.g., vacancy rates, occupancy)
- **month**: Filter by time period, recent quarters, specific years
- **date_grain**: Confirm quarterly data (though all records are quarterly)

### Good Grouping/Aggregation Columns
- **series_name/series_code**: Group metrics for comparative analysis
- **month**: Time-based aggregations, trending over quarters/years
- Combined grouping: series by time for longitudinal analysis

### Potential Join Keys
- **series_code**: More efficient join key than series_name (shorter strings)
- **month**: Join with other economic/housing datasets by time period
- **Composite key**: (series_code, month) for unique record identification

### Data Quality Considerations

1. **Scale Differences**: Current_value contains both rates (0-100) and counts (thousands), requiring careful interpretation
2. **Null Patterns**: 1.56% nulls in 6-month and 1-year changes suggest limited historical data for some records
3. **Percentage Changes**: Values are in decimal format (-0.42 = -42%), not percentage format
4. **Temporal Consistency**: All data at quarterly grain, no mixed frequencies
5. **Latest Data**: "Latest aggregates" suggests this is a current snapshot table, possibly updated quarterly

### Recommended Query Patterns

1. **Time-series queries**: Use month for ordering and windowing
2. **Metric comparison**: Group by series_name for cross-metric analysis
3. **Trend analysis**: Use pct_change columns for growth/decline patterns
4. **Recent data**: Filter on MAX(month) for most current values
5. **Rate vs. Count**: Filter series to separate percentage metrics from unit counts

## Keywords

housing inventory, vacancy rates, homeownership rate, rental vacancy, occupied units, owner occupied, renter occupied, quarterly data, housing metrics, housing market, real estate statistics, economic indicators, housing supply, vacancy statistics, time series, housing aggregates, seasonal adjustment, housing units, off market housing, economic data

## Table and Column Documentation

### Table Comment
Not provided in the analysis report.

### Column Comments
Not provided in the analysis report.