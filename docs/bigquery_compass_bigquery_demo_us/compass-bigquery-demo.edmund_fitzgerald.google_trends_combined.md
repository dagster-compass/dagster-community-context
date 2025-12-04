---
columns:
- date (DATE)
- keyword (STRING)
- source (STRING)
- value (FLOAT64)
schema_hash: a944d443b31cab890fcc72e7fed7569e37a8e7dad550d208c30f68ca6ff6757a

---
# Comprehensive Data Summary: compass-bigquery-demo.edmund_fitzgerald.google_trends_combined

## Overall Dataset Characteristics

**Total Rows:** 8,122

**General Description:** This table contains Google Trends data tracking search interest over time for keywords related to the Edmund Fitzgerald shipwreck, Gordon Lightfoot's famous song about the tragedy, and related topics. The data spans from 2004 to 2024, capturing approximately 20 years of search trends across both web search and YouTube platforms.

**Data Quality:** 
- Excellent completeness - 0% null values across all columns
- Clean, structured time-series data with monthly granularity
- Consistent categorical values with no apparent data quality issues
- 263 unique monthly date points indicating comprehensive temporal coverage

**Notable Patterns:**
- Dual-source tracking (web_search and youtube) allows for cross-platform trend analysis
- 10 distinct keywords focused on Edmund Fitzgerald incident and associated cultural elements
- Value range (0-100) represents normalized Google Trends interest scores
- Many zero values suggest low baseline interest with periodic spikes

## Column Details

### source (STRING)
**Data Type:** Categorical text field with 2 distinct values

**Values:**
- `web_search`: Traditional Google web search trends
- `youtube`: YouTube search/viewing trends

**Null Pattern:** No null values (0.00%)

**Distribution:** Appears balanced between both sources, enabling comparative analysis between web and video platform interest

**Usage Notes:** Key dimension for segmenting search behavior by platform type

---

### keyword (STRING)
**Data Type:** Categorical text field with 10 distinct values

**Complete Value List:**
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

**Null Pattern:** No null values (0.00%)

**Keyword Categories:**
- **Direct Event References:** "Edmund Fitzgerald", "Edmund Fitzgerald shipwreck", "Lake Superior shipwreck"
- **Time-Based Searches:** "Edmund Fitzgerald anniversary"
- **Media Content:** "Edmund Fitzgerald documentary", "Edmund Fitzgerald song"
- **Artist-Related:** "Gordon Lightfoot", "Gordon Lightfoot Wreck of the Edmund Fitzgerald"
- **Song-Specific:** "Wreck of the Edmund Fitzgerald", "Wreck of the Edmund Fitzgerald lyrics"

**Usage Notes:** Primary dimension for analyzing specific aspects of public interest

---

### date (DATE)
**Data Type:** Date field (monthly granularity)

**Temporal Coverage:**
- Earliest: 2004-01-01
- Latest: 2024 (based on sample)
- Unique Values: 263 distinct months
- ~20 years of historical data

**Null Pattern:** No null values (0.00%)

**Format:** YYYY-MM-01 (first day of each month)

**Distribution:** Monthly time series data with consistent intervals

**Usage Notes:** 
- Primary time dimension for trend analysis
- Enables seasonal pattern detection (especially November anniversary spikes)
- Suitable for time-series aggregations and moving averages

---

### value (FLOAT64)
**Data Type:** Numeric (floating-point)

**Range:** 0.0 to 100.0

**Unique Values:** 72 distinct values

**Distribution Characteristics:**
- **Lower Bound:** 0.0 (appears frequently in samples)
- **Upper Bound:** 100.0 (peak interest score)
- **Scale:** Google Trends normalized score (0-100 scale where 100 represents peak popularity)
- **Common Values:** Many records show 0.0, suggesting low baseline interest with periodic spikes

**Null Pattern:** No null values (0.00%)

**Interpretation:** 
- 100 = Peak search interest during the time period
- 50 = Half the peak search interest
- 0 = Insufficient search volume for that keyword/time combination

**Usage Notes:** Primary metric for measuring search interest intensity and trend patterns

## Table and Column Documentation

**Table Comment:** Not provided

**Column Comments:** Not provided in the source data

## Potential Query Considerations

### Ideal for Filtering:
1. **source:** Filter by platform (web_search vs youtube) for platform-specific analysis
2. **keyword:** Filter by specific topics (e.g., song-related vs documentary-related)
3. **date:** Time-range filtering (e.g., anniversary months, specific years, recent trends)
4. **value:** Threshold filtering (e.g., only periods with significant interest > 10)

### Ideal for Grouping/Aggregation:
1. **date:** 
   - Monthly trends
   - Yearly aggregations (EXTRACT(YEAR FROM date))
   - Seasonal patterns (EXTRACT(MONTH FROM date))
   - Anniversary analysis (November focus)
   
2. **source:** Platform comparison (web vs YouTube interest)

3. **keyword:** Topic popularity comparison, content type analysis

4. **Combined Dimensions:**
   - keyword + source (which topics perform better on which platform)
   - date + keyword (trending topics over time)
   - EXTRACT(MONTH FROM date) + keyword (seasonal patterns by topic)

### Potential Join Keys:
- **date:** Could join with other time-series data (weather, news events, music charts)
- **keyword:** Could join with a keyword metadata table (category, related terms)
- **source:** Could join with platform metadata or broader social media trends

### Analytical Opportunities:
1. **Anniversary Spike Analysis:** Examine November patterns when Edmund Fitzgerald sank (November 10, 1975)
2. **Platform Preference:** Compare web_search vs youtube for different content types
3. **Cultural Impact:** Track Gordon Lightfoot's song influence vs historical event interest
4. **Long-term Trends:** 20-year view of how historical event interest decays/sustains
5. **Seasonal Patterns:** Identify recurring patterns (holidays, anniversaries, cultural moments)

### Data Quality Considerations:

1. **Zero Values:** Many records have value=0, indicating:
   - Insufficient search volume for Google Trends reporting
   - Need for careful handling in visualizations and statistical calculations
   - Consider filtering WHERE value > 0 for meaningful analysis

2. **Relative Scaling:** Google Trends values are normalized (0-100):
   - Not absolute search volumes
   - Comparisons valid within same query timeframe
   - Cross-keyword comparisons should account for different baseline popularity

3. **Monthly Granularity:** 
   - Data aggregated to first day of month
   - Cannot analyze intra-month variations
   - Suitable for medium to long-term trend analysis

4. **Sample Bias:** 
   - Sample shows many 0.0 values, suggesting sporadic interest
   - Peak events (anniversaries, news coverage) likely drive most non-zero values

## Keywords

Edmund Fitzgerald, Google Trends, search trends, web search, YouTube, Gordon Lightfoot, shipwreck, Lake Superior, search interest, time series data, monthly data, trend analysis, search volume, keyword analysis, platform comparison, anniversary, documentary, song lyrics, cultural trends, historical event interest, social media analytics, 2004-2024, 20 years data, normalized search data, seasonal patterns