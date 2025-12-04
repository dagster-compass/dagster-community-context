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

- **Total Rows**: 1,742,275 records
- **Dataset Type**: Storm event location data spanning from June 1972 to May 2025 (event_yearmonth: 197206-202505)
- **Temporal Coverage**: 354 unique year-month combinations over approximately 53 years
- **Event Scale**: Tracks 1,272,091 unique events across 317,600 episodes
- **Location Granularity**: Up to 8 location points per event (location_index 1-8)
- **Data Quality**: Generally good, with most critical identifiers having 100% completeness. Location attributes show varying degrees of completeness (11-27% null rates for optional fields)

## Column Details

### Identifier Columns

**location_index** (INT64)
- Purpose: Sequential identifier for multiple locations within a single event
- Values: 1 through 8 (discrete)
- Complete: 100% populated
- Usage: Indicates ordering of location points for storm events that affect multiple areas
- Query consideration: Good for filtering specific location sequences or counting locations per event

**episode_id** (INT64)
- Purpose: Groups related storm events into episodes
- Range: 2 to 990,000,001
- Cardinality: 317,600 unique episodes
- Complete: 100% populated
- Usage: Primary grouping key for related storm events
- Query consideration: Excellent for aggregating multiple related events

**event_id** (INT64)
- Purpose: Unique identifier for individual storm events
- Range: 7 to 990,000,001
- Cardinality: 1,272,091 unique events
- Complete: 100% populated
- Usage: Primary key for individual storm occurrences
- Query consideration: Key join column; ~4 locations per event on average (1.37:1 ratio)

### Temporal Column

**event_yearmonth** (INT64)
- Format: YYYYMM (e.g., 201906 = June 2019)
- Range: 197206 (June 1972) to 202505 (May 2025)
- Cardinality: 354 unique months
- Complete: 100% populated
- Usage: Time-based filtering and temporal analysis
- Query consideration: Excellent partition/filter column; consider extracting year and month separately for analysis

### Directional Location Attributes

**location_azimuth** (STRING)
- Purpose: Compass direction from reference point
- Values: 16 cardinal/intercardinal directions (N, NE, ENE, E, ESE, SE, SSE, S, SSW, SW, WSW, W, WNW, NW, NNW, NNE)
- Null Rate: 24.57% (optional attribute)
- Usage: Indicates direction of storm location relative to named reference point
- Query consideration: Good for geographic/directional analysis when paired with location_range_miles

**location_range_miles** (FLOAT64)
- Purpose: Distance from reference location in miles
- Range: 0.0 to 519.78 miles
- Cardinality: 5,674 unique values
- Null Rate: 24.57% (matches azimuth nulls)
- Pattern: Many events at 0.0 miles (direct hits on named locations)
- Usage: Combined with azimuth for relative positioning
- Query consideration: Filter for proximity analysis; nulls indicate absolute location rather than relative

**location_name** (STRING)
- Purpose: Named reference point (cities, airports, landmarks)
- Cardinality: 54,319 unique location names
- Null Rate: 11.36%
- Examples: Cities (OWENSBORO, HUDSON), Airports ((1K5)ELKHART), Landmarks (FT ROSS)
- Usage: Human-readable location identifier
- Query consideration: Good for filtering by known locations; case-sensitive string matching

### Absolute Coordinate Columns

**location_latitude** (FLOAT64)
- Purpose: Geographic latitude in decimal degrees
- Range: -14.5551 to 97.1 (note: 97.1 appears to be an error; valid range should be -90 to 90)
- Cardinality: 182,970 unique values
- Null Rate: 15.02%
- Usage: Primary latitude coordinate
- Query consideration: Data quality issue with values >90; filter for valid range (-90 to 90) in queries

**location_longitude** (FLOAT64)
- Purpose: Geographic longitude in decimal degrees
- Range: -171.4 to 171.4689
- Cardinality: 315,788 unique values
- Null Rate: 15.02% (matches latitude)
- Usage: Primary longitude coordinate
- Query consideration: Valid range; pair with latitude for spatial queries

**location_latitude_alternate** (FLOAT64)
- Purpose: Alternative latitude encoding (appears to be degrees-minutes format: DDMMSS)
- Range: -1,433,306 to 7,030,174
- Cardinality: 183,166 unique values
- Null Rate: 27.11%
- Example: 3746200.0 = 37°46'20.0" N
- Usage: Alternative coordinate representation
- Query consideration: Requires conversion formula; higher null rate than primary coordinates

**location_longitude_alternate** (FLOAT64)
- Purpose: Alternative longitude encoding (degrees-minutes format: DDDMMSS)
- Range: -17,128,134 to 17,055,188
- Cardinality: 316,165 unique values
- Null Rate: 27.11% (matches alternate latitude)
- Example: 878298.0 = 87°82'98.0" W (note: seconds >60 suggests data quality issues)
- Usage: Alternative coordinate representation
- Query consideration: Complex conversion needed; prefer primary coordinates

## Potential Query Considerations

### Filtering Columns
- **event_yearmonth**: Excellent for temporal filtering; partition-friendly
- **episode_id/event_id**: Specific event lookup
- **location_name**: Known location filtering
- **location_latitude/longitude**: Geographic bounding box queries
- **location_azimuth**: Directional filtering
- **location_index**: Filter for specific location sequences

### Grouping/Aggregation Columns
- **event_yearmonth**: Temporal aggregation (monthly, yearly trends)
- **episode_id**: Group related events
- **location_name**: Location-based statistics
- **location_azimuth**: Directional distribution analysis
- **location_index**: Count locations per event

### Join Keys
- **event_id**: Primary key for joining with other storm event tables
- **episode_id**: Join to episode-level data
- **event_yearmonth**: Time-based joins

### Data Quality Considerations
1. **Coordinate Validation**: Filter location_latitude between -90 and 90 (outliers exist)
2. **Null Handling**: ~25% of directional attributes (azimuth/range) are null; ~15% of primary coordinates are null; ~27% of alternate coordinates are null
3. **Alternate Coordinates**: Complex format requiring conversion; prefer primary lat/long
4. **Location Multiplicity**: Events can have 1-8 locations; be aware when counting
5. **Date Range**: Data spans 1972-2025, consider temporal data quality variations
6. **Location Names**: May contain special characters and formatting (airport codes, etc.)

### Recommended Query Patterns
- Use primary lat/long for spatial analysis
- Filter event_yearmonth for time ranges
- Join on event_id for detailed event information
- Group by episode_id for event cluster analysis
- Use location_name with LIKE for flexible location matching
- Calculate distance/direction when both azimuth and range are non-null

## Keywords

storm events, weather data, NOAA, severe weather, geographic locations, coordinates, latitude, longitude, episodes, temporal data, location tracking, event locations, storm tracking, weather database, US storms, cardinal directions, azimuth, distance, range, 1972-2025, time series, spatial data, BigQuery, multi-location events, storm paths, weather episodes

## Table and Column Documentation

**Table Comment**: Not provided

**Column Comments**: Not provided