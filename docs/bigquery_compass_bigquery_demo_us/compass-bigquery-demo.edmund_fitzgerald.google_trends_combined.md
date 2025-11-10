---
columns:
- date (DATE)
- keyword (STRING)
- source (STRING)
- value (FLOAT64)
schema_hash: a944d443b31cab890fcc72e7fed7569e37a8e7dad550d208c30f68ca6ff6757a

---
# Data Summary: google_trends_combined Table

## Overall Dataset Characteristics

### Basic Statistics
- **Total Rows**: 8,122 records
- **Time Period**: Spans from 2004 to 2024 (approximately 20 years)
- **Data Granularity**: Monthly aggregated data (263 unique months)
- **Data Quality**: Excellent - 0% null values across all columns

### General Observations
- This dataset tracks Google Trends data for Edmund Fitzgerald-related search terms
- Data is split between two source platforms: web search and YouTube
- The dataset combines 10 different keyword variations related to the Edmund Fitzgerald shipwreck, Gordon Lightfoot's famous song, and related topics
- Value metric appears to be normalized on a 0-100 scale (typical for Google Trends relative popularity scores)
- Data shows strong temporal patterns with monthly granularity

---

## Column Details

### 1. keyword (STRING)
- **Purpose**: Categorizes the specific search term being tracked
- **Null Rate**: 0% (complete data)
- **Cardinality**: 10 unique keywords
- **Value Categories**:
  - Direct Edmund Fitzgerald references: "Edmund Fitzgerald", "Edmund Fitzgerald anniversary", "Edmund Fitzgerald documentary", "Edmund Fitzgerald shipwreck", "Edmund Fitzgerald song"
  - Gordon Lightfoot/Song related: "Gordon Lightfoot", "Gordon Lightfoot Wreck of the Edmund Fitzgerald", "Wreck of the Edmund Fitzgerald", "Wreck of the Edmund Fitzgerald lyrics"
  - General topic: "Lake Superior shipwreck"
- **Query Consideration**: Excellent for grouping and filtering; natural dimension for analysis

### 2. date (DATE)
- **Purpose**: Time dimension representing the month of measurement
- **Null Rate**: 0% (complete data)
- **Cardinality**: 263 unique months
- **Time Range**: 2004-01-01 to approximately 2024
- **Format**: First day of each month (e.g., 2004-01-01, 2004-02-01)
- **Pattern**: Regular monthly intervals with no gaps
- **Query Consideration**: Primary time dimension for time-series analysis, filtering, and trend identification

### 3. source (STRING)
- **Purpose**: Identifies the Google platform where searches occurred
- **Null Rate**: 0% (complete data)
- **Cardinality**: 2 unique values
- **Values**:
  - "web_search": Traditional Google web search
  - "youtube": YouTube platform searches
- **Distribution**: Binary split across the dataset
- **Query Consideration**: Key dimension for comparing search behavior across platforms

### 4. value (FLOAT64)
- **Purpose**: Represents normalized search interest/popularity score
- **Null Rate**: 0% (complete data)
- **Cardinality**: 72 unique values
- **Range**: 0.0 to 100.0
- **Distribution**: 
  - Includes 0.0 (no/minimal interest)
  - Maximum of 100.0 (peak interest)
  - Discrete values (likely integers stored as floats)
- **Interpretation**: Google Trends relative popularity metric where 100 represents peak popularity
- **Query Consideration**: Primary metric for aggregation (SUM, AVG, MAX, MIN); useful for trending and comparison analysis

---

## Potential Query Considerations

### Filtering Opportunities
1. **Time-based filtering**:
   - Filter by specific years or date ranges
   - Identify anniversary periods (November, when the Edmund Fitzgerald sank in 1975)
   - Compare different time periods (e.g., pre-2010 vs post-2010)

2. **Keyword filtering**:
   - Focus on song-related vs shipwreck-related terms
   - Compare Gordon Lightfoot searches vs direct Edmund Fitzgerald searches
   - Isolate specific search intents (documentary, lyrics, anniversary)

3. **Source filtering**:
   - Separate web search behavior from YouTube search behavior
   - Platform-specific trend analysis

### Grouping/Aggregation Opportunities
1. **Temporal aggregations**: 
   - Monthly trends (already at monthly grain)
   - Yearly aggregations for long-term patterns
   - Seasonal patterns (month of year)

2. **Categorical groupings**:
   - By keyword to compare popularity of different terms
   - By source to compare platform engagement
   - Combined keyword + source for detailed breakdowns

3. **Metric aggregations**:
   - Average interest over time periods
   - Peak interest identification (MAX)
   - Total accumulated interest (SUM)

### Join Keys & Relationships
- **No explicit foreign keys present**, but potential relationships include:
  - Could join with date dimension tables for enhanced time analysis
  - Could join with external events table (e.g., Gordon Lightfoot news, anniversary events)
  - Could correlate with weather/shipping data from Lake Superior

### Data Quality Considerations for Queries
1. **Strengths**:
   - Complete data (no nulls)
   - Consistent time granularity
   - Standardized value scale

2. **Limitations**:
   - Value 0.0 appears frequently, indicating low/no search volume periods
   - Relative scale (0-100) means absolute search volumes are unknown
   - Data is normalized within each keyword/source combination

3. **Query Best Practices**:
   - When comparing keywords, be aware that each may have different normalization baselines
   - Consider filtering out zero values for certain analyses
   - Use EXTRACT functions for date-based grouping
   - Apply CASE statements to categorize keywords into broader themes

---

## Keywords

Edmund Fitzgerald, Google Trends, search volume, time series, Gordon Lightfoot, shipwreck, Lake Superior, YouTube search, web search, keyword analysis, search trends, popularity metrics, monthly data, 2004-2024, disaster history, maritime history, song lyrics, documentary, anniversary trends, seasonal patterns

---

## Table and Column Documentation

**Note**: No table comment or column comments were provided in the source data analysis report.