---
columns:
- date (DATE)
- keyword (STRING)
- source (STRING)
- value (FLOAT64)
schema_hash: a944d443b31cab890fcc72e7fed7569e37a8e7dad550d208c30f68ca6ff6757a

---
# Table Summary: google_trends_combined

## Overall Dataset Characteristics

**Total Rows:** 8,122

**General Description:** This table contains Google Trends data tracking search interest over time for various keywords related to the Edmund Fitzgerald shipwreck and Gordon Lightfoot's famous song about it. The data spans approximately 263 months (roughly 22 years, from 2004 onwards based on sample dates) and tracks 10 different related keywords across two search platforms (web search and YouTube).

**Data Quality:** Excellent - no null values detected in any column. The data appears clean and well-structured.

**Notable Patterns:**
- Data is collected monthly (first day of each month)
- Values range from 0-100, following Google Trends' normalized scoring system
- Many records show 0 value, indicating low or no search interest for certain keyword/date/source combinations
- The dataset tracks both general searches (Edmund Fitzgerald) and specific aspects (anniversary, song lyrics, documentary)

## Column Details

### source (STRING)
- **Type:** Categorical identifier
- **Null Values:** None (0.00%)
- **Distinct Values:** 2
- **Values:** `web_search`, `youtube`
- **Purpose:** Differentiates between Google web search trends and YouTube search trends
- **Query Consideration:** Primary dimension for comparing search behavior across platforms

### date (DATE)
- **Type:** Temporal (monthly granularity)
- **Null Values:** None (0.00%)
- **Distinct Values:** 263 unique months
- **Date Range:** Starting from 2004-01-01 (based on possible values), with samples showing dates through 2025-11-01
- **Format:** YYYY-MM-DD (always the 1st of the month)
- **Pattern:** Monthly time series data spanning ~21+ years
- **Query Consideration:** 
  - Excellent for time-series analysis and trend visualization
  - Can be used for temporal filtering (specific years, months, date ranges)
  - Suitable for seasonal/cyclical pattern analysis (e.g., November anniversary spikes)

### keyword (STRING)
- **Type:** Categorical text
- **Null Values:** None (0.00%)
- **Distinct Values:** 10 unique search terms
- **Categories:**
  - Direct shipwreck references: "Edmund Fitzgerald", "Edmund Fitzgerald shipwreck", "Lake Superior shipwreck", "Edmund Fitzgerald anniversary", "Edmund Fitzgerald documentary"
  - Song-related: "Wreck of the Edmund Fitzgerald", "Wreck of the Edmund Fitzgerald lyrics", "Gordon Lightfoot Wreck of the Edmund Fitzgerald"
  - Artist: "Gordon Lightfoot"
  - Combined: "Edmund Fitzgerald song"
- **Query Consideration:** 
  - Can group keywords into categories (shipwreck vs. song-related)
  - Useful for comparing interest in different aspects of the story
  - Good for keyword-specific filtering

### value (FLOAT64)
- **Type:** Numeric (Google Trends normalized score)
- **Null Values:** None (0.00%)
- **Range:** 0.0 to 100.0
- **Distinct Values:** 72 unique values
- **Distribution:** Many zero values (indicating low/no search interest), with values ranging up to 100 (peak interest)
- **Interpretation:** Google Trends scores represent relative search interest (100 = peak popularity in the dataset)
- **Query Consideration:**
  - Primary metric for aggregation (AVG, SUM, MAX, MIN)
  - Useful for identifying peaks and trends
  - Can filter for significant interest (e.g., value > 10)
  - Zero values are meaningful (no search interest), not missing data

## Potential Query Considerations

### Good Filtering Columns:
- **date**: For time-range queries, seasonal analysis, specific event periods
- **source**: To compare web vs. YouTube search behavior
- **keyword**: To focus on specific search terms or categories
- **value**: To find high-interest periods (e.g., WHERE value > 50)

### Good Grouping/Aggregation Columns:
- **date**: Time-series aggregations (by year, month, quarter)
- **source**: Compare trends across platforms
- **keyword**: Aggregate interest across search terms
- **Combinations**: GROUP BY date, source / GROUP BY keyword, source

### Potential Analysis Queries:
1. **Temporal trends**: Track search interest over time for specific keywords
2. **Seasonal patterns**: Identify anniversary spikes (likely November, when the ship sank)
3. **Platform comparison**: Web search vs. YouTube interest
4. **Keyword comparison**: Which aspects (song vs. shipwreck) generate more interest
5. **Peak detection**: Identify dates with highest search interest
6. **Correlation analysis**: Relationship between different keywords

### Data Quality Considerations:
- **Zero values are meaningful**: Represent actual low interest, not missing data
- **Normalized scoring**: Values are relative within the dataset, not absolute search volumes
- **Monthly granularity**: Cannot analyze daily or weekly patterns
- **Platform differences**: Web and YouTube trends may follow different patterns

### Potential Join Keys:
- **date**: Could join with other time-series data (news events, weather data, Gordon Lightfoot album releases)
- **keyword**: Could join with search term taxonomy or categorization tables
- No obvious primary key; composite key would be (source, date, keyword)

## Keywords
Edmund Fitzgerald, shipwreck, Google Trends, search interest, Gordon Lightfoot, Lake Superior, time series, web search, YouTube, historical events, maritime disaster, song lyrics, search analytics, temporal data, trend analysis

## Table and Column Documentation

**Table Comment:** Not provided

**Column Comments:** 
- source: No comment provided
- date: No comment provided
- keyword: No comment provided
- value: No comment provided