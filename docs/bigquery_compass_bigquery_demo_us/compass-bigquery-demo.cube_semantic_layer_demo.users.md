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

## Keywords
users, user demographics, customer data, geographic data, timestamp data, user profiles, age demographics, gender data, US states, cities, user registration, created date, user IDs

## Overall Dataset Characteristics

**Total Rows:** 30,000

**General Data Quality:** Excellent - Zero null values across all columns, indicating complete and well-maintained user data.

**Notable Patterns:**
- The dataset spans approximately 12 years (2017-2029), with the latest timestamps appearing to be future-dated test data
- Geographically distributed across 35 US states and 187 cities
- Nearly complete uniqueness in `created_at` (29,999 unique values for 30,000 rows)
- All user IDs are unique, serving as natural primary keys
- Age distribution ranges from 18 to 85 years old across 68 distinct age values
- Balanced gender distribution with only two categories (male/female)

**Data Distribution:**
- Common surnames (138 unique) and first names (200 unique) suggest typical US name distributions
- State codes follow standard US postal abbreviations with "us-" prefix
- Cities represent major US metropolitan areas

## Table and Column Documentation

**Table Comment:** Not provided

**Column Comments:** Not provided

## Column Details

### id (INT64)
- **Type:** Integer, Primary Key
- **Range:** 1 to 30,000 (sequential)
- **Null Pattern:** No nulls (0%)
- **Uniqueness:** Fully unique (30,000 distinct values)
- **Purpose:** Unique identifier for each user record

### first_name (STRING)
- **Type:** Text field
- **Null Pattern:** No nulls (0%)
- **Distribution:** 200 unique names, common English first names
- **Sample Values:** Gregory, Dennis, Beverly, Kathleen, Laura, Natalie, Gerald
- **Pattern:** Standard capitalized US first names including both traditional and modern names (Aaron, Abigail, Alexander, etc.)

### last_name (STRING)
- **Type:** Text field
- **Null Pattern:** No nulls (0%)
- **Distribution:** 138 unique surnames
- **Sample Values:** Williams, Lubowitz, Reynolds, Wilson, Bennett, Carter, Muller, Wood
- **Pattern:** Common English surnames including Anglo-Saxon, German, and other Western European origins

### gender (STRING)
- **Type:** Categorical (2 values)
- **Null Pattern:** No nulls (0%)
- **Values:** "male" and "female"
- **Distribution:** Appears relatively balanced based on samples

### age (INT64)
- **Type:** Integer
- **Range:** 18 to 85 years
- **Null Pattern:** No nulls (0%)
- **Distribution:** 68 distinct age values spanning adult ages
- **Sample Values:** 47, 54, 68, 72, 81, 30
- **Pattern:** Adult age range suggesting this represents customer/user age

### city (STRING)
- **Type:** Text field
- **Null Pattern:** No nulls (0%)
- **Distribution:** 187 unique US cities
- **Sample Values:** Charleston, Kenosha, Akron, Lexington, Aurora, Eugene, Newark, North Charleston
- **Pattern:** Major and mid-sized US metropolitan areas

### state (STRING)
- **Type:** Categorical (35 values)
- **Null Pattern:** No nulls (0%)
- **Format:** "us-{state_code}" (e.g., us-ca, us-ny)
- **Distribution:** 35 US states represented
- **Sample Values:** us-mo, us-ca, us-ak, us-ky, us-il, us-or, us-nj, us-sc
- **Pattern:** Standardized state codes with "us-" prefix

### created_at (TIMESTAMP)
- **Type:** Timestamp with timezone (UTC)
- **Null Pattern:** No nulls (0%)
- **Range:** 2017-03-08 to 2029-08-19 (approximately 12-year span)
- **Uniqueness:** Nearly unique (29,999 of 30,000 records)
- **Sample Values:** 2028-03-09, 2018-05-10, 2017-08-08, 2020-12-29, 2023-12-22
- **Pattern:** User account creation timestamps; future dates suggest test/demo data

## Query Considerations

### Ideal Filtering Columns:
- **id**: Exact user lookups (primary key)
- **state**: Geographic filtering (35 distinct values make this efficient)
- **gender**: Binary filtering for demographic analysis
- **age**: Range-based filtering for age cohorts (e.g., 18-25, 26-35)
- **created_at**: Temporal filtering (cohort analysis, registration trends)
- **city**: Specific geographic markets (187 cities)

### Ideal Grouping/Aggregation Columns:
- **state**: State-level aggregations (manageable cardinality at 35)
- **gender**: Demographic breakdowns
- **age**: Age group analysis (can be bucketed)
- **city**: City-level metrics
- **created_at**: Time-series analysis (by year, month, quarter)
- **last_name**: Could be used for diversity analysis (138 values)

### Potential Join Keys:
- **id**: Primary key for joining to other user-related tables (orders, events, transactions)
- **state + city**: Geographic joins to location dimension tables
- **created_at**: Temporal joins to date/calendar dimensions

### Data Quality Considerations:

1. **Future Dates**: Queries filtering on `created_at` should be aware that dates extend into 2029, suggesting this is demo/test data
2. **No Nulls**: All columns are fully populated, so NULL handling is unnecessary
3. **Age Verification**: Age field appears to be static (not calculated from birthdate), may become stale over time
4. **State Format**: Remember "us-" prefix when filtering states
5. **Case Sensitivity**: Names are properly capitalized; queries should account for case matching
6. **Timestamp Precision**: Includes seconds and timezone information for precise temporal analysis
7. **Geographic Completeness**: Not all US states represented (35 of 50), queries assuming national coverage should be validated

### Recommended Query Patterns:

- **Cohort Analysis**: Group by date truncations of `created_at`
- **Geographic Analysis**: Group by `state` or `city`
- **Demographic Segmentation**: Combine `gender` and age ranges
- **User Lookups**: Filter by `id` for specific user details
- **Temporal Trends**: Time-series queries on registration patterns using `created_at`