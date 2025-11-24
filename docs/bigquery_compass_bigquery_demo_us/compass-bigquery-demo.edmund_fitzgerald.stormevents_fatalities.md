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

**Description:** This table contains records of fatalities associated with storm events, spanning from 1951 to 2025. The dataset tracks individual fatalities with demographic information, location details, and links to storm events through event IDs.

**Data Quality Observations:**
- Generally good data completeness with most critical fields populated
- Significant missing data in `fatality_time` (97.44% null), suggesting time-of-death is rarely recorded
- Moderate missing data in demographic fields: `fatality_age_years` (23.28%) and `fatality_sex` (18.42%)
- High uniqueness in `fatality_id` (23,566 unique values out of 24,480 rows) indicates some duplicate fatality records
- Date range spans over 70 years (1951-2025)

**Notable Patterns:**
- The dataset contains both direct (D) and indirect (I) fatality classifications
- Fatalities occur across diverse locations (20 unique locations)
- Event linking through `event_id` suggests this table can be joined with a parent storm events table
- The `fatality_yearmonth` and `event_yearmonth` fields enable temporal analysis, though there's an anomalous `999999.0` value in `event_yearmonth`

## Column Details

### fatality_id (INT64)
- **Primary Key Candidate:** Unique identifier for fatalities
- **Data Type:** Integer
- **Null Values:** None (0%)
- **Range:** 2 to 990,000,007
- **Characteristics:** 23,566 unique values suggest some fatalities may have multiple records or the ID scheme changed over time
- **Query Use:** Primary filtering and identification field

### event_id (INT64)
- **Foreign Key Candidate:** Links to storm events
- **Data Type:** Integer
- **Null Values:** None (0%)
- **Range:** 445 to 990,000,003
- **Unique Values:** 14,386 events
- **Characteristics:** Multiple fatalities per event (24,480 fatalities across 14,386 events = ~1.7 fatalities per event average)
- **Query Use:** JOIN key for storm event details, grouping for event-level analysis

### fatality_date (DATE)
- **Data Type:** Date
- **Null Values:** Minimal (0.07%, 17 records)
- **Unique Values:** 6,901 distinct dates
- **Range:** Covers 1951-2025 (based on yearmonth fields)
- **Query Use:** Primary temporal filtering field, date-based aggregations

### fatality_type (STRING)
- **Data Type:** String
- **Null Values:** None (0%)
- **Values:** Two types only - "D" (Direct) and "I" (Indirect)
- **Query Use:** Critical categorical filter for distinguishing direct vs. indirect storm-related deaths

### fatality_location (STRING)
- **Data Type:** String
- **Null Values:** 5.62%
- **Unique Values:** 20 distinct locations
- **Common Values:** In Water, Boat, Boating, Business, Camping, Church, Golfing, Heavy Equipment/Construction, Permanent Home, Under Tree, Outside/Open Areas, Unknown, Other
- **Query Use:** Categorical grouping for location-based analysis

### fatality_age_years (FLOAT64)
- **Data Type:** Float
- **Null Values:** 23.28% (significant missing data)
- **Range:** 0.0 to 102.0 years
- **Unique Values:** 103 distinct ages
- **Query Use:** Demographic analysis, age-based filtering and binning

### fatality_sex (STRING)
- **Data Type:** String
- **Null Values:** 18.42%
- **Values:** "M" (Male), "F" (Female)
- **Query Use:** Demographic filtering and gender-based analysis

### fatality_time (DATE)
- **Data Type:** Date (appears to be mistyped, likely should be TIME)
- **Null Values:** 97.44% (almost entirely null)
- **Unique Values:** 145 non-null values
- **Characteristics:** Values like "1700-01-01" suggest time stored as date with year representing hour (17:00)
- **Data Quality Issue:** Severely incomplete; not reliable for analysis
- **Query Use:** Limited utility due to data sparseness

### fatality_day (INT64)
- **Data Type:** Integer
- **Null Values:** None (0%)
- **Range:** 0 to 31
- **Characteristics:** Day of month extracted from fatality_date; "0" may represent unknown day
- **Query Use:** Day-of-month analysis, though `fatality_date` is more reliable

### fatality_yearmonth (INT64)
- **Data Type:** Integer
- **Null Values:** None (0%)
- **Format:** YYYYMM (e.g., 201708 = July 2018)
- **Range:** 195102 to 202505
- **Unique Values:** 695 distinct months
- **Query Use:** Monthly trend analysis, temporal grouping

### event_yearmonth (FLOAT64)
- **Data Type:** Float
- **Null Values:** 0.09%
- **Format:** YYYYMM format (e.g., 201708.0)
- **Range:** 195102.0 to 999999.0
- **Data Quality Issue:** Contains anomalous value 999999.0 (likely indicating unknown/missing event date)
- **Query Use:** Event-based temporal analysis; filter out 999999.0 for valid data

## Potential Query Considerations

### Good Filtering Columns:
- `fatality_type` - Clean categorical with only 2 values (D/I)
- `fatality_date` - Well-populated temporal filter
- `event_id` - No nulls, good for event-specific queries
- `fatality_yearmonth` - No nulls, efficient for time-based filtering
- `fatality_location` - Reasonable completeness (94.38%)

### Good Grouping/Aggregation Columns:
- `fatality_type` - Direct vs. Indirect analysis
- `fatality_location` - Location-based fatality counts
- `fatality_yearmonth` / `event_yearmonth` - Temporal trends
- `event_id` - Fatalities per storm event
- `fatality_sex` - Gender demographics (when not null)
- `fatality_age_years` - Age demographics (with binning)

### Join Keys:
- **Primary:** `event_id` - Link to parent storm events table
- **Secondary:** `fatality_id` - Link to any detailed fatality information tables

### Data Quality Considerations for Queries:

1. **Handle Missing Demographics:**
   - Include NULL handling for `fatality_age_years` (23.28% null)
   - Include NULL handling for `fatality_sex` (18.42% null)

2. **Filter Anomalous Values:**
   - Exclude `event_yearmonth = 999999.0` for valid temporal analysis
   - Consider `fatality_day = 0` as potential data quality issue

3. **Time Field Limitations:**
   - Avoid using `fatality_time` due to 97.44% null rate
   - Rely on `fatality_date` for temporal precision

4. **Duplicate Consideration:**
   - 24,480 rows with only 23,566 unique `fatality_id` values suggests ~900 potential duplicates
   - Use DISTINCT or GROUP BY when counting unique fatalities

5. **Date Consistency:**
   - Both `fatality_date` and `fatality_yearmonth` available; choose based on precision needs
   - `event_yearmonth` may differ from `fatality_yearmonth` (death may occur after event)

## Keywords

storm events, fatalities, deaths, weather-related deaths, natural disasters, mortality, storm casualties, NOAA, severe weather, direct deaths, indirect deaths, casualty location, demographic data, temporal analysis, event casualties, weather fatalities, storm impact, death records, public safety, meteorological data

## Table and Column Documentation

**Table Comment:** Not provided in the analysis report.

**Column Comments:** No column-level comments were provided in the analysis report.