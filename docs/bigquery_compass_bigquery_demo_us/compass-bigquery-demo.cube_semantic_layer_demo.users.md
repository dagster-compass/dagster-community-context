---
columns:
- age (INT64)
- city (STRING)
- created_at (TIMESTAMP)
- first_name (STRING)
- gender (STRING)
- id (INT64)
- last_name (STRING)
- state (STRING)
schema_hash: d6646132e83e5c57cbb5aa73c8aeafd76df9e2b50873cd987eb61aafd8642916

---
# Table Summary: compass-bigquery-demo.cube_semantic_layer_demo.users

## Overall Dataset Characteristics

- **Total Rows**: 30,000 records
- **Data Quality**: Excellent - no null values present in any column
- **Primary Key**: `id` column (unique integer from 1 to 30,000)
- **Time Span**: Records span from 2017 to 2029 (includes future dates, suggesting test/demo data)
- **Geographic Coverage**: United States-focused with 35 states and 187 cities represented
- **Data Type**: User demographic and registration information

## Column Details

### id (INT64)
- **Type**: Integer, Primary Key
- **Range**: 1 to 30,000
- **Uniqueness**: 100% unique (30,000 distinct values)
- **Null Values**: None (0%)
- **Usage**: Primary identifier for each user record

### first_name (STRING)
- **Type**: Text/String
- **Uniqueness**: 200 distinct first names
- **Null Values**: None (0%)
- **Common Names**: Aaron, Abigail, Adam, Alan, Albert, Alexander, Alexis, Alice, Amanda, Amber, Betty, Austin, Kathleen, Walter, John
- **Pattern**: Standard English first names with good diversity

### last_name (STRING)
- **Type**: Text/String
- **Uniqueness**: 138 distinct last names
- **Null Values**: None (0%)
- **Common Names**: Adams, Allen, Anderson, Bailey, Baker, Bayer, Bennett, Brooks, Brown, Campbell, Kuhn, Feeney, Jackson, Ratke, Davis
- **Pattern**: Standard English surnames, relatively common pool

### gender (STRING)
- **Type**: Categorical (Binary)
- **Values**: Only 2 distinct values - "female" and "male"
- **Null Values**: None (0%)
- **Distribution**: Binary gender classification
- **Usage**: Excellent for demographic segmentation

### age (INT64)
- **Type**: Integer
- **Range**: 18 to 85 years
- **Uniqueness**: 68 distinct age values (complete coverage of range)
- **Null Values**: None (0%)
- **Distribution**: Spans full adult age spectrum
- **Usage**: Good for age-based segmentation and analysis

### city (STRING)
- **Type**: Text/String
- **Uniqueness**: 187 distinct cities
- **Null Values**: None (0%)
- **Examples**: Akron, Albany, Alexandria, Allentown, Anaheim, Anchorage, Ann Arbor, Arlington, Atlanta, Augusta, Bowling Green, Charleston, Olathe, Dayton, Hialeah, West Jordan, Grand Island
- **Pattern**: US city names

### state (STRING)
- **Type**: Categorical/Text
- **Format**: US state codes with "us-" prefix (e.g., "us-ak", "us-al", "us-az")
- **Uniqueness**: 35 distinct states
- **Null Values**: None (0%)
- **Examples**: us-oh, us-fl, us-ga, us-ut, us-ne, us-nj, us-co, us-mi, us-ak, us-al, us-az, us-ca, us-ct, us-hi, us-il
- **Usage**: Good for geographic grouping and regional analysis

### created_at (TIMESTAMP)
- **Type**: Timestamp with timezone
- **Uniqueness**: Nearly 100% unique (29,999 distinct values out of 30,000)
- **Null Values**: None (0%)
- **Time Range**: 2017-02-01 to 2029-08-13 (12+ year span)
- **Format**: YYYY-MM-DD HH:MM:SS+00:00
- **Note**: Contains future dates (beyond current date), indicating test/demo dataset
- **Usage**: Excellent for time-series analysis, cohort analysis, and temporal filtering

## Query Considerations

### Excellent Filtering Columns
- **state**: Only 35 values, perfect for geographic filtering
- **gender**: Binary field, simple demographic filtering
- **age**: Numeric range filtering (e.g., age groups, demographics)
- **created_at**: Date/time range filtering for cohort analysis

### Good Grouping/Aggregation Columns
- **state**: Regional aggregations (35 groups)
- **city**: City-level aggregations (187 groups)
- **gender**: Gender-based metrics
- **age**: Age cohort analysis (can be bucketed)
- **created_at**: Time-based aggregations (daily, monthly, yearly)

### Potential Join Keys
- **id**: Primary key for joining with other tables (e.g., orders, events, transactions)
- **Likely relationships**: This appears to be a dimension table that would join to fact tables via user_id

### Search/Lookup Columns
- **first_name** and **last_name**: User search functionality
- **city** and **state**: Geographic lookup

## Data Quality Considerations

1. **No Missing Data**: All columns have 0% null values - excellent for queries without null handling
2. **Consistent Formatting**: State codes follow consistent "us-XX" pattern
3. **Clean Integer Keys**: ID sequence is complete (1-30,000)
4. **Timestamp Precision**: All timestamps include timezone information
5. **Future Dates Present**: Queries filtering by current date may include unrealistic future registrations
6. **Name Diversity**: Moderate diversity in names (200 first names, 138 last names) suggests realistic but synthetic data

## Keywords

users table, user demographics, customer data, user registration, timestamp analysis, geographic data, US states, age demographics, gender analysis, user cohorts, created date, user profiles, dimensional data, demo data, semantic layer, BigQuery table, user attributes, geographic segmentation, temporal analysis, user analytics

## Table and Column Documentation

**Table Comment**: Not provided

**Column Comments**: None provided for any columns