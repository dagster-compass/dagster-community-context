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

- **Total Rows**: 112,009 line items
- **Data Quality**: Excellent - no null values in any column (0% null percentage across all fields)
- **Primary Entity**: Order line items representing individual products within orders
- **Date Range**: Spans from 2016 to 2029 (includes future dates, suggesting this may be demo/test data)

**Notable Patterns:**
- **Order Distribution**: 40,000 unique orders with an average of ~2.8 line items per order (112,009 items / 40,000 orders)
- **Product Catalog**: Limited to 100 products (product_id ranges 1-100)
- **Price Variability**: Wide price range from $0.10 to $500.00 (assuming cents), suggesting diverse product types
- **Temporal Coverage**: Dataset covers approximately 13 years with high granularity timestamps

## Column Details

### **id** (INT64)
- **Type**: Primary Key
- **Range**: 1 to 112,009
- **Nulls**: None (0%)
- **Uniqueness**: 100% unique (112,009 distinct values)
- **Use Case**: Primary key for exact record lookups

### **order_id** (INT64)
- **Type**: Foreign Key
- **Range**: 1 to 40,000
- **Nulls**: None (0%)
- **Uniqueness**: 40,000 distinct values (many-to-one relationship)
- **Distribution**: Average ~2.8 line items per order
- **Use Case**: 
  - Critical for order-level aggregations
  - Join key to orders table
  - GROUP BY for order summaries

### **product_id** (INT64)
- **Type**: Foreign Key
- **Range**: 1-100
- **Nulls**: None (0%)
- **Uniqueness**: Only 100 distinct products
- **Distribution**: Each product appears in ~1,120 line items on average
- **Use Case**:
  - Essential for product-level analysis
  - Join key to products table
  - Good filter candidate for product-specific queries

### **price** (INT64)
- **Type**: Numeric Measure (likely in cents)
- **Range**: 10 to 50,000 (suggests $0.10 to $500.00)
- **Nulls**: None (0%)
- **Uniqueness**: 17,203 unique price points
- **Distribution**: High variability suggests different product types or dynamic pricing
- **Use Case**:
  - Primary measure for SUM, AVG, MIN, MAX aggregations
  - Revenue calculations
  - Price range filtering
  - Should be converted to decimal for currency display (divide by 100)

### **created_at** (TIMESTAMP)
- **Type**: Timestamp with timezone (UTC)
- **Range**: 2016 to 2029 (13+ year span)
- **Nulls**: None (0%)
- **Uniqueness**: 112,000 unique timestamps (near-unique)
- **Format**: UTC timezone (+00:00)
- **Note**: Future dates present - queries may need filtering for "actual" vs "projected" data
- **Use Case**:
  - Time-series analysis and trending
  - Date range filtering (WHERE clauses)
  - GROUP BY for temporal aggregations (daily, monthly, yearly)
  - ORDER BY for chronological sorting

## Potential Query Considerations

### **Good for Filtering:**
- `created_at` - Date range filters for time-bound analysis (e.g., `WHERE created_at < CURRENT_TIMESTAMP()` to exclude future dates)
- `product_id` - Specific product or product category analysis
- `price` - Price range segmentation (low/medium/high value items)
- `order_id` - Single order or order cohort analysis

### **Good for Grouping/Aggregation:**
- `product_id` - Product-level metrics (GROUP BY product_id)
- `order_id` - Order-level aggregations
- `created_at` - Temporal analysis (GROUP BY DATE(created_at) for daily trends, GROUP BY DATE_TRUNC(created_at, MONTH) for monthly analysis)
- `price` - Revenue metrics (SUM(price) for total revenue, AVG(price) for average line item value)

### **Potential Join Keys:**
- `order_id` - Join to orders table (expected parent table)
- `product_id` - Join to products table (expected dimension table for product details)
- **Cardinality**: Many line_items to one order; many line_items to one product

### **Data Quality Considerations:**

1. **Future Dates**: Queries should filter `created_at < CURRENT_TIMESTAMP()` unless analyzing projections
2. **Price Format**: Remember to divide by 100 for currency display
3. **Complete Data**: No null handling required - all fields are populated
4. **Sequential IDs**: The id column suggests no deletions; consider if analyzing historical patterns

## Keywords

transaction data, order line items, e-commerce, sales data, product sales, revenue analysis, order details, line-level data, transactional database, fact table, order items, purchase history, sales transactions, BigQuery, cube semantic layer, demo data, time-series data, product analytics, order analytics, retail data

## Table and Column Documentation

**Table Comment**: Not provided

**Column Comments**: Not provided

## cubes:
  - name: line_items
    sql: SELECT * FROM line_items
    public: false

    joins:
      - name: products
        sql: "{CUBE.product_id} = {products.id}"
        relationship: many_to_one

    dimensions:
      - name: id
        sql: id
        type: number
        primary_key: true

      - name: order_id
        sql: order_id
        type: number
        public: false

      - name: product_id
        sql: product_id
        type: number
        public: false


      - name: price
        sql: "price::DECIMAL"
        type: number
        format: currency

    measures:
      - name: count
        type: count

      - name: sum_price
        sql: "{price}"
        type: sum
        public: false

      - name: avg_price
        sql: "{sum_price} / {count}"
        type: number


      - name: price_range
        sql: "FLOOR(MIN({price})) || '..' || CEIL(MAX({price}))"
        type: string

      - name: product_count
        sql: product_id
        type: count_distinct_approx
