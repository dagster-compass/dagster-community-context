---
columns:
- lake (STRING)
- latitude (FLOAT64)
- longitude (FLOAT64)
schema_hash: e6dbc9a41ef2ec6cea50628ee7f266c1238159a71b48b1142f674052b677f1a8

---
# Table Documentation Summary: great_lakes_coordinates_detailed

## Overall Dataset Characteristics

**Dataset Size:** 30 rows

**Purpose:** This table contains geographical coordinate data for the five Great Lakes of North America, providing latitude and longitude points that likely represent various locations across each lake (possibly shoreline points, survey locations, or other reference coordinates).

**Data Quality:** Excellent - no null values detected in any column (0% null percentage across all fields).

**Distribution Patterns:**
- Geographic coverage spans approximately 7° latitude (41.6° to 48.2° N) and 13° longitude (-89.7° to -76.3° W)
- All five Great Lakes are represented in the dataset
- Multiple coordinate pairs per lake (average ~6 points per lake based on 30 total rows for 5 lakes)
- Coordinates fall within the expected geographical boundaries of the Great Lakes region

**Table Comment:** Not provided

---

## Column Details

### 1. **latitude** (FLOAT64)
- **Data Type:** Floating-point decimal number (geographic coordinate)
- **Null Values:** None (0.00%)
- **Value Range:** 41.6° N to 48.2° N
- **Unique Values:** 23 distinct latitude values
- **Distribution Pattern:** Relatively well-distributed across the range, with some latitude values appearing multiple times (30 rows but only 23 unique values suggests 7 repeated latitude values)
- **Geographic Context:** Spans from southern Lake Erie (41.6°) to northern Lake Superior (48.2°)
- **Column Comment:** Not provided

### 2. **longitude** (FLOAT64)
- **Data Type:** Floating-point decimal number (geographic coordinate)
- **Null Values:** None (0.00%)
- **Value Range:** -89.7° W to -76.3° W
- **Unique Values:** 26 distinct longitude values
- **Distribution Pattern:** High uniqueness (26 out of 30 values are distinct), suggesting broad east-west coverage
- **Geographic Context:** Spans from western Lake Superior (-89.7°) to eastern Lake Ontario (-76.3°)
- **Column Comment:** Not provided

### 3. **lake** (STRING)
- **Data Type:** Text string (categorical)
- **Null Values:** None (0.00%)
- **Unique Values:** 5 (complete enumeration of the Great Lakes)
- **Possible Values:**
  - Lake Erie
  - Lake Huron
  - Lake Michigan
  - Lake Ontario
  - Lake Superior
- **Distribution:** Each lake has multiple coordinate points in the dataset
- **Column Comment:** Not provided

---

## Query Considerations

### Optimal Filtering Columns:
- **`lake`** - Primary categorical filter; ideal for queries focusing on specific lakes (e.g., "WHERE lake = 'Lake Superior'")
- **`latitude` / `longitude`** - Geographic range filters for bounding box queries (e.g., "WHERE latitude BETWEEN 42.0 AND 44.0")

### Aggregation/Grouping Opportunities:
- **`lake`** - Excellent GROUP BY candidate for calculating statistics per lake (e.g., average coordinates, geographic center, coordinate count per lake)
- Geographic analysis: Calculate centroid coordinates, bounding boxes, or geographic span per lake

### Potential Join Keys:
- **`lake`** - Can join with other Great Lakes-related tables (e.g., shipping data, water quality, historical records)
- **`latitude, longitude`** pair - Could join with point-based geographic data or spatial datasets

### Spatial Query Potential:
- Coordinates can be used to create GEOGRAPHY points for spatial queries in BigQuery
- Distance calculations between points
- Proximity searches (e.g., finding nearest coordinates to a specific location)

### Data Quality Considerations:
- **No missing data:** All queries can assume complete data without NULL handling
- **Coordinate precision:** Float values provide sufficient precision for most geographic analyses
- **Limited sample size:** Only 30 points total; statistical analyses should consider small sample size
- **Uneven distribution:** Unknown if points are evenly distributed per lake or weighted toward certain areas

---

## Keywords

`Great Lakes`, `coordinates`, `latitude`, `longitude`, `Lake Superior`, `Lake Michigan`, `Lake Huron`, `Lake Erie`, `Lake Ontario`, `geography`, `geospatial data`, `Edmund Fitzgerald`, `mapping`, `location data`, `North America`, `freshwater lakes`, `spatial analysis`, `GIS`, `coordinate pairs`, `geographic reference points`

---

## Table and Column Documentation

### Table Comment
*No table comment provided in the schema*

### Column Comments
- **latitude:** *No column comment provided*
- **longitude:** *No column comment provided*
- **lake:** *No column comment provided*