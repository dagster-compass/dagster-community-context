---
columns:
- created_at (TIMESTAMP)
- id (INT64)
- order_id (INT64)
- price (INT64)
- product_id (INT64)
schema_hash: 42fb564d70aca5734c9795bceadf738fdbfb9e250cde6c00d487238fcf8cd042

---
# Table Summary: compass-bigquery-demo.cube_semantic_layer_demo.line_items

## Overall Dataset Characteristics

### Dataset Overview
- **Total Rows**: 112,009 line items
- **Data Quality**: Excellent - no null values in any column (0% null percentage across all fields)
- **Primary Entity**: Order line items representing individual products within orders
- **Date Range**: Spans from 2016 to 2029 (includes future dates, suggesting this may be demo/test data)

### Notable Patterns
- **Order Distribution**: 40,000 unique orders with an average of ~2.8 line items per order (112,009 items / 40,000 orders)
- **Product Catalog**: Limited to 100 products (product_id ranges 1-100)
- **Price Variability**: Wide price range from $0.10 to $500.00 (assuming cents), suggesting diverse product types
- **Temporal Coverage**: Dataset covers approximately 13 years with high granularity timestamps

## Column Details

### id (INT64) - Primary Key
- **Purpose**: Unique line item identifier
- **Characteristics**: Sequential numbering from 1 to 112,009
- **Uniqueness**: 100% unique (112,009 distinct values)
- **Null Pattern**: No nulls
- **Query Usage**: Primary key for exact record lookups

### order_id (INT64) - Foreign Key
- **Purpose**: Links line items to parent orders
- **Characteristics**: Values range from 1 to 40,000
- **Uniqueness**: 40,000 distinct values (many-to-one relationship)
- **Distribution**: Average ~2.8 line items per order
- **Null Pattern**: No nulls
- **Query Usage**: 
  - Critical for order-level aggregations
  - Join key to orders table
  - GROUP BY for order summaries

### product_id (INT64) - Foreign Key
- **Purpose**: References product catalog
- **Characteristics**: Small fixed range (1-100)
- **Uniqueness**: Only 100 distinct products
- **Distribution**: Each product appears in ~1,120 line items on average
- **Null Pattern**: No nulls
- **Query Usage**:
  - Essential for product-level analysis
  - Join key to products table
  - High cardinality for GROUP BY operations
  - Good filter candidate for product-specific queries

### price (INT64) - Numeric Measure
- **Purpose**: Line item price (likely in cents)
- **Characteristics**: 
  - Range: 10 to 50,000 (suggests $0.10 to $500.00)
  - 17,203 unique price points
- **Distribution**: High variability suggests different product types or dynamic pricing
- **Null Pattern**: No nulls
- **Query Usage**:
  - Primary measure for SUM, AVG, MIN, MAX aggregations
  - Revenue calculations
  - Price range filtering
  - Should be converted to decimal for currency display (divide by 100)

### created_at (TIMESTAMP) - Temporal Key
- **Purpose**: Line item creation timestamp
- **Characteristics**:
  - Range: 2016 to 2029 (13+ year span)
  - 112,000 unique timestamps (near-unique)
  - UTC timezone (+00:00)
- **Distribution**: High granularity (seconds precision)
- **Null Pattern**: No nulls
- **Query Usage**:
  - Time-series analysis and trending
  - Date range filtering (WHERE clauses)
  - GROUP BY for temporal aggregations (daily, monthly, yearly)
  - ORDER BY for chronological sorting
  - **Note**: Future dates present - queries may need filtering for "actual" vs "projected" data

## Potential Query Considerations

### Recommended Filters
1. **created_at**: Date range filters for time-bound analysis
   - Example: `WHERE created_at < CURRENT_TIMESTAMP()` to exclude future dates
2. **product_id**: Specific product or product category analysis
3. **price**: Price range segmentation (low/medium/high value items)
4. **order_id**: Single order or order cohort analysis

### Aggregation Opportunities
1. **Revenue Metrics**:
   - `SUM(price)` for total revenue
   - `AVG(price)` for average line item value
2. **Volume Metrics**:
   - `COUNT(*)` for line item count
   - `COUNT(DISTINCT order_id)` for order count
3. **Product Performance**:
   - GROUP BY product_id for product-level metrics
4. **Temporal Analysis**:
   - GROUP BY DATE(created_at) for daily trends
   - GROUP BY DATE_TRUNC(created_at, MONTH) for monthly analysis

### Join Relationships
- **orders table**: JOIN ON order_id (expected parent table)
- **products table**: JOIN ON product_id (expected dimension table for product details)
- **Cardinality**: Many line_items to one order; many line_items to one product

### Data Quality Considerations
1. **Future Dates**: Queries should filter `created_at < CURRENT_TIMESTAMP()` unless analyzing projections
2. **Price Format**: Remember to divide by 100 for currency display
3. **Complete Data**: No null handling required - all fields are populated
4. **Sequential IDs**: The id column suggests no deletions; consider if analyzing historical patterns

## Keywords

transaction data, order line items, e-commerce, sales data, product sales, revenue analysis, order details, line-level data, transactional database, fact table, order items, purchase history, sales transactions, BigQuery, cube semantic layer, demo data, time-series data, product analytics, order analytics, retail data

## Table and Column Documentation

**Table Comment**: Not provided

**Column Comments**: Not provided