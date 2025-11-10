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
# Table Documentation Summary: stormevents_fatalities

## Overall Dataset Characteristics

**Total Rows:** 24,480

**General Description:** This table contains records of fatalities related to storm events, tracking demographic information, location, and temporal details of weather-related deaths from 1951 to 2025. The data appears to be part of a comprehensive storm events database tracking both direct (D) and indirect (I) fatalities.

**Data Quality Observations:**
- High-quality temporal data with minimal nulls in date fields
- Significant missing data in demographic fields (age: 23.28%, sex: 18.42%)
- fatality_time field is largely unusable (97.44% null)
- Event linkage appears robust with event_id having no nulls
- Some anomalous values exist (event_yearmonth showing 999999.0, likely indicating missing/unknown values)

**Notable Patterns:**
- Data spans approximately 74 years (1951-2025)
- 20 distinct fatality locations tracked
- Age distribution ranges from infants (0.0) to elderly (102.0)
- Multiple fatalities can be linked to single storm events (14,386 unique events for 24,480 fatalities)

## Column Details

### fatality_id (INT64)
- **Type:** Integer, Primary identifier
- **Nulls:** 0.00% - Excellent data quality
- **Range:** 2 to 990,000,007
- **Uniqueness:** 23,566 unique values (96.3% of total rows)
- **Purpose:** Primary key for individual fatality records
- **Query Considerations:** Good for exact matching and deduplication checks

### event_id (INT64)
- **Type:** Integer, Foreign key
- **Nulls:** 0.00% - Complete data
- **Range:** 445 to 990,000,003
- **Uniqueness:** 14,386 unique events
- **Purpose:** Links fatalities to storm events (multiple fatalities per event possible)
- **Query Considerations:** Essential join key for connecting to event details; good for grouping to analyze multi-fatality events

### fatality_date (DATE)
- **Type:** Date
- **Nulls:** 0.07% - Near-complete data
- **Range:** 1951-2025 (6,901 unique dates)
- **Format:** YYYY-MM-DD
- **Query Considerations:** Primary temporal filter; useful for time-series analysis, trending, and year-over-year comparisons

### fatality_yearmonth (INT64)
- **Type:** Integer representation of year-month
- **Nulls:** 0.00% - Complete data
- **Range:** 195102 to 202505 (695 unique values)
- **Format:** YYYYMM (e.g., 201906 = June 2019)
- **Query Considerations:** Excellent for monthly aggregations and time-based grouping without date parsing

### fatality_day (INT64)
- **Type:** Integer (day of month)
- **Nulls:** 0.00%
- **Range:** 0-31
- **Note:** Value 0 appears anomalous (possibly indicating unknown day)
- **Query Considerations:** Useful for day-of-month analysis patterns

### fatality_time (DATE)
- **Type:** Date (likely TIME stored as DATE)
- **Nulls:** 97.44% - **NOT RECOMMENDED FOR ANALYSIS**
- **Pattern:** Non-null values appear as dates in 1700s range (1700-01-01 to 1715-01-01), suggesting time-of-day stored as date
- **Query Considerations:** Largely unusable due to missing data; avoid in queries unless specifically filtering for records with time data

### event_yearmonth (FLOAT64)
- **Type:** Float representation of year-month
- **Nulls:** 0.09% - Near-complete
- **Range:** 195102.0 to 999999.0
- **Special Values:** 999999.0 appears as placeholder for unknown/missing event dates
- **Query Considerations:** Useful for event-to-fatality temporal analysis; filter out 999999.0 for valid temporal queries

### fatality_age_years (FLOAT64)
- **Type:** Float (age in years)
- **Nulls:** 23.28% - Significant missing data
- **Range:** 0.0 to 102.0 (103 unique values)
- **Distribution:** Covers full lifespan from infants to elderly
- **Query Considerations:** Useful for demographic analysis but requires null handling; can create age bands for aggregation

### fatality_sex (STRING)
- **Type:** String (categorical)
- **Nulls:** 18.42% - Moderate missing data
- **Values:** 'M' (Male), 'F' (Female)
- **Query Considerations:** Good for gender-based analysis; requires null handling for complete demographic profiles

### fatality_type (STRING)
- **Type:** String (categorical)
- **Nulls:** 0.00% - Complete data
- **Values:** 'D' (Direct), 'I' (Indirect)
- **Purpose:** Classifies whether death was directly caused by storm or indirect consequence
- **Query Considerations:** Essential for distinguishing immediate vs. secondary storm impacts; excellent filter/group by column

### fatality_location (STRING)
- **Type:** String (categorical)
- **Nulls:** 5.62% - Good data quality
- **Unique Values:** 20 distinct locations
- **Common Categories:** 
  - Permanent Home
  - Vehicle/Towed Trailer
  - Outside/Open Areas
  - In Water
  - Boating/Boat
  - Business
  - Camping
  - Church
  - Ball Field
  - Golfing
  - Heavy Equipment/Construction
- **Query Considerations:** Excellent for location-based risk analysis; well-suited for grouping and filtering

## Potential Query Considerations

### Strong Filter Columns:
1. **fatality_type** - Complete data, 2 clear categories
2. **fatality_yearmonth** - Complete temporal data, good for date ranges
3. **fatality_date** - Near-complete, precise temporal filtering
4. **fatality_location** - Low nulls, meaningful categories

### Good Grouping/Aggregation Columns:
1. **fatality_yearmonth** - Monthly trend analysis
2. **fatality_location** - Risk by location type
3. **fatality_type** - Direct vs. indirect impact analysis
4. **event_id** - Multi-fatality event analysis
5. **fatality_age_years** - Age demographic patterns (with null handling)

### Join Keys:
- **event_id** - Primary join key to related storm event tables
- **fatality_id** - Unique identifier for deduplication or detailed lookups

### Data Quality Considerations:
1. **Always filter out** event_yearmonth = 999999.0 for temporal analysis
2. **Handle nulls** in age (23.28%) and sex (18.42%) for demographic queries
3. **Avoid fatality_time** unless specifically needed (97% null)
4. **Check for fatality_day = 0** which may indicate unknown day
5. **Account for multiple fatalities per event** when aggregating by event_id

### Recommended Query Patterns:
- Time-series: Use fatality_yearmonth for efficient monthly aggregations
- Demographics: JOIN age and sex but handle nulls appropriately
- Location risk: GROUP BY fatality_location with fatality_type
- Event severity: COUNT fatalities per event_id to identify major disasters
- Temporal trends: Compare direct vs. indirect fatalities over time

## Keywords

storm fatalities, weather deaths, direct fatalities, indirect fatalities, storm casualties, natural disaster deaths, weather-related mortality, NOAA storm data, meteorological fatalities, severe weather deaths, demographic storm analysis, temporal storm analysis, fatality locations, age demographics, storm event casualties, disaster mortality tracking, weather hazard deaths, storm victim data, multi-fatality events, fatality time series

## Table and Column Documentation

**Table Comment:** Not provided

**Column Comments:** Not provided

This table represents a critical public safety dataset for analyzing weather-related mortality patterns, risk factors, and demographic vulnerabilities to severe weather events across more than seven decades of U.S. history.