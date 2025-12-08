---
columns:
- completed_at (STRING)
- created_at (TIMESTAMP)
- id (INT64)
- status (STRING)
- user_id (INT64)
schema_hash: ac6a2575da918ecb86264db94cfd6c9748e8ab331c35d72882d341f95d4af95a

---
# Table Summary: orders

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

### id (INT64)
- **Purpose**: Primary key / unique order identifier
- **Range**: 1 to 40,000
- **Characteristics**: Sequential integer, 100% unique, no nulls
- **Query Use**: Primary key for joins, filtering specific orders

### user_id (INT64)
- **Purpose**: Foreign key linking to users/customers
- **Range**: 2 to 30,000
- **Characteristics**: 22,185 unique users, no nulls, some users have multiple orders
- **Query Use**: Foreign key for joins, grouping by customer, filtering by user

### status (STRING)
- **Purpose**: Current state of the order
- **Values**: 4 distinct statuses
  - `completed`
  - `processing`
  - `returned`
  - `shipped`
- **Characteristics**: No nulls, categorical data, ~25% distribution per status
- **Query Use**: Excellent for filtering, grouping, and aggregating order metrics by state

### created_at (TIMESTAMP)
- **Purpose**: Order creation timestamp
- **Format**: UTC timestamp (e.g., "2018-11-09 08:16:58+00:00")
- **Characteristics**: 
  - No nulls
  - 39,999 unique values (near-unique per order)
  - Range: 2017 to 2029
- **Query Use**: Time-based filtering, date range queries, temporal aggregations, ordering results

### completed_at (STRING)
- **Purpose**: Order completion timestamp
- **Format**: ISO 8601 string (e.g., "2019-10-11T04:47:25.000Z") or string literal "null"
- **Data Quality Issue**: Stored as STRING instead of TIMESTAMP/DATETIME
  - Contains string "null" rather than actual NULL values
  - Approximately 50% of records have string "null" value
  - Only 19,863 unique non-null completion dates
- **Characteristics**:
  - 0% technical nulls (column always populated)
  - ~50% semantic nulls (string "null" values)
  - Represents logical state: orders with status "returned" or "shipped" likely have "null" completion
- **Query Use**: 
  - Requires string comparison (`WHERE completed_at != 'null'`) to filter completed orders
  - Needs CAST/PARSE for date operations
  - Calculate completion time (completed_at - created_at) for completed orders

## Potential Query Considerations

### Good for Filtering
- **status**: Filter by order state (e.g., only completed orders)
- **created_at**: Date range filters, recent orders, historical analysis
- **completed_at**: Filter completed vs in-progress orders (remember to check for "null" string)
- **user_id**: Customer-specific order history
- **id**: Specific order lookup

### Good for Grouping/Aggregation
- **status**: Count orders by status, status distribution analysis
- **user_id**: Orders per customer, customer behavior analysis
- **created_at**: Time-based aggregations (daily/monthly/yearly order counts, trends)
- **Date extractions**: EXTRACT(YEAR/MONTH/DAY FROM created_at) for temporal grouping

### Potential Join Keys
- **id**: Primary key for joining with order_items, payments, or shipment tables
- **user_id**: Foreign key to join with users/customers table

### Data Quality Considerations

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