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

- **Total Rows**: 40,000 records
- **Data Quality**: High quality with no null values in critical identifier and timestamp columns
- **Date Range**: Spans from 2017 to 2027, indicating historical data with future dates (possibly test data or projections)
- **Primary Key**: `id` column (unique for all 40,000 rows, sequential from 1 to 40,000)
- **Distribution Pattern**: Near-complete uniqueness in created_at timestamps suggests fine-grained order tracking
- **Notable Observation**: The `completed_at` column contains string "null" values rather than SQL NULL, requiring special handling in queries

## Column Details

### id (INT64)
- **Type**: Integer, Primary Key
- **Range**: 1 to 40,000 (sequential)
- **Nulls**: 0%
- **Unique Values**: 40,000 (100% unique)
- **Usage**: Unique order identifier, ideal for counting distinct orders and joining with order details/line items tables

### created_at (TIMESTAMP)
- **Type**: Timestamp with timezone (UTC +00:00)
- **Nulls**: 0%
- **Unique Values**: 39,999 (nearly 100% unique - one duplicate timestamp)
- **Date Range**: 2017-08-15 to 2027-01-14
- **Format**: Standard SQL timestamp with timezone
- **Usage**: Excellent for time-based filtering, date aggregations, time series analysis, and cohort analysis

### status (STRING)
- **Type**: Categorical string
- **Nulls**: 0%
- **Unique Values**: 4 distinct statuses
- **Possible Values**: 
  - `completed`
  - `processing`
  - `returned`
  - `shipped`
- **Distribution**: Relatively balanced across categories based on samples
- **Usage**: Primary column for order status filtering, grouping by order state, and funnel analysis

### user_id (INT64)
- **Type**: Integer, Foreign Key
- **Range**: 2 to 30,000
- **Nulls**: 0%
- **Unique Values**: 22,185 distinct users
- **Average Orders per User**: ~1.8 orders per user (40,000 orders / 22,185 users)
- **Usage**: Join key to users/customers table, user-level aggregations, repeat customer analysis

### completed_at (STRING)
- **Type**: String (ISO 8601 datetime format or literal "null")
- **Nulls**: 0% SQL NULL, but contains string "null" values
- **Unique Values**: 19,863 distinct values
- **Format**: ISO 8601 string format "YYYY-MM-DDTHH:MM:SS.sssZ" or "null"
- **Data Quality Issue**: Stored as STRING instead of TIMESTAMP, with string literal "null" for missing values
- **Completion Rate**: Approximately 49.7% of orders have completion dates (19,863 / 40,000)
- **Usage**: Requires type conversion (PARSE_TIMESTAMP) and null handling (WHERE completed_at != 'null') for time-based analysis

## Query Considerations

### Excellent for Filtering
- **created_at**: Time-based filters (date ranges, specific years/months/days)
- **status**: Order state filtering (completed orders, active orders, returns)
- **user_id**: Customer-specific order history
- **id**: Specific order lookups

### Excellent for Grouping/Aggregation
- **status**: Count orders by status, status distribution
- **created_at**: Time-series aggregations (daily/monthly/yearly order counts)
- **user_id**: Customer-level metrics (orders per customer, repeat customers)
- Date extractions from created_at: Year, month, quarter, day of week for seasonality analysis

### Potential Join Keys
- **id**: Primary key for joining with order_items, order_details, shipments tables
- **user_id**: Foreign key to join with users/customers dimension table

### Data Quality Considerations

1. **completed_at String Issue**: 
   - Must use `completed_at != 'null'` instead of `IS NOT NULL`
   - Requires `PARSE_TIMESTAMP('%Y-%m-%dT%H:%M:%S.%fZ', completed_at)` for timestamp operations
   - Consider creating a view with proper TIMESTAMP casting

2. **Future Dates**: 
   - Data extends to 2027, may need filtering for historical analysis
   - Could indicate test data, forecasts, or scheduled orders

3. **Status Completeness**:
   - Only orders with `status = 'completed'` should have non-null completed_at values
   - Validate this relationship for data integrity

4. **User Distribution**:
   - 22,185 unique users with 40,000 orders suggests some repeat customers
   - Useful for customer lifetime value and retention analysis

### Recommended Query Patterns

```sql
-- Time-based analysis (handle created_at)
WHERE DATE(created_at) BETWEEN '2020-01-01' AND '2023-12-31'
GROUP BY DATE_TRUNC(created_at, MONTH)

-- Status filtering
WHERE status IN ('completed', 'shipped')

-- Completed orders only (handle string null)
WHERE status = 'completed' AND completed_at != 'null'

-- Calculate completion time
SELECT 
  TIMESTAMP_DIFF(
    PARSE_TIMESTAMP('%Y-%m-%dT%H:%M:%S.%fZ', completed_at),
    created_at,
    DAY
  ) as days_to_complete
WHERE completed_at != 'null'

-- Repeat customers
SELECT user_id, COUNT(*) as order_count
GROUP BY user_id
HAVING COUNT(*) > 1
```

## Keywords

order management, e-commerce orders, order status, order tracking, order lifecycle, order completion, user orders, customer orders, order history, order analytics, order metrics, transaction data, sales orders, order fulfillment, order processing, timestamp analysis, time series data, customer behavior, repeat purchases, order funnel, BigQuery orders, semantic layer, cube orders table

## Table and Column Documentation

**Table Comment**: Not provided

**Column Comments**: Not provided