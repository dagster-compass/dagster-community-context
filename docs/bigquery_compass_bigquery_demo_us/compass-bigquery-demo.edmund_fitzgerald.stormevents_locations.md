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
# Table Summary: compass-bigquery-demo.edmund_fitzgerald.stormevents_locations

## Overall Dataset Characteristics

**Total Rows:** 1,742,275

**Description:** This table contains geographic location data for storm events, with multiple location points per event (indicated by location_index 1-8). The dataset spans from June 1972 to May 2025 (based on event_yearmonth range), providing detailed spatial information about where storm events occurred.

**Data Quality Observations:**
- Good primary key structure with event_id and location_index combinations
- Significant null values in location detail fields (~24-27% for range/azimuth data, ~11-15% for coordinate data)
- Some data quality issues in coordinate fields (latitude values >90, extremely large alternate coordinate values)
- Generally complete for core identifiers (event_yearmonth, episode_id, event_id, location_index)

**Notable Patterns:**
- Most events have multiple location points (location_index ranges 1-8)
- Location coordinates appear in two formats: standard lat/lon and an "alternate" format with much larger values (possibly a different coordinate system or encoding)
- Distance and directional data (range_miles and azimuth) are frequently missing together (same 24.57% null rate)

## Column Details

### event_yearmonth (INT64)
- **Format:** YYYYMM integer format
- **Range:** 197206 (June 1972) to 202505 (May 2025)
- **Null Values:** None (0%)
- **Unique Values:** 354 distinct year-month combinations
- **Comment:** None provided
- **Usage:** Primary temporal dimension for filtering and time-series analysis

### episode_id (INT64)
- **Format:** Sequential integer identifiers
- **Range:** 2 to 990,000,001
- **Null Values:** None (0%)
- **Unique Values:** 317,600 distinct episodes
- **Comment:** None provided
- **Usage:** Groups related storm events together; potential join key to episode-level tables

### event_id (INT64)
- **Format:** Sequential integer identifiers
- **Range:** 7 to 990,000,001
- **Null Values:** None (0%)
- **Unique Values:** 1,272,091 distinct events
- **Comment:** None provided
- **Usage:** Primary identifier for individual storm events; key for joining to other event tables

### location_range_miles (FLOAT64)
- **Format:** Decimal distance values
- **Range:** 0.0 to 519.78 miles
- **Null Values:** 24.57%
- **Distribution:** Includes precise measurements to 2 decimal places
- **Common Pattern:** Many events at 0.0 miles (exact location)
- **Comment:** None provided
- **Usage:** Distance metric from reference point; useful for proximity analysis

### location_index (INT64)
- **Format:** Sequential integers 1-8
- **Range:** 1 to 8
- **Null Values:** None (0%)
- **Unique Values:** 8
- **Comment:** None provided
- **Usage:** Indicates multiple location points per event; critical for proper event aggregation (part of composite key with event_id)

### location_azimuth (STRING)
- **Format:** Compass direction abbreviations
- **Null Values:** 24.57% (same as location_range_miles)
- **Unique Values:** 16 distinct directions
- **Possible Values:** E, ENE, ESE, N, NE, NNE, NNW, NW, S, SE, SSE, SSW, SW, W, WNW, WSW
- **Comment:** None provided
- **Usage:** Cardinal/intercardinal direction from reference point; pairs with location_range_miles

### location_name (STRING)
- **Format:** Place names, some with airport codes
- **Null Values:** 11.36%
- **Unique Values:** 54,319 distinct locations
- **Common Patterns:** City names, airport identifiers (e.g., "(01R)AFB GNRY RNG AL"), geographic features
- **Comment:** None provided
- **Usage:** Human-readable location identifier; good for filtering by known places

### location_latitude (FLOAT64)
- **Format:** Decimal degrees
- **Range:** -14.5551 to 97.1 (NOTE: values >90 indicate data quality issues)
- **Null Values:** 15.02%
- **Unique Values:** 182,970 distinct values
- **Precision:** Typically 4-5 decimal places
- **Comment:** None provided
- **Usage:** Standard geographic coordinate; primary for mapping and spatial queries

### location_longitude (FLOAT64)
- **Format:** Decimal degrees
- **Range:** -171.4 to 171.4689
- **Null Values:** 15.02% (matches location_latitude)
- **Unique Values:** 315,788 distinct values
- **Precision:** Typically 4-5 decimal places
- **Comment:** None provided
- **Usage:** Standard geographic coordinate; primary for mapping and spatial queries

### location_latitude_alternate (FLOAT64)
- **Format:** Large integer-like values
- **Range:** -1,433,306 to 7,030,174
- **Null Values:** 27.11%
- **Unique Values:** 183,166 distinct values
- **Pattern:** Appears to be coordinates * 100,000 (e.g., 37.12378° → 3712378.0)
- **Comment:** None provided
- **Usage:** Alternative coordinate encoding; likely for precision or legacy system compatibility

### location_longitude_alternate (FLOAT64)
- **Format:** Large integer-like values
- **Range:** -17,128,134 to 17,055,188
- **Null Values:** 27.11% (matches location_latitude_alternate)
- **Unique Values:** 316,165 distinct values
- **Pattern:** Appears to be coordinates * 100,000 (e.g., -79.8628° → 7986280.0, with sign possibly stored separately)
- **Comment:** None provided
- **Usage:** Alternative coordinate encoding; companion to location_latitude_alternate

## Query Considerations

### Good for Filtering:
- **event_yearmonth**: Temporal filtering (by year, month, or ranges)
- **event_id**: Specific event lookups
- **episode_id**: Finding all events in an episode
- **location_name**: Text-based location searches
- **location_azimuth**: Directional filtering (e.g., all northern events)

### Good for Grouping/Aggregation:
- **event_yearmonth**: Time-series analysis
- **location_azimuth**: Directional analysis
- **location_index**: Analyzing multi-point events
- **location_name**: Location-based statistics

### Potential Join Keys:
- **event_id**: Primary key for joining to main events table
- **episode_id**: For joining to episode-level data
- **Composite key (event_id, location_index)**: Unique row identifier

### Data Quality Considerations:
1. **Coordinate Validation**: Filter out latitude values >90 or <-90
2. **Null Handling**: ~24-27% of range/azimuth and alternate coordinates are NULL
3. **Coordinate Pairs**: location_latitude and location_longitude are NULL together (15.02%)
4. **Alternate Coordinates**: Different null pattern (27.11%) suggests not always populated
5. **Location Index**: Always query with location_index or use DISTINCT on event_id to avoid duplication
6. **Coordinate Systems**: Choose between standard (lat/lon) or alternate format based on precision needs

### Spatial Analysis Notes:
- Use location_latitude/longitude for standard GIS operations
- location_range_miles and location_azimuth provide polar coordinates from reference point
- Multiple location points per event suggest path or area coverage
- Consider using ST_GEOGPOINT for BigQuery spatial functions

## Keywords

storm events, weather data, geographic locations, coordinates, latitude, longitude, storm tracking, meteorological data, event locations, spatial data, weather events, NOAA, storm database, location tracking, azimuth, distance, polar coordinates, multi-point events, temporal weather data, geographic analysis, storm paths

## Table and Column Documentation

**Table Comment:** None provided

**Column Comments:** None provided for any columns