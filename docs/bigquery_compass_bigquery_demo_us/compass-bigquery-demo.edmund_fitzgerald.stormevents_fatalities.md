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
# Table Summary: stormevents_fatalities

## Overall Dataset Characteristics

**Total Rows:** 24,480

**General Description:** This table contains storm-related fatality records, tracking deaths and injuries from weather events from 1951 to 2025. Each record represents an individual fatality or injury associated with a storm event.

**Data Quality Observations:**
- Generally high data quality with most core fields populated
- The `fatality_time` field is severely incomplete (97.44% null), making it largely unusable
- Approximately 18-23% missing data for demographic fields (sex and age)
- Some anomalous values in `event_yearmonth` (999999.0) appear to indicate unknown/missing event dates
- Future dates present (up to 2025-05), suggesting either forecasted data or data entry errors

**Notable Patterns:**
- Data spans over 70 years (1951-2025)
- Direct fatalities (D) vs Indirect fatalities (I) are tracked via `fatality_type`
- Most fatalities occur in vehicles, permanent homes, and outdoor areas
- Male fatalities significantly outnumber female fatalities in non-null records

## Column Details

### fatality_id (INT64)
**Primary identifier for each fatality record**
- **Null Values:** 0% (fully populated)
- **Unique Values:** 23,566 (96% unique rate)
- **Range:** 2 to 990,000,007
- **Query Considerations:** Primary key candidate; use for unique record identification

### event_id (INT64)
**Links fatality to specific storm event**
- **Null Values:** 0% (fully populated)
- **Unique Values:** 14,386 distinct events
- **Range:** 445 to 990,000,003
- **Query Considerations:** Foreign key for joining to storm events table; multiple fatalities can share same event_id; excellent for aggregating fatalities by storm event

### fatality_date (DATE)
**Date when fatality occurred**
- **Null Values:** 0.07% (excellent coverage)
- **Unique Values:** 6,901 distinct dates
- **Format:** YYYY-MM-DD
- **Range:** 1951 to 2025
- **Query Considerations:** Primary temporal filter; suitable for time-series analysis, trend identification, and date range queries

### fatality_time (DATE)
**Time of fatality (stored as DATE type)**
- **Null Values:** 97.44% (severely incomplete)
- **Unique Values:** Only 145 values when present
- **Data Issues:** Appears to be incorrectly stored as DATE type with year values like 1700-1706
- **Query Considerations:** NOT RECOMMENDED for analysis due to poor data quality and apparent data type mismatch

### fatality_day (INT64)
**Day of month when fatality occurred**
- **Null Values:** 0% (fully populated)
- **Range:** 0-31 (0 appears to indicate unknown day)
- **Query Considerations:** Use with fatality_yearmonth for temporal grouping; value of 0 may need filtering in queries

### fatality_yearmonth (INT64)
**Year-month of fatality in YYYYMM format**
- **Null Values:** 0% (fully populated)
- **Unique Values:** 695 distinct year-months
- **Format:** Integer like 201606 (June 2016)
- **Range:** 195102 to 202505
- **Query Considerations:** Excellent for monthly aggregations and time-series analysis; reliable temporal grouping field

### event_yearmonth (FLOAT64)
**Year-month of associated storm event**
- **Null Values:** 0.09%
- **Unique Values:** 611 distinct values
- **Format:** Float like 201606.0
- **Range:** 195102.0 to 999999.0
- **Anomalous Values:** 999999.0 appears to indicate unknown/missing event dates
- **Query Considerations:** Filter out 999999.0 for temporal analysis; useful for identifying lag between event and fatality

### fatality_location (STRING)
**Location where fatality occurred**
- **Null Values:** 5.62%
- **Unique Values:** 20 distinct locations
- **Common Values:** 
  - Vehicle/Towed Trailer (most common)
  - Permanent Home
  - Outside/Open Areas
  - Boat/Boating
  - Business
- **Query Considerations:** Good categorical grouping field; useful for location-based risk analysis and filtering

### fatality_age_years (FLOAT64)
**Age of victim in years**
- **Null Values:** 23.28%
- **Unique Values:** 103 distinct ages
- **Range:** 0.0 to 102.0
- **Distribution:** Includes infants (0.0) through elderly (102.0)
- **Query Considerations:** Suitable for age-based analysis and demographic grouping; consider handling nulls in aggregations; can create age ranges/bins for analysis

### fatality_sex (STRING)
**Gender of victim**
- **Null Values:** 18.42%
- **Unique Values:** 2 (M, F)
- **Query Considerations:** Good for demographic analysis; male fatalities appear more prevalent; handle nulls appropriately in gender-based queries

### fatality_type (STRING)
**Classification of fatality**
- **Null Values:** 0% (fully populated)
- **Unique Values:** 2 values
  - **D:** Direct fatality (death directly caused by storm)
  - **I:** Indirect fatality (death indirectly related to storm)
- **Query Considerations:** Critical classification field; essential for distinguishing direct vs indirect storm impacts; excellent for categorical filtering and comparison

## Potential Query Considerations

### Excellent Filtering Columns:
- `fatality_date` - precise temporal filtering
- `fatality_yearmonth` - monthly temporal filtering
- `fatality_type` - direct vs indirect classification
- `fatality_location` - location-based analysis
- `event_id` - event-specific queries

### Good Grouping/Aggregation Columns:
- `fatality_yearmonth` - temporal trends
- `fatality_location` - spatial patterns
- `fatality_type` - impact classification
- `fatality_sex` - demographic analysis
- `fatality_age_years` - age-based patterns (with null handling)
- `event_id` - fatalities per storm event

### Potential Join Keys:
- `event_id` - likely joins to storm events table
- `fatality_id` - unique record identifier

### Data Quality Considerations for Queries:
1. **Always filter out `event_yearmonth = 999999.0`** for temporal event analysis
2. **Avoid using `fatality_time`** - only 2.56% populated with questionable values
3. **Handle nulls in demographic fields** (age: 23%, sex: 18%)
4. **Consider `fatality_day = 0`** as missing/unknown day value
5. **Future dates exist** (2025) - may need to filter based on current date for historical analysis
6. **Multiple fatalities per event** - use appropriate aggregation when joining to events

### Common Query Patterns:
- Fatalities by year/month: GROUP BY fatality_yearmonth
- Direct vs indirect comparison: WHERE fatality_type IN ('D', 'I')
- Location risk analysis: GROUP BY fatality_location
- Demographic patterns: GROUP BY fatality_sex, age ranges
- Storm severity: COUNT fatalities per event_id

## Keywords

storm fatalities, weather deaths, natural disaster casualties, NOAA storm data, weather-related injuries, storm event deaths, direct fatalities, indirect fatalities, weather victim demographics, storm casualty analysis, severe weather impacts, fatality locations, storm death statistics, weather mortality data, Edmund Fitzgerald dataset, BigQuery weather data, storm event casualties, weather-related mortality, fatality time series, storm impact analysis

## Table and Column Documentation

**Table Comment:** Not provided in the analysis report.

**Column Comments:** No column-level comments were provided in the analysis report. The column names are self-descriptive (e.g., fatality_location, fatality_age_years, event_id), but no additional metadata or documentation was present in the source data.