---
columns:
- completed_at (STRING)
- created_at (TIMESTAMP)
- id (INT64)
- status (STRING)
- user_id (INT64)
schema_hash: ac6a2575da918ecb86264db94cfd6c9748e8ab331c35d72882d341f95d4af95a

---
# Table Analysis Summary: compass-bigquery-demo.cube_semantic_layer_demo.orders

## Overall Dataset Characteristics

- **Total Rows**: 40,000
- **Data Quality**: Excellent - all columns have 0% null values at the column level
- **Time Range**: Orders span from 2016 to 2027, suggesting this includes both historical data and future projections/test data
- **Distribution**: Data appears to represent an e-commerce or order management system with order lifecycle tracking
- **Notable Pattern**: The `completed_at` field contains the string "null" rather than actual NULL values for incomplete orders, which is an important data quality consideration

## Column Details

### id (INT64) - Primary Key
- **Type**: Integer (INT64)
- **Range**: 1 to 40,000
- **Uniqueness**: 100% unique (40,000 unique values)
- **Null Pattern**: No nulls (0.00%)
- **Purpose**: Primary identifier for orders
- **Query Consideration**: Ideal for filtering specific orders, joining with other tables

### user_id (INT64) - Foreign Key
- **Type**: Integer (INT64)
- **Range**: 2 to 30,000
- **Unique Values**: 22,185 distinct users
- **Null Pattern**: No nulls (0.00%)
- **Distribution**: ~1.8 orders per user on average (40,000 orders / 22,185 users)
- **Purpose**: Links orders to customers/users
- **Query Consideration**: Excellent for grouping by customer, joining with user tables, customer segmentation analysis

### status (STRING) - Categorical
- **Type**: String
- **Null Pattern**: No nulls (0.00%)
- **Unique Values**: 4 statuses
- **Possible Values**: 
  - `completed`
  - `processing`
  - `returned`
  - `shipped`
- **Purpose**: Tracks order fulfillment stage
- **Query Consideration**: Ideal for filtering (WHERE status = 'completed'), grouping/aggregation (COUNT by status), status funnel analysis

### created_at (TIMESTAMP)
- **Type**: Timestamp with timezone
- **Null Pattern**: No nulls (0.00%)
- **Unique Values**: 39,999 (nearly unique - suggests high precision timestamps)
- **Time Range**: 2020 to 2027
- **Format**: ISO 8601 with timezone (e.g., "2020-07-26 16:14:35+00:00")
- **Purpose**: Order creation timestamp
- **Query Consideration**: Excellent for time-based filtering, date range queries, temporal analysis, trending, and time series grouping (by day/month/year)

### completed_at (STRING) - **Data Quality Issue**
- **Type**: String (not TIMESTAMP - important!)
- **Null Pattern**: 0% at column level, but contains string "null" values
- **Unique Values**: 19,863 unique values
- **Format**: ISO 8601 string format (e.g., "2016-02-21T22:24:34.000Z") OR the string "null"
- **Data Quality Issue**: Uses string literal "null" instead of actual NULL values for incomplete orders
- **Purpose**: Order completion timestamp
- **Query Consideration**: 
  - Requires string comparison (`completed_at != 'null'` or `completed_at = 'null'`)
  - Cannot use IS NULL / IS NOT NULL operators
  - May need CAST/PARSE for date operations
  - Should filter out "null" strings for completion time analysis

## Potential Query Considerations

### Good for Filtering:
- **status**: Filter by order stage (e.g., `WHERE status = 'completed'`)
- **id**: Filter specific orders
- **created_at**: Date range filters (e.g., `WHERE created_at >= '2024-01-01'`)
- **completed_at**: Filter completed orders (`WHERE completed_at != 'null'`)
- **user_id**: Filter orders for specific customers

### Good for Grouping/Aggregation:
- **status**: Count/sum by order status, conversion funnel metrics
- **user_id**: Customer-level metrics (orders per customer, customer segmentation)
- **created_at**: Time-based aggregations (daily/monthly order counts, trends)
- **DATE(created_at)**: Group by day/month/year for time series analysis

### Potential Join Keys:
- **user_id**: Primary join key to user/customer dimension tables
- **id**: Join to order line items, order details, payments tables

### Data Quality Considerations:

1. **completed_at String Literal Issue**: 
   - Must use `completed_at != 'null'` instead of `IS NOT NULL`
   - Cannot directly perform date operations without parsing
   - Approximately 50% of orders have actual completion dates (19,863 unique values vs 40,000 rows)

2. **Future Dates Present**:
   - Data extends to 2027, suggesting test/synthetic data or future-dated orders
   - May need to filter for realistic date ranges depending on use case

3. **Status-Completion Consistency**:
   - Orders with status='completed' should have non-"null" completed_at values
   - Orders with status='processing' or 'shipped' likely have completed_at='null'
   - Should validate this relationship in queries

### Example Query Patterns:

```sql
-- Completed orders only
WHERE status = 'completed' AND completed_at != 'null'

-- Orders by month
GROUP BY DATE_TRUNC(created_at, MONTH)

-- Customer order counts
GROUP BY user_id

-- Current year orders (adjust year as needed)
WHERE EXTRACT(YEAR FROM created_at) = 2024
```

## Keywords

e-commerce, orders, order management, order status, fulfillment, customer orders, transactions, order lifecycle, completed orders, shipped orders, processing orders, returned orders, order tracking, user orders, customer transactions, order timestamps, order completion, order creation, BigQuery semantic layer, Cube demo data, time series orders, order funnel, order analytics

## Table and Column Docs

**Table Comment**: Not provided

**Column Comments**: Not provided

---

**Critical Note**: The `completed_at` field storing string "null" instead of proper NULL values is the most significant data quality consideration and will require special handling in all SQL queries involving order completion status.