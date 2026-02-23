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
# Summary Documentation: stormevents_locations Table

## Overall Dataset Characteristics

**Total Rows:** 1,742,275

**General Description:** This table contains location data for storm events, with multiple location points per event (indicated by `location_index` 1-8). The dataset spans from June 1972 to May 2025 (based on `event_yearmonth` range), providing comprehensive geographic tracking of storm event locations across what appears to be primarily US weather data.

**Data Quality Observations:**
- High data completeness for core identifiers (event_id, episode_id, event_yearmonth, location_index all 100% populated)
- Significant null values in location details: ~11% for location names, ~15% for coordinates, ~25% for directional/range data, and ~27% for alternate coordinate formats
- The presence of 8 location indices per event suggests detailed path or multi-point tracking of storm events
- Some coordinate anomalies exist (latitude range includes values like 97.1, longitude includes values outside standard ranges)

**Notable Patterns:**
- 317,600 unique episodes containing 1,272,091 unique events, indicating multiple events per episode
- Location coordinates appear in two formats: standard decimal degrees and an "alternate" format that may represent a different coordinate system or encoding
- Azimuth data uses 16-point compass directions (N, NE, ENE, E, ESE, etc.)

## Column Details

### Identifier Columns

**location_index** (INT64)
- Purpose: Sequential location point identifier (1-8) for each event
- Data Quality: 100% populated
- Values: Always between 1 and 8
- Usage: Indicates multiple location points per storm event; essential for ordering location sequences

**episode_id** (INT64)
- Purpose: Groups related weather events into episodes
- Data Quality: 100% populated
- Range: 2 to 990,000,001
- Cardinality: 317,600 unique episodes
- Usage: Primary grouping key for related storm events

**event_id** (INT64)
- Purpose: Unique identifier for individual storm events
- Data Quality: 100% populated
- Range: 7 to 990,000,001
- Cardinality: 1,272,091 unique events
- Usage: Primary key for individual events; multiple location points share same event_id

**event_yearmonth** (INT64)
- Purpose: Temporal identifier in YYYYMM format
- Data Quality: 100% populated
- Range: 197206 (June 1972) to 202505 (May 2025)
- Cardinality: 354 unique year-month combinations
- Usage: Ideal for temporal filtering and time-series analysis

### Location Identification

**location_name** (STRING)
- Purpose: Named location or landmark near the event
- Null Rate: 11.36%
- Cardinality: 54,319 unique names
- Format: Includes cities, airports (with codes like (01R)AFB GNRY RNG AL), landmarks
- Usage: Human-readable location reference; good for place-name filtering

**location_azimuth** (STRING)
- Purpose: Compass direction from named location
- Null Rate: 24.57%
- Values: 16-point compass (N, NE, ENE, E, ESE, SE, SSE, S, SSW, SW, WSW, W, WNW, NW, NNW)
- Usage: Combined with `location_range_miles` to describe position relative to named location

**location_range_miles** (FLOAT64)
- Purpose: Distance in miles from named location
- Null Rate: 24.57% (matches azimuth null rate)
- Range: 0.0 to 519.78 miles
- Precision: Up to 2 decimal places
- Usage: Distance measurement for relative positioning

### Coordinate Data - Standard Format

**location_latitude** (FLOAT64)
- Purpose: Latitude in decimal degrees
- Null Rate: 15.02%
- Range: -14.5551 to 97.1 (contains anomalies; normal range should be -90 to 90)
- Cardinality: 182,970 unique values
- Data Quality Note: Values >90 indicate data quality issues
- Usage: Primary coordinate for geospatial queries

**location_longitude** (FLOAT64)
- Purpose: Longitude in decimal degrees
- Null Rate: 15.02% (matches latitude)
- Range: -171.4 to 171.4689
- Cardinality: 315,788 unique values
- Usage: Primary coordinate for geospatial queries; appears more reliable than latitude

### Coordinate Data - Alternate Format

**location_latitude_alternate** (FLOAT64)
- Purpose: Alternative latitude encoding
- Null Rate: 27.11%
- Range: -1,433,306.0 to 7,030,174.0
- Format: Appears to be degrees/minutes/seconds packed into integer-like format (e.g., 3756130.0 = 37°56'13.0")
- Usage: May be needed for legacy system compatibility or specific calculations

**location_longitude_alternate** (FLOAT64)
- Purpose: Alternative longitude encoding
- Null Rate: 27.11% (matches alternate latitude)
- Range: -17,128,134.0 to 17,055,188.0
- Format: Similar packed DMS format as latitude alternate
- Usage: Companion to latitude_alternate

## Query Considerations

### Recommended Filtering Columns
- **event_yearmonth**: Excellent for temporal filtering; indexed format makes range queries efficient
- **episode_id** / **event_id**: Primary keys for specific event lookup
- **location_name**: When searching for events near known locations
- **location_latitude** / **location_longitude**: For bounding box or radius searches (but check for data quality)

### Recommended Grouping/Aggregation
- **event_yearmonth**: Time-series analysis by month/year
- **episode_id**: Aggregating multiple events within an episode
- **location_name**: Event counts by location
- **location_azimuth**: Directional analysis of storm patterns
- **location_index**: Analyzing event paths (start, middle, end points)

### Potential Join Keys
- **event_id**: Primary key for joining to main storm events table
- **episode_id**: For joining episode-level data
- **event_yearmonth**: Could join to temporal dimension tables

### Data Quality Considerations for Queries

1. **Null Handling Strategy:**
   - Location details (~25% null) vs coordinates (~15% null) have different completeness
   - Queries requiring precise coordinates should filter WHERE location_latitude IS NOT NULL
   - Alternate coordinates are even more sparse (~27% null)

2. **Coordinate Validation:**
   - Filter latitude values: WHERE location_latitude BETWEEN -90 AND 90
   - Longitude appears cleaner but validate range: WHERE location_longitude BETWEEN -180 AND 180

3. **Multi-location Events:**
   - Many events have multiple location points (location_index 1-8)
   - Consider whether to use all points, just first/last, or aggregate center
   - Use PARTITION BY event_id ORDER BY location_index for path analysis

4. **Temporal Considerations:**
   - 50+ years of data; older data may have different quality/completeness
   - Consider filtering recent years for higher quality: WHERE event_yearmonth >= 200001

5. **Coordinate System Selection:**
   - Standard lat/long (~15% null) vs alternate format (~27% null)
   - Standard format recommended unless specific need for alternate encoding

## Keywords

storm events, weather data, location tracking, geographic coordinates, latitude, longitude, NOAA, meteorological data, storm path, event locations, temporal weather data, compass directions, azimuth, geospatial analysis, weather episodes, multi-point tracking, DMS coordinates, decimal degrees, US weather, storm tracking, location index, event sequences

## Table and Column Documentation

**Table Comment:** Not provided in the analysis report.

**Column Comments:** No specific column comments were provided in the analysis report. The column purposes and characteristics described above are derived from data analysis rather than explicit documentation.