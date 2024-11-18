# Database Design and Introduction to MySQL

Data Warehouse:
1. Characterstics of data warehouse
   - Subject-oriented
   - Integrated
   - Non-volatile
   - Time-variant
   
2. Dimentional Modelling
   - Facts 
   - Dimensions

# Database Design

- An organisation cannot track its business activities efficiently by maintaining a large number of files. Hence, databases are used for accessing and managing data efficiently. A software known as Database Management System (DBMS) is used widely in the industry to analyse data easily.

# What is a Data Warehouse?

A data warehouse is a collection of data. It has the following properties:

- **Subject-oriented:** A data warehouse should contain information about a few well-defined subjects rather than the enterprise.
- **Integrated:** A data warehouse is an integrated repository of data. It contains information from various systems within an organisation.
- **Non-volatile:** The data values in a database cannot be changed without a valid reason.
- **Time-variant:** A data warehouse contains historical data for analysis.

- A data warehouse would thus be the central repository of data of the entire enterprise.
- OLAP, which stands for Online Analytical Processing systems. OLAP is used to extract business-relevant information and perform analysis on the data stored in data warehouses.
  

# Structure of a Data Warehouse

- One of the primary methods of designing a data warehouse is dimensional modelling.
- The two key elements of dimensional modelling include facts and dimensions, which are basically the different types of variables that are used to design a data warehouse.
- They are arranged in a specific manner, known as a schema diagram.
- Facts are the numerical data in a data warehouse and dimensions are the metadata (that is, data explaining some other data) attached to the fact variables.

# 1.Star Schema

A **Star Schema** is a type of database schema commonly used in data warehousing and business intelligence (BI) systems. It is designed to optimize query performance and facilitate the analysis of large volumes of data. The Star Schema gets its name from the way its structure resembles a star, with a central "fact" table connected to several "dimension" tables, forming the shape of a star.

## Key Components of a Star Schema

### 1. Fact Table
- The central table in the schema that contains the quantitative data (measures) to be analyzed, such as sales amounts, quantities, or transaction totals.
- The fact table includes foreign keys that reference the dimension tables and typically contains numeric facts (e.g., `total_sales`, `quantity_sold`, `revenue`).
- Example: A **Sales Fact** table might have columns for `sale_id`, `product_id`, `store_id`, `date_id`, `amount_sold`, and `total_revenue`.

### 2. Dimension Tables
- These tables contain descriptive attributes or characteristics that provide context to the facts.
- Dimensions are used to filter, group, or segment the data in the fact table.
- Example: Dimension tables might include `Product`, `Store`, `Time`, `Customer`, or `Region` tables.
  - The `Product` dimension might contain attributes like `product_id`, `product_name`, `category`, `brand`, etc.
  - The `Time` dimension might contain attributes like `date_id`, `day`, `month`, `quarter`, and `year`.

### 3. Relationships
- The fact table is connected to each dimension table through foreign keys. These foreign keys point to the primary keys in the dimension tables.
- This design makes it easy to query and aggregate data by different attributes (e.g., total sales by product, region, or time period).

## Example of Star Schema

Let's consider an example for a sales data warehouse:

### Fact Table: Sales Fact
| sale_id | product_id | store_id | date_id  | total_sales | quantity_sold |
|---------|------------|----------|----------|-------------|---------------|
| 1       | 101        | 200      | 20230101 | 500         | 10            |
| 2       | 102        | 201      | 20230102 | 300         | 5             |

### Dimension Table: Product
| product_id | product_name | category   | brand |
|------------|--------------|------------|-------|
| 101        | Laptop       | Electronics| XYZ   |
| 102        | Smartphone   | Electronics| ABC   |

### Dimension Table: Store
| store_id | store_name   | city        | region |
|----------|--------------|-------------|--------|
| 200      | Store A      | New York    | North  |
| 201      | Store B      | Los Angeles | West   |

### Dimension Table: Time
| date_id   | day | month | quarter | year |
|-----------|-----|-------|---------|------|
| 20230101  | 1   | 1     | 1       | 2023 |
| 20230102  | 2   | 1     | 1       | 2023 |

## Advantages of the Star Schema

1. **Simplicity**:
   - The structure is easy to understand, with a central fact table and easily identifiable dimension tables.
   - This simplicity makes it easier to design and query.

2. **Performance**:
   - Queries are fast because the star schema is optimized for read-heavy operations (as is typical in BI systems).
   - The denormalized structure of the dimension tables reduces the need for complex joins.

3. **Efficient Querying**:
   - Since the dimension tables are typically smaller than the fact table, querying is efficient. It is straightforward to perform aggregations or drill down on different levels of dimension attributes (e.g., total sales by month, by region, etc.).

4. **Ease of Maintenance**:
   - Dimension tables are usually static (i.e., they don’t change frequently), so they don’t require much maintenance once they are set up.

## Disadvantages of the Star Schema

1. **Data Redundancy**:
   - In the dimension tables, data can be redundant because attributes are typically repeated for each fact record. For example, the product name and category would be stored repeatedly for each sale of that product.
   - This leads to higher storage costs and possible inconsistencies if the dimension data is not properly managed.

2. **Normalization Issues**:
   - The star schema is generally denormalized, which can lead to some level of data redundancy and make it harder to enforce consistency in dimension tables (for example, product descriptions might be inconsistent across rows).

3. **Limited Flexibility**:
   - Star schema is suited for analytical queries but may not be ideal for transactional systems. It does not handle complex many-to-many relationships between facts and dimensions as efficiently as other schema types (e.g., Snowflake Schema).
  
![image](https://github.com/user-attachments/assets/a83947a0-7af6-4723-99b8-1cabd6f75a71)


## Star Schema vs. Snowflake Schema

| S.No | Star Schema                                                             | Snow Flake Schema                                                            |
|------|-------------------------------------------------------------------------|------------------------------------------------------------------------------|
| 1    | Data redundancy is more.                                                | Data redundancy is less.                                                     |
| 2    | Storage space for dimension tables is more.                             | Storage space for dimension tables is comparatively less.                    |
| 3    | Contains de-normalized dimension tables.                                | Contains normalized dimension tables.                                        |
| 4    | Single fact table is surrounded by multiple dimension tables.           | Single fact table is surrounded by multiple hierarchies of dimension tables. |
| 5    | Queries use direct joins between fact and dimensions to fetch the data. | Queries use complex joins between fact and dimensions to fetch the data.     |
| 6    | Query execution time is less.                                           | Query execution time is more.                                                |
| 7    | Anyone can easily understand and design the schema.                     | It is tough to understand and design the schema.                             |
| 8    | Uses top down approach.                                                 | Uses bottom up approach.                                                     |



# 2.Snowflake Schema

The **Snowflake Schema** is a type of database schema used in data warehousing and business intelligence (BI) systems. It is a more normalized version of the **Star Schema** and is designed to organize data in a way that reduces redundancy and improves storage efficiency. The Snowflake Schema is named for its structure, which looks like a snowflake due to the way dimension tables are split into multiple related tables.

## Key Components of a Snowflake Schema

### 1. Fact Table
- Like in the Star Schema, the **Fact Table** is the central table containing the quantitative data (measures) that are being analyzed, such as sales figures, transaction totals, or revenue.
- The fact table includes foreign keys that reference the dimension tables and typically contains numeric facts (e.g., `total_sales`, `quantity_sold`, `revenue`).
- Example: A **Sales Fact** table might have columns like `sale_id`, `product_id`, `store_id`, `date_id`, `amount_sold`, and `total_revenue`.

### 2. Dimension Tables
- **Dimension Tables** provide descriptive attributes that give context to the facts (e.g., product information, store details, time periods).
- In the Snowflake Schema, dimension tables are **normalized**, meaning they are broken down into multiple related tables to remove redundancy.
- Example: The `Product` dimension table might be split into separate tables for `Product`, `Category`, and `Brand`.

### 3. Relationships
- The fact table connects to each normalized dimension table through foreign keys, just like in the Star Schema. However, in a Snowflake Schema, these keys may link to multiple normalized sub-tables in each dimension.
- These normalized tables introduce additional complexity, but they help minimize data redundancy and ensure consistency across the database.

## Example of Snowflake Schema

Let's consider an example of a sales data warehouse that uses a Snowflake Schema:

### Fact Table: Sales Fact
| sale_id | product_id | store_id | date_id  | total_sales | quantity_sold |
|---------|------------|----------|----------|-------------|---------------|
| 1       | 101        | 200      | 20230101 | 500         | 10            |
| 2       | 102        | 201      | 20230102 | 300         | 5             |

### Dimension Table: Product (Normalized)
- **Product Table**
  | product_id | product_name | category_id |
  |------------|--------------|-------------|
  | 101        | Laptop       | 1           |
  | 102        | Smartphone   | 2           |

- **Category Table**
  | category_id | category_name  |
  |-------------|----------------|
  | 1           | Electronics    |
  | 2           | Mobile Devices |

- **Brand Table**
  | brand_id | brand_name |
  |----------|------------|
  | 1        | XYZ        |
  | 2        | ABC        |

### Dimension Table: Store (Normalized)
- **Store Table**
  | store_id | store_name   | location_id |
  |----------|--------------|-------------|
  | 200      | Store A      | 10          |
  | 201      | Store B      | 11          |

- **Location Table**
  | location_id | city        | region |
  |-------------|-------------|--------|
  | 10          | New York    | North  |
  | 11          | Los Angeles | West   |

### Dimension Table: Time
| date_id   | day | month | quarter | year |
|-----------|-----|-------|---------|------|
| 20230101  | 1   | 1     | 1       | 2023 |
| 20230102  | 2   | 1     | 1       | 2023 |

## Advantages of the Snowflake Schema

1. **Reduced Redundancy**:
   - The Snowflake Schema normalizes the dimension tables, which reduces data redundancy by eliminating repeated information. For example, instead of storing the `category_name` in the `Product` table for each product, it is stored only in the `Category` table.

2. **Improved Data Integrity**:
   - By splitting the dimension tables into related sub-tables, the Snowflake Schema enforces a higher level of data integrity and consistency. Changes to a category or brand, for example, only need to be made in one place (the `Category` or `Brand` table), reducing the chance of inconsistencies.

3. **Storage Efficiency**:
   - Normalization leads to smaller dimension tables, which can save storage space, particularly for large datasets with a lot of repeated data.

4. **Easier Updates**:
   - Updates to dimension data (e.g., changes in product category or store location) are easier and less error-prone, as they occur in fewer places.

## Disadvantages of the Snowflake Schema

1. **Increased Complexity**:
   - The Snowflake Schema is more complex than the Star Schema because of its normalized structure, which leads to more tables and relationships. This can make it harder to design, maintain, and query.

2. **Performance Issues**:
   - Queries may require more joins, as data from different normalized tables must be linked together. This can make querying more complex and potentially slower, especially for large datasets.
   - In read-heavy environments like data warehousing and BI, performance may degrade due to the overhead of performing many joins.

3. **Difficult to Understand**:
   - Due to its normalized structure and multiple layers of tables, the Snowflake Schema can be harder to understand for end-users compared to the simpler, denormalized Star Schema.

4. **More Maintenance**:
   - Maintaining the relationships between the multiple normalized tables can be more difficult, particularly if the schema evolves over time. This could result in additional administrative overhead.

![image](https://github.com/user-attachments/assets/d82ff40f-4d48-4447-99f0-ac63c2bb4c08)


# 3.Galaxy Schema (Fact Constellation Schema)

The **Galaxy Schema**, also known as the **Fact Constellation Schema**, is a type of database schema used in data warehousing and business intelligence (BI) systems. It is a more complex version of the **Star Schema** and **Snowflake Schema**, consisting of multiple fact tables that share common dimension tables. This structure is ideal for scenarios where multiple subject areas need to be analyzed together, making it suitable for complex analytical queries.

## Key Components of a Galaxy Schema

### 1. Fact Tables
- **Fact Tables** in a Galaxy Schema are similar to those in the **Star Schema** and **Snowflake Schema** but are typically more than one. Each fact table contains quantitative data (measures) that can be analyzed, such as sales figures, profits, or transaction counts.
- The fact tables in the Galaxy Schema are often linked to the same set of dimension tables, but each fact table might represent a different business process or subject area (e.g., sales, inventory, or order data).
- Example: You could have a **Sales Fact** table and an **Inventory Fact** table, both of which are connected to shared dimension tables like `Product`, `Time`, and `Store`.

### 2. Dimension Tables
- **Dimension Tables** are used to provide context to the facts and allow for filtering and grouping in queries. These tables often contain descriptive attributes like product names, customer information, time periods, or geographical data.
- In the Galaxy Schema, the dimension tables are shared across multiple fact tables, which can lead to a more flexible design that allows for complex analytical queries involving different subject areas.
  
### 3. Relationships
- In the Galaxy Schema, dimension tables are connected to multiple fact tables. This design allows for the integration of multiple business processes in the same schema.
- For example, both the **Sales Fact** table and **Inventory Fact** table might share dimension tables like `Product`, `Store`, and `Time`. However, each fact table will contain its own specific measures.

## Example of a Galaxy Schema

Let's consider an example of a sales and inventory data warehouse that uses a Galaxy Schema:

### Fact Table: Sales Fact
| sale_id | product_id | store_id | date_id  | total_sales | quantity_sold |
|---------|------------|----------|----------|-------------|---------------|
| 1       | 101        | 200      | 20230101 | 500         | 10            |
| 2       | 102        | 201      | 20230102 | 300         | 5             |

### Fact Table: Inventory Fact
| inventory_id | product_id | store_id | date_id  | stock_quantity | stock_value |
|--------------|------------|----------|----------|----------------|-------------|
| 1            | 101        | 200      | 20230101 | 50             | 5000        |
| 2            | 102        | 201      | 20230102 | 30             | 3000        |

### Shared Dimension Table: Product
| product_id | product_name | category   | brand |
|------------|--------------|------------|-------|
| 101        | Laptop       | Electronics| XYZ   |
| 102        | Smartphone   | Electronics| ABC   |

### Shared Dimension Table: Store
| store_id | store_name   | city        | region |
|----------|--------------|-------------|--------|
| 200      | Store A      | New York    | North  |
| 201      | Store B      | Los Angeles | West   |

### Shared Dimension Table: Time
| date_id   | day | month | quarter | year |
|-----------|-----|-------|---------|------|
| 20230101  | 1   | 1     | 1       | 2023 |
| 20230102  | 2   | 1     | 1       | 2023 |

## Advantages of the Galaxy Schema

1. **Flexibility**:
   - The Galaxy Schema supports multiple fact tables, which makes it ideal for complex data models involving multiple business processes or subject areas (e.g., sales, inventory, and order data).
   - This flexibility allows businesses to analyze multiple aspects of their operations together.

2. **Easier to Manage Multiple Facts**:
   - With multiple fact tables sharing common dimension tables, the Galaxy Schema makes it easier to manage different facts that are related but require separate analysis.
   - For example, you can analyze sales and inventory data independently but still link them through common dimensions like `Product` or `Time`.

3. **Integrated Business Processes**:
   - The ability to combine different fact tables into a single schema makes it easier to run complex queries that integrate data across multiple business processes.
   - This integration is particularly useful for multidimensional analysis, such as comparing sales against inventory levels over time.

4. **Efficiency**:
   - The shared use of dimension tables allows for more efficient storage and better performance in querying, as the same dimension table is not duplicated for every fact table.

## Disadvantages of the Galaxy Schema

1. **Complexity**:
   - The Galaxy Schema is more complex than both the Star Schema and Snowflake Schema, as it involves multiple fact tables and relationships. This complexity can make it harder to design, maintain, and query.
   - The presence of multiple fact tables may also result in more complex SQL queries, as users may need to join several fact tables.

2. **Increased Maintenance**:
   - Managing multiple fact tables and the relationships between them requires more effort. Changes in dimension tables or fact tables must be carefully managed to avoid inconsistencies.
   - If new business processes are introduced, it might require adding new fact tables and ensuring proper integration with existing tables.

3. **Performance Overhead**:
   - Queries might require multiple joins between fact tables and dimensions, which can lead to slower performance, particularly when working with large datasets.
   - Optimizing performance in a Galaxy Schema may require careful indexing and query optimization strategies.

4. **Data Integrity Issues**:
   - Ensuring that data across different fact tables is consistent can be challenging, especially when the fact tables represent different business processes.
   - Without proper design and maintenance, the schema could face issues related to data consistency and referential integrity.

![image](https://github.com/user-attachments/assets/7019c15e-e531-443d-a159-fdecb9ea0599)


# 4. Star Cluster Schema

The **Star Cluster Schema** is a variant of the **Star Schema** used in data warehousing and business intelligence (BI). It is designed to optimize performance when multiple fact tables are involved, typically in scenarios where there are related fact tables that share common dimension tables. The **Star Cluster Schema** aims to provide a more flexible and efficient way to manage such complex relationships.

## Key Characteristics of the Star Cluster Schema

The Star Cluster Schema builds on the basic structure of the **Star Schema**, but it incorporates some additional layers of complexity and flexibility:

### 1. Multiple Fact Tables
- Like the **Galaxy Schema** (or **Fact Constellation Schema**), the **Star Cluster Schema** involves multiple fact tables. However, these fact tables are often related and grouped into clusters. These clusters may share common dimension tables and may represent different aspects of the business process (e.g., sales, inventory, order management).
- Each fact table typically focuses on a specific business process, but they are organized in a way that reduces redundancy and maintains performance.

### 2. Clustered Dimensions
- The **Star Cluster Schema** involves dimension tables that may be shared across multiple fact tables. However, instead of having a completely denormalized structure like the traditional **Star Schema**, some of the dimension tables may be grouped or clustered together based on their usage across different fact tables.
- For example, you might have a common `Product` dimension that is shared by different fact tables, but the structure might cluster `Product` with `Time` and `Store` in a sub-schema that is dedicated to analyzing sales and inventory together.

### 3. Grouping of Fact Tables
- Fact tables are grouped into clusters, each representing a subject area or set of related business processes. For example, one cluster might represent the **Sales** process, while another could represent **Inventory Management**. These clusters are optimized to handle specific reporting and analysis tasks.
- Fact tables in the same cluster share dimension tables, and queries typically involve joining fact tables within the same cluster, rather than joining across multiple clusters.

## Example of a Star Cluster Schema

To better understand how the **Star Cluster Schema** might work, consider a business that tracks both sales and inventory data. Both sales and inventory data might share common dimensions such as `Product`, `Store`, and `Time`, but each business process (sales and inventory) would have its own fact tables.

### Fact Table: Sales Fact (Cluster 1)
| sale_id | product_id | store_id | date_id  | total_sales | quantity_sold |
|---------|------------|----------|----------|-------------|---------------|
| 1       | 101        | 200      | 20230101 | 500         | 10            |
| 2       | 102        | 201      | 20230102 | 300         | 5             |

### Fact Table: Inventory Fact (Cluster 1)
| inventory_id | product_id | store_id | date_id  | stock_quantity | stock_value |
|--------------|------------|----------|----------|----------------|-------------|
| 1            | 101        | 200      | 20230101 | 50             | 5000        |
| 2            | 102        | 201      | 20230102 | 30             | 3000        |

### Dimension Table: Product (Cluster 1)
| product_id | product_name | category   | brand |
|------------|--------------|------------|-------|
| 101        | Laptop       | Electronics| XYZ   |
| 102        | Smartphone   | Electronics| ABC   |

### Dimension Table: Store (Cluster 1)
| store_id | store_name   | city        | region |
|----------|--------------|-------------|--------|
| 200      | Store A      | New York    | North  |
| 201      | Store B      | Los Angeles | West   |

### Dimension Table: Time (Cluster 1)
| date_id   | day | month | quarter | year |
|-----------|-----|-------|---------|------|
| 20230101  | 1   | 1     | 1       | 2023 |
| 20230102  | 2   | 1     | 1       | 2023 |

In this example, the **Sales Fact** and **Inventory Fact** tables share the `Product`, `Store`, and `Time` dimensions, and they form the first cluster. Each of these tables focuses on a specific aspect of the business, but the shared dimensions allow for integrated reporting and analysis.

## Advantages of the Star Cluster Schema

### 1. Efficiency in Complex Queries
- The **Star Cluster Schema** allows for efficient querying within each cluster. Since fact tables within a cluster share common dimensions, querying within a cluster is optimized and can be faster than joining across unrelated tables.
- It’s easier to analyze related business processes together, as they are grouped in the same cluster.

### 2. Optimized for Multi-Process Analysis
- By clustering related fact tables together, the **Star Cluster Schema** facilitates the analysis of multiple related processes. For example, you could easily analyze sales alongside inventory data within the same query, as both are part of the same cluster.
- This schema is useful for business scenarios where multiple related aspects of a business need to be analyzed together, such as analyzing **Sales and Profit** or **Inventory and Demand**.

### 3. Reduced Redundancy
- Like the **Galaxy Schema**, the **Star Cluster Schema** reduces redundancy by sharing dimension tables across multiple fact tables.
- It eliminates the need for duplicating dimension tables for each fact table, which can save storage space and improve data consistency.

### 4. Scalability
- The schema can scale well as more fact tables and clusters are added. New business processes can be modeled as new clusters of fact tables, while still reusing existing dimension tables.
- This scalability makes the schema adaptable to the growing needs of the business.

## Disadvantages of the Star Cluster Schema

### 1. Complexity
- The **Star Cluster Schema** is more complex than the standard **Star Schema**. It requires careful design to ensure that related fact tables are grouped properly into clusters.
- The complexity of managing clusters and ensuring that the schema is flexible enough to handle new business processes can be a challenge.

### 2. Performance Overhead
- While queries within a cluster are efficient, there may be some performance overhead when querying across multiple clusters. Since clusters are logically separated, queries that require joining data across clusters may be slower than querying within a single cluster.
- Proper indexing and optimization strategies are required to maintain query performance.

### 3. Increased Maintenance
- Maintaining a **Star Cluster Schema** can be more time-consuming than a simple **Star Schema** due to the complexity of managing multiple clusters.
- Changes to dimension tables or fact tables need to be carefully managed to ensure consistency across clusters.

## Star Cluster Schema vs. Star Schema vs. Galaxy Schema

- **Star Schema**: A simple schema with one fact table and associated dimension tables. It’s easy to understand and design but may struggle with large datasets or multiple business processes.



![image](https://github.com/user-attachments/assets/4d9c7da4-dc3a-46a2-9616-534415abb1c0)








