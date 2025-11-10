---
columns:
- episode_id (INT64)
- event_id (INT64)
- event_yearmonth (INT64)
- location_azimuth (STRING)
- location_index (INT64)
- location_latitude (FLOAT64)
- location_latitude_alternate (FLOAT64)
- location_longitude (FLOAT64)
- location_longitude_alternate (FLOAT64)
- location_name (STRING)
- location_range_miles (FLOAT64)
schema_hash: 04f57cfc6327ebfaf6791fd219d6261cd9a68b0059167d98fee3ea9ea636bb73

---
# Table Summary: stormevents_locations

## Overview
This table contains **1,742,275 rows** of location data related to storm events, spanning from **June 1972 to May 2025**. The table represents a comprehensive dataset of geographic points associated with weather events, with each row representing a specific location within a storm event. Multiple locations can be associated with a single event (indicated by `location_index` ranging from 1-8).

## Overall Data Characteristics

**Data Quality:** Generally good, with most critical identifiers having 100% completeness. However, there are notable null percentages in location descriptors:
- Location names are missing in ~11% of records
- Azimuth and range information is missing in ~25% of records  
- Latitude/longitude coordinates are missing in ~15% of records
- Alternate coordinate formats are missing in ~27% of records

**Key Pattern:** The data shows a hierarchical structure where episodes contain multiple events, and events can have multiple location points (up to 8 indexed locations per event).

## Column Details

### Identifiers & Temporal Data

**event_yearmonth** (INT64)
- Format: YYYYMM (e.g., 201706 = June 2017)
- 354 unique month-year combinations
- Spans June 1972 (197206) to May 2025 (202505)
- Complete data (0% nulls)
- Primary temporal dimension for filtering

**episode_id** (INT64)
- 317,600 unique episodes
- Range: 2 to 990,000,001
- Complete data (0% nulls)
- Groups related storm events together

**event_id** (INT64)
- 1,272,091 unique events
- Range: 7 to 990,000,001
- Complete data (0% nulls)
- Primary event identifier (many-to-one with episodes)

**location_index** (INT64)
- Values: 1-8 only
- Indicates multiple location points per event
- Complete data (0% nulls)
- Used for ordering/sequencing locations within an event

### Location Descriptors

**location_name** (STRING)
- 54,319 unique location names
- 11.36% null values
- Examples: "COUNTYWIDE", "BARDWELL", "VALE", "WAMBA", "HANKINSON"
- Mix of city names, geographic features, and airports
- Some entries include airport codes (e.g., "(1K5)ELKHART")

**location_azimuth** (STRING)
- 16 unique values (compass directions)
- Values: E, ENE, ESE, N, NE, NNE, NNW, NW, S, SE, SSE, SSW, SW, W, WNW, WSW
- 24.57% null values
- Indicates direction from a reference point

**location_range_miles** (FLOAT64)
- Range: 0.0 to 519.78 miles
- 5,674 unique values
- 24.57% null values (matches azimuth null pattern)
- Indicates distance from a reference point
- Used in conjunction with azimuth for relative positioning

### Geographic Coordinates

**location_latitude** (FLOAT64)
- Range: -14.5551 to 97.1 (note: 97.1 appears anomalous, as valid latitudes are -90 to 90)
- 182,970 unique values
- 15.02% null values
- Standard decimal degree format
- Example values: 37.46667, 40.79, 38.12

**location_longitude** (FLOAT64)
- Range: -171.4 to 171.4689
- 315,788 unique values
- 15.02% null values (matches latitude null pattern)
- Standard decimal degree format
- Example values: -92.06, -88.15, -94.45

**location_latitude_alternate** (FLOAT64)
- Range: -1,433,306 to 7,030,174
- 183,166 unique values
- 27.11% null values
- Appears to be degrees-minutes-seconds format compressed (e.g., 332430.0 = 33°24'30")
- Example: 4427.0, 2433426.0, 2918000.0

**location_longitude_alternate** (FLOAT64)
- Range: -17,128,134 to 17,055,188
- 316,165 unique values
- 27.11% null values (matches alternate latitude null pattern)
- Appears to be degrees-minutes-seconds format compressed
- Example: 9849800.0, 9825290.0

## Query Considerations

### Optimal Filtering Columns
- **event_yearmonth**: Excellent for temporal filtering (354 distinct values, fully indexed conceptually)
- **episode_id / event_id**: Perfect for specific event lookups
- **location_index**: Useful for filtering to first/last locations in a sequence
- **location_azimuth**: Good for directional analysis (16 values)

### Aggregation Opportunities
- **event_yearmonth**: Time-series analysis, seasonal trends
- **location_name**: Geographic hotspot analysis
- **location_azimuth**: Directional pattern analysis
- **location_index**: Multi-point event analysis

### Join Keys
- **event_id**: Primary key for joining to main storm events table
- **episode_id**: For episode-level analysis across multiple events
- **(event_id, location_index)**: Composite key for unique location identification

### Data Quality Considerations

1. **Coordinate Validation Needed**: 
   - Latitude value of 97.1 exceeds valid range (-90 to 90)
   - Should validate geographic coordinates before spatial analysis

2. **Null Handling**:
   - ~25% of records lack azimuth/range data (relative positioning)
   - ~15% lack standard coordinates
   - ~27% lack alternate coordinate format
   - Must account for nulls in location-based queries

3. **Coordinate Format Duality**:
   - Both decimal and alternate formats available
   - Alternate formats have higher null percentage
   - Choose decimal format (latitude/longitude) for most queries

4. **Multiple Locations Per Event**:
   - Use location_index for ordering
   - Consider whether to aggregate or select specific locations
   - Joining without location_index will create multiple rows per event

5. **Temporal Range**:
   - Historical data starts in 1972
   - Future dates exist (up to 2025) - may be forecasts or data entry errors

## Keywords
storm events, weather data, geographic locations, coordinates, latitude, longitude, NOAA, severe weather, event locations, multi-point events, storm tracking, meteorological data, azimuth, range, location index, episode data, event data, temporal weather data, geographic analysis, compass directions, location names

## Table and Column Documentation

**Table Comment:** Not provided

**Column Comments:** 
- event_yearmonth: No comment provided
- episode_id: No comment provided  
- event_id: No comment provided
- location_index: No comment provided
- location_name: No comment provided
- location_azimuth: No comment provided
- location_range_miles: No comment provided
- location_latitude: No comment provided
- location_latitude_alternate: No comment provided
- location_longitude: No comment provided
- location_longitude_alternate: No comment provided

*Note: No formal documentation/comments are present in the table schema for this dataset.*