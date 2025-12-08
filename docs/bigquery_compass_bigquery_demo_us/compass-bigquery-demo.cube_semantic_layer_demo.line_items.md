---
columns:
- created_at (TIMESTAMP)
- id (INT64)
- order_id (INT64)
- price (INT64)
- product_id (INT64)
schema_hash: 42fb564d70aca5734c9795bceadf738fdbfb9e250cde6c00d487238fcf8cd042

---
# Table Summary: line_items

## Overall Dataset Characteristics

**Total Rows:** 112,009

**General Data Quality:** Excellent - All columns have 0% null values, indicating complete data integrity across the dataset.

**Table Purpose:** This appears to be a transactional line items table that records individual product purchases within orders. It's a classic order detail/line item table in an e-commerce or sales system.

**Notable Patterns:**
- The dataset spans multiple years (2018-2029), suggesting either historical data with future projections or test data
- Each line item has a unique ID, but multiple line items can belong to the same order (average ~2.8 items per order: 112,009 items / 40,000 orders)
- Product catalog consists of 100 distinct products
- Price distribution is wide-ranging ($10 to $50,000), suggesting diverse product categories or tiers

## Column Details

### id (INT64)
- **Type:** Primary key, integer identifier
- **Null Pattern:** None (0%)
- **Uniqueness:** 100% unique (112,009 distinct values for 112,009 rows)
- **Range:** Sequential from 1 to 112,009
- **Purpose:** Unique identifier for each line item record

### order_id (INT64)
- **Type:** Foreign key, integer identifier
- **Null Pattern:** None (0%)
- **Uniqueness:** 40,000 distinct values across 112,009 rows
- **Range:** 1 to 40,000
- **Purpose:** Links line items to parent orders; indicates multiple items per order
- **Relationship:** Average of 2.8 line items per order

### product_id (INT64)
- **Type:** Foreign key, integer identifier
- **Null Pattern:** None (0%)
- **Uniqueness:** 100 distinct products
- **Range:** 1 to 100
- **Purpose:** References product catalog
- **Distribution:** Appears to have consistent representation across the catalog

### price (INT64)
- **Type:** Numeric value (stored as integer, likely representing cents or lowest currency unit)
- **Null Pattern:** None (0%)
- **Uniqueness:** 17,203 distinct price points
- **Range:** $10 to $50,000 (or 10 to 50,000 cents)
- **Distribution:** Wide price range suggests product diversity or tiered pricing
- **Sample Values:** 82, 428, 74, 29, 1524, 136, 334, 976

### created_at (TIMESTAMP)
- **Type:** Timestamp with timezone (UTC +00:00)
- **Null Pattern:** None (0%)
- **Uniqueness:** Nearly unique (112,000 distinct timestamps for 112,009 rows)
- **Range:** 2018-12-21 to 2029-04-09 (approximately 10+ year span)
- **Purpose:** Records when the line item was created/purchased
- **Pattern:** High granularity (seconds precision) with minimal duplicates

## Query Considerations

### Good Filtering Columns:
- **created_at**: Excellent for time-based analysis, date range filters, trend analysis
- **order_id**: Filter by specific orders or order ranges
- **product_id**: Filter by specific products (limited to 100 values, good for categorical analysis)
- **price**: Range filters for price-based segmentation

### Good Grouping/Aggregation Columns:
- **order_id**: Group to calculate order totals, item counts per order
- **product_id**: Group for product performance analysis, sales by product
- **created_at**: Group by time periods (daily, monthly, yearly sales)
- **price**: Can be bucketed for price range analysis

### Potential Join Keys:
- **order_id**: Join to orders table for customer information, shipping details, order status
- **product_id**: Join to products table for product names, categories, descriptions, cost data
- **id**: Primary key for referencing specific line items

### Aggregation Opportunities:
- **SUM(price)**: Total revenue calculations
- **COUNT(*)**: Item quantity, order frequency
- **AVG(price)**: Average transaction value
- **COUNT(DISTINCT order_id)**: Unique order counts

### Data Quality Considerations:

**Strengths:**
- No missing data - all fields are complete
- Consistent data types
- Sequential ID pattern suggests reliable data loading
- High cardinality in timestamps indicates precise transaction recording

**Considerations:**
- Future dates (up to 2029) may need filtering for real-time analysis
- Price stored as integer - may need division by 100 for currency display
- No quantity field - assumes one unit per line item or quantity is implicit
- No discount or tax fields - price appears to be the final line item amount

**Query Tips:**
- Use date extraction functions (DATE(), YEAR(), MONTH()) on created_at for time-series analysis
- Consider price as cents/pennies and divide by 100 for dollar amounts if needed
- Group by order_id to aggregate line items into order-level metrics
- Join with product and order tables for enriched analysis

## Keywords

e-commerce, sales transactions, line items, order details, transactional data, product sales, purchase history, revenue analysis, order items, shopping cart, transaction records, sales data, order line items, product purchases, timestamp data, price points, order breakdown, cart items, purchase details, sales metrics

## Table and Column Documentation

**Table Comment:** Not provided

**Column Comments:** Not provided