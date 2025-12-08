---
columns:
- completed_at (STRING)
- created_at (TIMESTAMP)
- id (INT64)
- status (STRING)
- user_id (INT64)
schema_hash: ac6a2575da918ecb86264db94cfd6c9748e8ab331c35d72882d341f95d4af95a

---
# Table Summary: compass-bigquery-demo.cube_semantic_layer_demo.orders

## Overall Dataset Characteristics

- **Total Rows**: 40,000 orders
- **Data Quality**: High quality with no null values in critical fields (status, created_at, user_id, id)
- **Time Span**: Orders span from 2017 to 2029, suggesting this includes both historical and projected/future data
- **Distribution**: 
  - 4 distinct order statuses with relatively balanced distribution
  - 22,185 unique users placing 40,000 orders (average ~1.8 orders per user)
  - Near-unique created_at timestamps (39,999 unique values for 40,000 rows)
  - Only ~50% of orders have completion dates (19,863 non-null completed_at values)

## Column Details

### **id** (INT64)
- **Type**: Primary key / unique order identifier
- **Range**: 1 to 40,000
- **Nulls**: None (0%)
- **Uniqueness**: 100% unique
- **Use Case**: Primary key for joins, filtering specific orders

### **user_id** (INT64)
- **Type**: Foreign key linking to users/customers
- **Range**: 2 to 30,000
- **Nulls**: None (0%)
- **Uniqueness**: 22,185 unique users
- **Use Case**: Foreign key for joins, grouping by customer, filtering by user

### **status** (STRING)
- **Type**: Categorical string
- **Values**: 4 distinct statuses
  - `completed`
  - `processing`
  - `returned`
  - `shipped`
- **Nulls**: None (0%)
- **Distribution**: ~25% distribution per status
- **Use Case**: Excellent for filtering, grouping, and aggregating order metrics by state

### **created_at** (TIMESTAMP)
- **Type**: Timestamp with timezone (UTC)
- **Format**: UTC timestamp (e.g., "2018-11-09 08:16:58+00:00")
- **Nulls**: None (0%)
- **Uniqueness**: 39,999 unique values (near-unique per order)
- **Range**: 2017 to 2029
- **Use Case**: Time-based filtering, date range queries, temporal aggregations, ordering results

### **completed_at** (STRING)
- **Type**: String (stored as STRING instead of TIMESTAMP/DATETIME)
- **Format**: ISO 8601 string (e.g., "2019-10-11T04:47:25.000Z") or string literal "null"
- **Nulls**: 0% technical nulls, ~50% semantic nulls (string "null" values)
- **Uniqueness**: 19,863 unique non-null completion dates
- **Data Quality Issue**: Contains string "null" rather than actual NULL values
- **Use Case**: 
  - Requires string comparison (`WHERE completed_at != 'null'`) to filter completed orders
  - Needs CAST/PARSE for date operations
  - Calculate completion time (completed_at - created_at) for completed orders

## Potential Query Considerations

### **Good for Filtering:**
- `status` - Filter by order state (e.g., only completed orders)
- `created_at` - Date range filters, recent orders, historical analysis
- `completed_at` - Filter completed vs in-progress orders (remember to check for "null" string)
- `user_id` - Customer-specific order history
- `id` - Specific order lookup

### **Good for Grouping/Aggregation:**
- `status` - Count orders by status, status distribution analysis
- `user_id` - Orders per customer, customer behavior analysis
- `created_at` - Time-based aggregations (daily/monthly/yearly order counts, trends)
- Date extractions: EXTRACT(YEAR/MONTH/DAY FROM created_at) for temporal grouping

### **Potential Join Keys:**
- `id` - Primary key for joining with order_items, payments, or shipment tables
- `user_id` - Foreign key to join with users/customers table

### **Data Quality Considerations:**

1. **completed_at String Format**: 
   - Must use `completed_at != 'null'` instead of `IS NOT NULL`
   - Requires parsing/casting for date operations: `PARSE_TIMESTAMP('%Y-%m-%dT%H:%M:%E3SZ', completed_at)`
   - Consider filtering by status='completed' as alternative indicator

2. **Future Dates**: 
   - Data extends to 2029, which may be projections or test data
   - Consider filtering to current date for actual historical analysis

3. **Status Logic**:
   - Orders with status 'completed' should have completed_at values
   - Orders with status 'processing', 'shipped', or 'returned' likely have 'null' completion dates
   - Validate this relationship when analyzing completion rates

4. **Calculated Metrics**:
   - Order completion time: requires parsing completed_at and comparing with created_at
   - Completion rate: filter where completed_at != 'null' or status = 'completed'
   - Average orders per user: 40,000 orders / 22,185 users ≈ 1.8 orders

## Keywords

orders, e-commerce, transactions, order status, order lifecycle, customer orders, sales data, order management, order tracking, completed orders, shipped orders, returned orders, processing orders, order timestamps, order creation date, order completion date, user orders, customer purchases, order analytics, sales analytics, order metrics, BigQuery orders, transactional data, order history

## Table and Column Documentation

**Table Comment**: Not provided

**Column Comments**: 
- id: Not provided
- user_id: Not provided
- status: Not provided
- created_at: Not provided
- completed_at: Not provided

## cubes:
  - name: base_orders

    sql: SELECT * FROM orders

    public: false

    joins:
      - name: line_items
        sql: '{CUBE.id} = {line_items.order_id}'
        relationship: one_to_many

      - name: users
        sql: "{CUBE.user_id} = {users.id}"
        relationship: many_to_one


    dimensions:
      - name: id
        sql: id
        type: number
        primary_key: true

      - name: user_id
        sql: user_id
        type: number
        public: false

      - name: status
        sql: status
        type: string

      - name: created_at
        sql: "{CUBE}.created_at::TIMESTAMP"
        type: time

      - name: completed_at
        sql: "{CUBE}.completed_at::TIMESTAMP"
        type: time


    measures:
      - name: count
        type: count

      - name: completed_count
        type: count
        filters:
          - sql: "{CUBE}.status = 'completed'"

      - name: completed_percentage
        sql: "({completed_count} / NULLIF({count}, 0)) * 100.0"
        type: number
        format: percent

      - name: total
        type: count
        rolling_window:
          trailing: unbounded

      {% set metrics = {
        'dau': '1 day',
        'wau': '1 week',
        'mau': '1 month'
      } %}
      {% for name, window in metrics | items %}
      - name: {{ name }}
        sql: user_id
        type: count_distinct
        rolling_window:
          trailing: {{ window }}
      {% endfor %}

    pre_aggregations:
      - name: orders_by_month
        measures:
          - count
          - completed_count
          - completed_percentage
        time_dimension: created_at
        granularity: month

      - name: orders_and_line_items_of_users
        measures:
          - count
          - line_items.count
          - line_items.sum_price
        dimensions:
          - users.gender
          - users.state

## views:
  - name: orders
    cubes:
      - join_path: base_orders
        includes:
          - status
          - created_at
          - count
          - completed_count
          - completed_percentage
          - total
          - dau

  - name: customers
    cubes:
      # The 'join_path' property references a cube by its name
      - join_path: base_orders
        # This property will prepend 'count' with the name of the cube
        prefix: true
        # This property will override the name of the cube and make it 'orders' instead of 'base_orders'
        alias: orders
        # The 'includes' property allows to include dimensions and measures of that cube into this view.
        # Providing '*' will include all dimensions and measures of that cube at once
        includes:
          - count
        # The 'join_path' property can also reference a series of cubes, separated by dots.
        # These cubes would be joined in a sequence to the rightmost cube.
        # It provides the full control over the join path
      - join_path: base_orders.users
        includes: "*"
      - join_path: base_orders.line_items
        prefix: true
        includes:
          - count
          - avg_price
          - wau
          - mau
      - join_path: base_orders.users
        prefix: true
        includes:
          - city
          - age
          - state
      - join_path: base_orders.line_items
        prefix: true
        includes:
          - sum_price
          - avg_price
          - product_count