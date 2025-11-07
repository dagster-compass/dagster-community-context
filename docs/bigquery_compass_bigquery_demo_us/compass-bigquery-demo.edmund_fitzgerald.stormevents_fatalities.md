---
columns:
- event_id (INT64)
- event_yearmonth (FLOAT64)
- fatality_age_years (FLOAT64)
- fatality_date (DATE)
- fatality_day (INT64)
- fatality_id (INT64)
- fatality_location (STRING)
- fatality_sex (STRING)
- fatality_time (DATE)
- fatality_type (STRING)
- fatality_yearmonth (INT64)
schema_hash: c76da1b64b2bb0a2d5d5a621101afbfd88fb0da26913d7d55d6aa46ea546e2ef

---
# Table Summary: compass-bigquery-demo.edmund_fitzgerald.stormevents_fatalities

## Overall Dataset Characteristics

- **Total Rows**: 24,480 records
- **Time Span**: Data spans from 1951 to 2025 (195102 to 202505 in yearmonth format)
- **Data Type**: Storm event fatality records tracking deaths and injuries from weather events
- **Data Quality**: Generally good with some notable null patterns:
  - Most columns have low null rates (<25%)
  - `fatality_time` column is 97.44% null (largely unused)
  - Some demographic data gaps (18-23% nulls for age and sex)
- **Distribution Pattern**: Event-based fatality tracking with multiple fatalities often linked to single events (14,386 unique events for 24,480 fatalities)

## Column Details

### Identifier Columns

**fatality_id** (INT64)
- Primary identifier for each fatality record
- Range: 2 to 990,000,007
- No nulls (0.00%)
- 23,566 unique values out of 24,480 rows (some duplicate IDs exist)
- Good for joins and unique record identification

**event_id** (INT64)
- Links fatalities to specific storm events
- Range: 445 to 990,000,003
- No nulls (0.00%)
- 14,386 unique values (multiple fatalities per event common)
- Key field for joining to storm event tables
- Average ~1.7 fatalities per event

### Temporal Columns

**fatality_date** (DATE)
- Date of the fatality
- Near-complete data (0.07% nulls)
- 6,901 unique dates
- Sample range: 1951 to 2025
- Good for temporal filtering and trend analysis

**fatality_yearmonth** (INT64)
- Year-month composite in YYYYMM format
- No nulls (0.00%)
- 695 unique values
- Range: 195102 to 202505
- Excellent for monthly aggregations and time series

**event_yearmonth** (FLOAT64)
- Year-month of the associated event
- Very low null rate (0.09%)
- 611 unique values
- Includes special value 999999.0 (likely indicates missing/unknown)
- Range: 195102.0 to 999999.0

**fatality_day** (INT64)
- Day of month (1-31, with 0 for unknown)
- No nulls (0.00%)
- 32 unique values (0-31)
- Day 0 likely represents unknown day

**fatality_time** (DATE)
- Intended for time of death but stored as DATE type
- 97.44% null (mostly unused)
- Only 145 unique values
- Values appear malformed (1700-01-01 format suggests time stored incorrectly)
- **NOT RECOMMENDED for queries**

### Demographic Columns

**fatality_age_years** (FLOAT64)
- Age of victim in years
- 23.28% null (missing for ~1 in 4 records)
- Range: 0.0 to 102.0
- 103 unique values
- Useful for age-based analysis when present

**fatality_sex** (STRING)
- Gender of victim
- 18.42% null
- 2 values: 'M' (Male), 'F' (Female)
- Good for demographic breakdowns

### Classification Columns

**fatality_type** (STRING)
- Type of fatality
- No nulls (0.00%)
- 2 values: 'D' (Direct), 'I' (Indirect)
- 'D' = Direct fatality (directly caused by weather)
- 'I' = Indirect fatality (indirectly related to weather event)
- Critical for classification analysis

**fatality_location** (STRING)
- Location where fatality occurred
- 5.62% null
- 20 unique categories
- Common values: "Other", "Unknown", "Camping", "Permanent Home", "Mobile/Trailer Home", "Outside/Open Areas", "Boat", "Boating", "Business", "Church"
- Other locations: Ball Field, Golfing, Heavy Equipment/Construction, In Water
- Useful for risk location analysis

## Query Considerations

### Best Columns for Filtering
- **fatality_date**: Precise date filtering with minimal nulls
- **fatality_yearmonth**: Efficient monthly filtering, no nulls
- **fatality_type**: Clean binary classification (Direct/Indirect)
- **event_id**: Linking to specific events
- **fatality_day**: Day of month filtering

### Best Columns for Grouping/Aggregation
- **fatality_yearmonth**: Temporal trends (monthly)
- **fatality_type**: Direct vs Indirect analysis
- **fatality_location**: Location-based risk analysis
- **fatality_sex**: Gender demographics
- **event_id**: Fatalities per event analysis
- **event_yearmonth**: Event-based temporal grouping

### Potential Join Keys
- **event_id**: Primary key for joining to storm events table
- **fatality_id**: Unique identifier for this table
- Date fields can join to temporal dimension tables

### Data Quality Considerations
1. **Avoid fatality_time**: 97% null and appears malformed
2. **Handle nulls in demographics**: 18-23% missing for age and sex
3. **Special values**: event_yearmonth = 999999.0 indicates missing data
4. **Day 0**: In fatality_day represents unknown day
5. **Duplicate fatality_ids**: Some IDs appear multiple times (23,566 unique vs 24,480 rows)
6. **Location nulls**: 5.62% have "None" - combine with "Unknown" for analysis
7. **Temporal consistency**: Check fatality_date vs fatality_yearmonth for consistency

### Recommended Query Patterns
- Filter by date ranges using fatality_date or fatality_yearmonth
- Group by fatality_type for Direct vs Indirect analysis
- Use event_id to count fatalities per storm event
- Filter out event_yearmonth = 999999.0 for clean temporal analysis
- Use COALESCE for handling null demographics
- Consider fatality_location for spatial risk analysis

## Keywords
storm events, weather fatalities, deaths, injuries, NOAA, severe weather, casualties, storm deaths, meteorological fatalities, weather-related deaths, direct fatalities, indirect fatalities, disaster casualties, extreme weather, time series, temporal analysis, demographic analysis, fatality location, event casualties, storm impact

## Table and Column Documentation

**Note**: No table-level comment or column-level comments were provided in the analysis report. This table appears to be part of the NOAA Storm Events Database tracking fatalities associated with severe weather events in the United States.