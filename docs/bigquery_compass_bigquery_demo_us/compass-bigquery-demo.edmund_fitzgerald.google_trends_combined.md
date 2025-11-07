---
columns:
- date (DATE)
- keyword (STRING)
- source (STRING)
- value (FLOAT64)
schema_hash: a944d443b31cab890fcc72e7fed7569e37a8e7dad550d208c30f68ca6ff6757a

---
# Table Summary: compass-bigquery-demo.edmund_fitzgerald.google_trends_combined

## Overall Dataset Characteristics

### Dataset Size and Scope
- **Total Rows**: 8,122 records
- **Time Period**: January 2004 to January 2025 (approximately 21 years of data)
- **Temporal Granularity**: Monthly data (263 unique dates)
- **Data Quality**: Excellent - 0% null values across all columns

### General Observations
This dataset tracks Google Trends data (search interest over time) for keywords related to the Edmund Fitzgerald shipwreck and Gordon Lightfoot's famous song. The data captures both web search and YouTube search trends, providing insights into public interest in this historical maritime disaster and its cultural references.

### Notable Patterns
- **Value Distribution**: Search interest values range from 0 to 100 (standard Google Trends normalization)
- **Keyword Focus**: 10 distinct keywords covering various aspects: the ship itself, the anniversary, documentaries, the song, Gordon Lightfoot, and Lake Superior shipwrecks
- **Dual Source Tracking**: Data is split between web search and YouTube platforms, allowing for comparison of interest across media types
- **Low Average Interest**: Many 0.0 values suggest generally low search volume for these historical topics, likely with periodic spikes around anniversaries or cultural events

---

## Column Details

### 1. keyword (STRING)
**Description**: The search term being tracked in Google Trends

- **Data Type**: STRING
- **Null Values**: None (0%)
- **Cardinality**: 10 unique values (low cardinality - good for grouping)

**Complete Keyword List**:
1. Edmund Fitzgerald
2. Edmund Fitzgerald anniversary
3. Edmund Fitzgerald documentary
4. Edmund Fitzgerald shipwreck
5. Edmund Fitzgerald song
6. Gordon Lightfoot
7. Gordon Lightfoot Wreck of the Edmund Fitzgerald
8. Wreck of the Edmund Fitzgerald
9. Wreck of the Edmund Fitzgerald lyrics
10. Lake Superior shipwreck

**Analysis**: Keywords are divided into thematic categories - direct references to the ship, the song/lyrics, the artist (Gordon Lightfoot), and broader topics (shipwrecks, documentaries, anniversary). This structured keyword set allows for categorical analysis of interest types.

---

### 2. source (STRING)
**Description**: The Google Trends data source platform

- **Data Type**: STRING
- **Null Values**: None (0%)
- **Cardinality**: 2 unique values

**Values**:
- `web_search`: Traditional Google web search data
- `youtube`: YouTube search data

**Analysis**: Binary classification allows for easy comparison between search behavior on Google's main search engine versus its video platform. This is particularly relevant for a topic tied to a famous song.

---

### 3. date (DATE)
**Description**: The month for which search interest is measured

- **Data Type**: DATE
- **Null Values**: None (0%)
- **Cardinality**: 263 unique dates
- **Range**: 2004-01-01 to 2025-01-01
- **Granularity**: Monthly (first day of each month)

**Temporal Coverage**: 
- Spans 21 years of search trend data
- Monthly intervals provide good balance between granularity and data volume
- Covers period from after the 2004 anniversary through recent times

**Analysis**: The date range is comprehensive for trend analysis, covering multiple anniversaries of the 1975 sinking (which occurred on November 10, 1975). Expect seasonal patterns, particularly spikes around November.

---

### 4. value (FLOAT64)
**Description**: Google Trends search interest index (0-100 scale)

- **Data Type**: FLOAT64
- **Null Values**: None (0%)
- **Cardinality**: 72 unique values
- **Range**: 0.0 to 100.0
- **Distribution**: Heavily skewed toward lower values (many 0.0 entries)

**Value Interpretation**:
- 100 = Peak search interest for the keyword in the time period
- 0 = Very low or no search interest (below threshold)
- Values are normalized relative to the highest point for that keyword

**Analysis**: The presence of many 0.0 values indicates this is a niche topic with intermittent interest. Higher values likely correspond to anniversaries (especially major ones like 40th, 45th, 50th), documentary releases, or news events related to the shipwreck.

---

## Potential Query Considerations

### Filtering Operations
**Best Columns for WHERE Clauses**:
1. **date**: Time-based filtering (specific years, date ranges, months)
   - Filter for November data: `EXTRACT(MONTH FROM date) = 11`
   - Anniversary years: `EXTRACT(YEAR FROM date) IN (2015, 2020, 2025)` (40th, 45th, 50th)
2. **source**: Platform-specific analysis (`source = 'youtube'`)
3. **keyword**: Specific keyword tracking or category filtering
4. **value**: Interest threshold filtering (`value > 50` for high-interest periods)

### Grouping and Aggregation
**Recommended GROUP BY Columns**:
1. **keyword**: Compare interest across different search terms
2. **source**: Web vs YouTube comparison
3. **EXTRACT(YEAR FROM date)**: Yearly trends
4. **EXTRACT(MONTH FROM date)**: Seasonal patterns (expect November peaks)
5. **Combination groupings**: `keyword, source` for detailed breakdowns

**Common Aggregations**:
- `AVG(value)`: Average search interest
- `MAX(value)`: Peak interest periods
- `SUM(value)`: Total interest (with caveats about normalization)
- `COUNT(*)`: Data point coverage

### Join Keys and Relationships
**Potential Join Scenarios**:
- **Date-based joins**: Link to calendar tables, historical events, or weather data
- **Keyword joins**: Connect to keyword metadata tables (if available)
- **No obvious foreign keys**: This appears to be a standalone fact table

### Time Series Analysis Opportunities
- **Trend Analysis**: Year-over-year comparisons
- **Seasonality**: Monthly patterns (especially November spikes)
- **Event Correlation**: Major anniversaries (1975 + 10, 20, 30, 40, 50 years)
- **Platform Comparison**: Web search vs YouTube interest over time

### Data Quality Considerations

**For Accurate Queries**:
1. **Normalization Awareness**: Values are relative within each keyword's timeframe, not absolute search volumes
2. **Zero Values**: Many 0.0 values are expected for niche historical topics; they're valid data points
3. **Monthly Granularity**: Don't expect daily precision; data represents monthly aggregates
4. **Platform Differences**: web_search and youtube values aren't directly comparable (different user bases/behaviors)
5. **Recent Data**: January 2025 data may be incomplete depending on query date

**Query Best Practices**:
- Use PARTITION BY for relative comparisons within keywords
- Consider filtering out or handling 0 values depending on analysis goals
- Use date functions to identify anniversary periods
- Apply moving averages to smooth monthly volatility
- Separate analyses by source when comparing platforms

---

## Keywords

Edmund Fitzgerald, shipwreck, Google Trends, search interest, Gordon Lightfoot, Lake Superior, maritime history, search trends, time series, web search, YouTube, monthly data, search analytics, trending data, historical events, song lyrics, documentary, anniversary tracking, seasonal patterns, interest over time, search volume, trend analysis, BigQuery, public interest metrics

---

## Table and Column Documentation

**Note**: No table comments or column comments were provided in the source data. The table name `google_trends_combined` suggests this is an aggregated dataset combining multiple Google Trends exports, likely for both web search and YouTube search data related to Edmund Fitzgerald keywords.