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

**Total Rows:** 112,009

**General Description:** This is a transactional line items table that represents individual products within orders. It appears to be a fact table in a semantic layer demo, containing order-level transaction details with pricing and temporal information.

**Data Quality:** Excellent - no null values detected in any column (0.00% null percentage across all fields).

**Notable Patterns:**
- The data spans approximately 11 years (2018-2029), with future dates suggesting this is test/demo data
- On average, each order contains ~2.8 line items (112,009 line items / 40,000 orders)
- Product catalog is limited to 100 distinct products
- Price distribution is wide-ranging (from $10 to $50,000)
- High cardinality in timestamps suggests precise transaction tracking

---

## Column Details

### **id** (INT64)
- **Purpose:** Primary key for line items
- **Type:** Integer, sequential
- **Range:** 1 to 112,009
- **Cardinality:** 112,009 unique values (one per row - perfect uniqueness)
- **Nulls:** None (0.00%)
- **Query Use:** Primary identifier for individual line items; use for exact record lookups and joins

### **order_id** (INT64)
- **Purpose:** Foreign key linking to orders table
- **Type:** Integer
- **Range:** 1 to 40,000
- **Cardinality:** 40,000 unique values
- **Nulls:** None (0.00%)
- **Distribution:** Multiple line items per order (avg 2.8 items per order)
- **Query Use:** Excellent for grouping/aggregation by order, joining to orders table, filtering by specific orders

### **product_id** (INT64)
- **Purpose:** Foreign key linking to products table
- **Type:** Integer
- **Range:** 1 to 100
- **Cardinality:** 100 unique values
- **Nulls:** None (0.00%)
- **Distribution:** Limited product catalog suggests repeated purchases across orders
- **Query Use:** Ideal for product-level analysis, grouping by product, joining to product dimension table

### **price** (INT64)
- **Purpose:** Transaction amount for the line item
- **Type:** Integer (likely representing cents or smallest currency unit)
- **Range:** 10 to 50,000
- **Cardinality:** 17,203 unique values
- **Nulls:** None (0.00%)
- **Distribution:** Wide range suggests diverse product pricing or quantity-based pricing
- **Query Use:** Perfect for SUM aggregations (revenue), AVG calculations, financial analysis, price range filtering

### **created_at** (TIMESTAMP)
- **Purpose:** Transaction timestamp
- **Type:** Timestamp with timezone (UTC indicated by +00:00)
- **Range:** 2018-05-30 to 2029-08-24 (approximately 11 years)
- **Cardinality:** 112,000 unique values (high precision, minimal duplicates)
- **Nulls:** None (0.00%)
- **Format:** ISO 8601 format with microsecond precision
- **Query Use:** Excellent for temporal analysis, time-series queries, date-based filtering and grouping

---

## Potential Query Considerations

### **Best Columns for Filtering:**
- `created_at`: Time-range filters (WHERE created_at BETWEEN...)
- `order_id`: Specific order lookups
- `product_id`: Product-specific analysis
- `price`: Price range filters (WHERE price > 1000)

### **Best Columns for Grouping/Aggregation:**
- `order_id`: Order-level metrics (items per order, order totals)
- `product_id`: Product performance analysis
- `created_at`: Temporal aggregations (daily/monthly/yearly trends using DATE_TRUNC or EXTRACT)
- Combined grouping: product sales by time period

### **Potential Join Keys:**
- `order_id`: Join to orders table (many-to-one relationship)
- `product_id`: Join to products dimension table (many-to-one relationship)
- `id`: Join as foreign key in other tables if needed

### **Data Quality Considerations:**
1. **Future Dates:** Data extends to 2029, indicating test/demo data - queries should consider appropriate date ranges
2. **Price as Integer:** May require division by 100 if representing cents (verify currency handling)
3. **No Quantity Column:** Price appears to be total line price (not unit price × quantity)
4. **Perfect Data Quality:** Zero nulls make queries simpler but may not reflect production scenarios

### **Common Query Patterns:**
- Revenue analysis: `SUM(price) GROUP BY order_id/product_id/DATE(created_at)`
- Order size analysis: `COUNT(*) GROUP BY order_id`
- Product popularity: `COUNT(*), SUM(price) GROUP BY product_id`
- Time-series trends: `SUM(price) GROUP BY DATE_TRUNC(created_at, MONTH)`
- Average order value: `AVG(order_total) FROM (SELECT order_id, SUM(price) as order_total GROUP BY order_id)`

---

## Keywords

e-commerce, line items, order details, transactions, sales data, revenue, pricing, products, orders, temporal data, fact table, semantic layer, BigQuery, demo data, order line items, transaction details, sales analytics, time series, product sales, order value, SKU, purchase data

---

## Table and Column Documentation

**Table Comment:** Not provided

**Column Comments:** Not provided