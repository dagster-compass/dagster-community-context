---
columns:
- created_at (TIMESTAMP)
- id (INT64)
- name (STRING)
- product_category (STRING)
schema_hash: fb3b60337ab24821d62c1c9c4c909ea6357ccb36b4026c88122915554134a42b

---
# Products Table Documentation Summary

## Overall Dataset Characteristics

- **Total Rows**: 100 records
- **Data Quality**: Excellent - no null values detected in any column
- **Time Range**: Created dates span from 2016 to 2024 (approximately 8 years)
- **Data Type**: This appears to be a product catalog table with synthetic/demo data (evidenced by whimsical product names like "Gorgeous Cotton Sausages")
- **Distribution**: Products are distributed across 10 distinct categories with 100 unique IDs

## Column Details

### id (INT64)
- **Purpose**: Primary key/unique identifier
- **Range**: 1 to 100 (sequential)
- **Characteristics**: 
  - No nulls (0.00%)
  - 100 unique values (one per row)
  - Complete sequential coverage
  - Integer type suitable for joins and indexing

### name (STRING)
- **Purpose**: Product name/title
- **Characteristics**:
  - No nulls (0.00%)
  - 62 unique values (indicates some duplicate names across the 100 products)
  - Pattern: Follows format of "[Adjective] [Material] [Noun]" (e.g., "Sleek Metal Shirt")
  - Text data suitable for search and display purposes

### product_category (STRING)
- **Purpose**: Product classification/categorization
- **Characteristics**:
  - No nulls (0.00%)
  - 10 distinct categories
  - **Complete Category List**: Beauty, Clothing, Computers, Electronics, Home, Jewellery, Phones, Sports, Toys, Watches
  - Evenly distributed (approximately 10 products per category)
  - Ideal for grouping and filtering operations

### created_at (TIMESTAMP)
- **Purpose**: Product creation/registration timestamp
- **Characteristics**:
  - No nulls (0.00%)
  - 100 unique timestamps (one per product)
  - **Time Range**: 2016-04-10 to 2024-10-13
  - Includes timezone information (UTC +00:00)
  - Full timestamp precision with microseconds
  - Suitable for time-based analysis and filtering

## Query Considerations

### Optimal Filtering Columns
- **product_category**: Excellent for WHERE clauses (10 distinct values, categorical data)
- **created_at**: Good for date range filters (e.g., products created in specific years/months)
- **id**: Perfect for specific record lookups (primary key)

### Grouping/Aggregation Opportunities
- **product_category**: Primary grouping dimension for category-level analysis
- **created_at**: Can be used with date functions (YEAR, MONTH, DATE) for temporal grouping
- **Examples**: 
  - Count of products per category
  - Products created per year/month
  - Category distribution over time

### Join Key Capabilities
- **id**: Primary key - likely used to join with other tables (orders, inventory, line_items, etc.)
- Expected foreign key relationships in related tables: `product_id`, `products.id`

### Data Quality Considerations
- **No missing data**: All columns have 100% completeness - no special null handling needed
- **Duplicate names**: Only 62 unique names for 100 products - queries filtering by name alone may return multiple products
- **Synthetic data**: Whimsical product names suggest this is demo/test data rather than production data
- **Sequential IDs**: ID range exactly matches row count (1-100), suggesting no deleted records
- **Category consistency**: Standardized category names (proper capitalization, consistent spelling)

## Keywords

products, product catalog, e-commerce, inventory, product categories, merchandise, items, goods, SKU, product master, demo data, sample data, beauty products, clothing, computers, electronics, home goods, jewellery, phones, sports equipment, toys, watches, product creation date, timestamp, product ID, product name, category analysis, product segmentation

## Table and Column Docs

**Table Comment**: Not provided

**Column Comments**: Not provided

---

## Additional Notes

This appears to be a demonstration/sample dataset for the Cube semantic layer, likely used for testing analytics queries and dashboard functionality. The data structure is clean and well-suited for:
- Category-based product analysis
- Time-series analysis of product creation
- Basic product catalog queries
- Join operations with transactional tables (orders, sales, etc.)

The absence of columns like price, stock quantity, or status suggests this table focuses on core product identification and may be joined with separate tables for pricing, inventory, and sales data.