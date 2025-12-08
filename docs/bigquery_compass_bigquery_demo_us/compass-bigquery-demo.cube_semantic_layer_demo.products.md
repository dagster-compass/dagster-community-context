---
columns:
- created_at (TIMESTAMP)
- id (INT64)
- name (STRING)
- product_category (STRING)
schema_hash: fb3b60337ab24821d62c1c9c4c909ea6357ccb36b4026c88122915554134a42b

---
# Table Summary: compass-bigquery-demo.cube_semantic_layer_demo.products

## Overall Dataset Characteristics

- **Total Rows**: 100
- **Data Quality**: Excellent - no null values across any columns
- **Time Span**: Data spans from 2016 to 2023 (approximately 7 years based on created_at timestamps)
- **Dataset Nature**: Product catalog with categories, names, creation timestamps, and unique identifiers
- **Notable Patterns**: 
  - Product names appear to follow a pattern (e.g., "Handcrafted/Handmade/Rustic + Material + Item")
  - Some product names are duplicated (62 unique names for 100 products)
  - Even distribution across 10 product categories

## Column Details

### id (INT64)
- **Data Type**: Integer (64-bit)
- **Null Values**: None (0%)
- **Range**: 1 to 100 (sequential, complete range)
- **Characteristics**: Primary key, unique identifier for each product
- **Pattern**: Sequential integers with no gaps

### product_category (STRING)
- **Data Type**: String/Text
- **Null Values**: None (0%)
- **Unique Values**: 10 distinct categories
- **Categories**: Beauty, Clothing, Computers, Electronics, Home, Jewellery, Phones, Sports, Toys, Watches
- **Pattern**: Standardized category names, proper capitalization
- **Distribution**: Appears relatively balanced across categories (10 rows per category average)

### name (STRING)
- **Data Type**: String/Text
- **Null Values**: None (0%)
- **Unique Values**: 62 unique names for 100 products
- **Pattern**: Follows format: [Adjective] + [Material] + [Item]
  - Adjectives: Handcrafted, Rustic, Handmade, Sleek, Practical
  - Materials: Frozen, Soft, Metal, Wooden, Plastic
  - Items: Table, Fish, Shirt, Gloves, Chair, Chicken
- **Duplication**: Some products share the same name (38 duplicates across the dataset)

### created_at (TIMESTAMP)
- **Data Type**: Timestamp with timezone (UTC)
- **Null Values**: None (0%)
- **Unique Values**: 100 (every row has a unique timestamp)
- **Date Range**: 2016-04-10 to 2023-07-14
- **Pattern**: Includes date, time, and microsecond precision
- **Distribution**: Spread across multiple years, suggesting ongoing product additions

## Potential Query Considerations

### Filtering Recommendations
- **product_category**: Excellent for WHERE clauses - only 10 values, consistent naming
- **created_at**: Useful for date range filtering (e.g., products added in specific years, quarters)
- **id**: Perfect for exact lookups and range queries
- **name**: Can be used for pattern matching with LIKE, but note duplicates

### Grouping/Aggregation Recommendations
- **product_category**: Primary grouping dimension for category-level analysis
- **created_at**: Can be extracted for temporal grouping (year, month, quarter)
- **name**: Less reliable for grouping due to duplicates, but possible for name-based analysis

### Join Key Considerations
- **id**: Primary key - ideal for joining with related tables (e.g., order_items, inventory, pricing)
- **product_category**: Potential foreign key relationship with a categories dimension table
- **created_at**: Could be used for temporal joins or range-based relationships

### Data Quality Considerations
- **No Missing Data**: All columns are complete, simplifying query logic (no NULL handling needed)
- **Name Duplicates**: When querying by name, expect multiple products; use id for unique identification
- **Category Consistency**: Clean categorical values enable reliable GROUP BY operations
- **Timestamp Precision**: High precision timestamps allow for granular temporal analysis
- **Sequential IDs**: Complete 1-100 range suggests no deleted records or gaps

## Keywords

products, product catalog, e-commerce, inventory, categories, product categories, merchandise, retail, items, goods, beauty products, clothing, computers, electronics, home goods, jewellery, jewelry, phones, sports equipment, toys, watches, product names, creation date, product id, timestamp data, catalog data, semantic layer, cube, BigQuery

## Table and Column Documentation

**Table Comment**: Not provided

**Column Comments**: Not provided

---

## Query Pattern Examples

This table is well-suited for:
- Category-based product analysis: `GROUP BY product_category`
- Temporal analysis: Product additions over time using `created_at`
- Product lookup: Direct retrieval via `id`
- Inventory counting: Total products per category
- Time-series analysis: Products created per year/month/quarter
- Cross-category comparisons: Aggregate metrics across different product categories