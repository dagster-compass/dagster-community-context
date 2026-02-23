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

- **Total Rows**: 30,000 users
- **Data Quality**: Excellent - no null values in any column
- **Completeness**: 100% complete dataset with all fields populated
- **Time Range**: Data spans from 2019 to 2029 (includes future dates, possibly for testing/forecasting)
- **Primary Key**: `id` column (sequential integers 1-30000, all unique)
- **Data Pattern**: This appears to be a user demographic dataset with personal information and registration timestamps

## Column Details

### id (INT64)
- **Type**: Integer, Primary Key
- **Range**: 1 to 30,000 (sequential)
- **Uniqueness**: 100% unique (30,000 distinct values)
- **Null Values**: None (0%)
- **Usage**: Primary identifier for users, ideal for joins and unique record identification

### first_name (STRING)
- **Type**: Text field
- **Uniqueness**: 200 distinct names (high repetition expected)
- **Null Values**: None (0%)
- **Common Values**: Aaron, Abigail, Adam, Alan, Albert, Alexander, Alexis, Alice, Amanda, Amber
- **Pattern**: Common American first names
- **Usage**: Low selectivity for filtering, suitable for display/reporting

### last_name (STRING)
- **Type**: Text field
- **Uniqueness**: 138 distinct surnames
- **Null Values**: None (0%)
- **Common Values**: Adams, Allen, Anderson, Bailey, Baker, Bayer, Bennett, Brooks, Brown, Campbell
- **Pattern**: Common American surnames
- **Usage**: Low selectivity for filtering, suitable for display/reporting

### gender (STRING)
- **Type**: Categorical field
- **Uniqueness**: 2 values only
- **Possible Values**: 'female', 'male'
- **Null Values**: None (0%)
- **Distribution**: Appears relatively balanced based on samples
- **Usage**: Excellent for grouping, segmentation, and demographic analysis

### age (INT64)
- **Type**: Integer
- **Range**: 18 to 85 years
- **Uniqueness**: 68 distinct age values
- **Null Values**: None (0%)
- **Distribution**: Covers adult age range with good granularity
- **Usage**: Ideal for age-based filtering, bucketing, and cohort analysis

### city (STRING)
- **Type**: Text field
- **Uniqueness**: 187 distinct cities
- **Null Values**: None (0%)
- **Common Values**: Akron, Albany, Alexandria, Allentown, Anaheim, Anchorage, Ann Arbor, Arlington, Atlanta, Augusta
- **Pattern**: US cities across multiple states
- **Usage**: Good for geographic filtering and city-level aggregation

### state (STRING)
- **Type**: Text field (formatted as country-state codes)
- **Uniqueness**: 35 distinct states
- **Null Values**: None (0%)
- **Format**: 'us-{state_abbreviation}' (e.g., us-ak, us-ca, us-ct)
- **Coverage**: 35 US states represented
- **Usage**: Excellent for state-level geographic analysis, grouping, and regional filtering

### created_at (TIMESTAMP)
- **Type**: Timestamp with timezone (UTC+00:00)
- **Uniqueness**: 29,999 distinct values (nearly unique)
- **Null Values**: None (0%)
- **Time Range**: 2019-12-13 to 2029-07-13 (spans ~10 years)
- **Note**: Includes future dates (beyond current date), possibly test/forecast data
- **Usage**: Excellent for time-series analysis, cohort studies, registration trends, date filtering

## Potential Query Considerations

### Excellent for Filtering:
- **id**: Precise user lookup
- **state**: Regional filtering (35 categories)
- **gender**: Demographic segmentation (2 categories)
- **age**: Age-based filtering and range queries
- **created_at**: Time-based filtering, date ranges, cohort analysis

### Excellent for Grouping/Aggregation:
- **state**: State-level aggregations (35 groups)
- **city**: City-level analysis (187 groups)
- **gender**: Gender-based metrics (2 groups)
- **age**: Age cohort analysis, age distribution
- **created_at**: Time-based aggregations (daily, monthly, yearly trends)

### Join Considerations:
- **id**: Primary key - ideal for joining with other tables (orders, events, transactions, etc.)
- Expected relationships: This users table likely connects to fact tables through user_id foreign keys

### Data Quality Considerations:
- **No Missing Data**: All columns are 100% populated - no need for null handling
- **Future Dates Warning**: `created_at` contains dates beyond current time; queries filtering on "current" or "past" data should account for this
- **Data Distribution**: Nearly even distribution across states suggests synthetic or balanced sampling
- **Name Repetition**: Low cardinality in first_name (200) and last_name (138) means name-based queries will return many results

### Query Performance Tips:
- **Indexed Lookups**: Use `id` for fastest single-record retrieval
- **Efficient Filters**: `state`, `gender`, and `age` provide good selectivity
- **Time-Series**: `created_at` is excellent for temporal analysis but may need partitioning for large-scale queries
- **Avoid**: Filtering by names alone (low selectivity) unless combined with other criteria

## Keywords

users, customers, demographics, user data, registration, signup, gender analysis, age distribution, geographic data, US states, cities, timestamp, created date, user attributes, dimensional data, customer dimension, user profiles, personal information, BigQuery, cube semantic layer

## Table and Column Documentation

**Table Comment**: Not provided

**Column Comments**: No column-level comments provided in the analysis