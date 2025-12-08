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
- **Data Quality**: Excellent - no null values detected in any column
- **Dataset Type**: Product catalog/inventory table
- **Time Range**: Products created between 2017-08-01 and 2022-09-09 (approximately 5 years)
- **Key Pattern**: This appears to be a sample/demo dataset with synthetic product names (e.g., "Handcrafted Frozen Table", "Sleek Soft Chicken") following a pattern of [Adjective] [Material] [Object]

## Column Details

### **id** (INT64)
- **Type**: Integer, Primary Key
- **Range**: 1 to 100
- **Nulls**: 0%
- **Uniqueness**: 100% unique (all 100 values are distinct)
- **Use Case**: Primary key for joins, filtering specific products

### **name** (STRING)
- **Type**: Text string
- **Nulls**: 0%
- **Uniqueness**: 62 unique values out of 100 rows (62% unique)
- **Pattern**: Descriptive product names following format: [Adjective] [Material/Type] [Item]
- **Examples**: "Handcrafted Frozen Table", "Sleek Soft Chicken", "Practical Plastic Chair"
- **Note**: 38 duplicate names exist, suggesting some products share the same name
- **Use Case**: Text search, display purposes, potential grouping (though duplicates exist)

### **product_category** (STRING)
- **Type**: Categorical string
- **Nulls**: 0%
- **Uniqueness**: 10 distinct categories
- **Complete Category List**: Beauty, Clothing, Computers, Electronics, Home, Jewellery, Phones, Sports, Toys, Watches
- **Distribution**: Appears relatively balanced across categories
- **Use Case**: Excellent for filtering, grouping, and aggregation operations

### **created_at** (TIMESTAMP)
- **Type**: Timestamp with timezone (UTC)
- **Nulls**: 0%
- **Uniqueness**: 100% unique (each product has distinct creation timestamp)
- **Range**: 2017-08-01 to 2022-09-09 (5+ years span)
- **Precision**: Microsecond precision
- **Use Case**: Time-based filtering, temporal analysis, ordering by creation date

## Potential Query Considerations

### **Good for Filtering:**
- `product_category` - Clean categorical data, perfect for WHERE clauses
- `id` - Primary key for exact lookups
- `created_at` - Temporal filtering (date ranges, year/month/day extraction)

### **Good for Grouping/Aggregation:**
- `product_category` - 10 well-defined categories for GROUP BY operations
- `created_at` - Can extract year, month, quarter for temporal aggregations
- `name` - Possible but consider 38% duplication rate

### **Potential Join Keys:**
- `id` - Primary key, likely used to join with related tables (e.g., orders, inventory, pricing)

### **Data Quality Considerations:**

1. **Duplicate Product Names**: 38 products share names with others - queries filtering by name may return multiple rows
2. **Synthetic Data**: Product names appear generated/synthetic rather than real products
3. **No Price/Stock Data**: This table only contains basic product metadata
4. **Complete Data**: Zero nulls means no special null handling required in queries
5. **Time Distribution**: Products created over 5 years - consider date-based filtering for recent products

## Keywords

products, product catalog, inventory, e-commerce, product categories, Beauty, Clothing, Computers, Electronics, Home, Jewellery, Phones, Sports, Toys, Watches, created_at, timestamp, product_id, product_name, categorical data, demo dataset, cube semantic layer, BigQuery

## Table and Column Documentation

**Table Comment**: Not provided

**Column Comments**: 
- **id**: Not provided
- **name**: Not provided
- **product_category**: Not provided
- **created_at**: Not provided

---

**Summary**: This is a clean, well-structured product catalog table with 100 products across 10 categories. It's ideal for demonstration purposes with zero null values and consistent data quality. The table supports product categorization, temporal analysis, and can serve as a dimension table in larger data models. The synthetic nature of product names and even distribution suggests this is a demo/test dataset for the Cube semantic layer.

## cubes:
  - name: products
    sql: SELECT * FROM products
    public: false

    dimensions:
      - name: id
        sql: id
        type: number
        primary_key: true

      - name: name
        sql: name
        type: string

      - name: created_at
        sql: "{CUBE}.created_at::TIMESTAMP"
        type: time

      - name: product_category
        sql: product_category
        type: string

    measures:
      - name: count
        type: count
