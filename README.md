# SQL Data Analytics Project

A SQL Server–based analytics project focused on exploring a retail sales dataset, building a lightweight data warehouse, and running business-oriented analysis using SQL. The project is structured as a hands-on learning exercise in dimensional modeling, data exploration, KPI calculation, trend analysis, segmentation, and reporting.

## Project Overview

This repository contains a complete example of how to:

- create a database and core analytical schemas,
- load curated CSV datasets into a SQL Server warehouse,
- investigate the structure of the data,
- calculate sales and customer metrics,
- analyze trends over time,
- segment customers and products,
- rank top-performing entities,
- generate report-style views for operational analysis.

The project uses a gold-layer schema with a star-like design based on three main entities:

- customers,
- products,
- sales transactions.

This makes it a good reference for SQL analytics workflows, business intelligence questions, and data warehouse learning exercises.

## Business Context

The dataset represents a fictional retail and sales environment with:

- customer information,
- product catalog details,
- sales transaction records,
- historical ordering and shipping dates,
- pricing and quantity data.

The objective is to transform raw information into analytical insight by examining:

- revenue generation,
- customer behavior,
- product performance,
- time-based changes in sales,
- customer and product segmentation,
- contribution of categories to total sales.

## Repository Structure

```text
SQL_Data_Analytics/
├── README.md
├── datasets/
│   ├── DataWarehouseAnalytics.bak
│   └── csv_files/
│       ├── gold.dim_customers.csv
│       ├── gold.dim_products.csv
│       ├── gold.fact_sales.csv
│       └── ... additional silver/bronze source files
├── scripts/
│   ├── 00_init_database.sql
│   ├── 01_database_exploration.sql
│   ├── 02_dimensions_exploration.sql
│   ├── 03_date_range_exploration.sql
│   ├── 04_measures_exploration.sql
│   ├── 05_magnitude_analysis.sql
│   ├── 06_ranking_analysis.sql
│   ├── 07_change_over_time_analysis.sql
│   ├── 08_cumulative_analysis.sql
│   ├── 09_performance_analysis.sql
│   ├── 10_data_segmentation.sql
│   ├── 11_part_to_whole_analysis.sql
│   ├── 12_report_customers.sql
│   ├── 13_report_products.sql
│   └── placeholder
└── ...
```

## Data Model

The warehouse is built in the gold schema and contains the following main tables:

### 1. gold.dim_customers

Customer dimension table.

Key fields include:

- customer_key
- customer_id
- customer_number
- first_name
- last_name
- country
- marital_status
- gender
- birthdate
- create_date

This table holds customer profile information and supports segmentation by geography, age, and demographics.

### 2. gold.dim_products

Product dimension table.

Key fields include:

- product_key
- product_id
- product_number
- product_name
- category_id
- category
- subcategory
- maintenance
- cost
- product_line
- start_date

This table supports category and product analysis such as revenue ranking, profitability review, and product categorization.

### 3. gold.fact_sales

Sales fact table.

Key fields include:

- order_number
- product_key
- customer_key
- order_date
- shipping_date
- due_date
- sales_amount
- quantity
- price

This is the transactional layer used to calculate sales performance, KPIs, and time-based trends.

## Dataset Files

The project includes both raw source files and curated gold-layer CSVs.

### CSV datasets

The CSV files under datasets/csv_files include:

- source bronze and silver data files,
- gold.dim_customers.csv,
- gold.dim_products.csv,
- gold.fact_sales.csv,
- export files used to build analytical views.

The script files use the gold-level tables as the primary analytical dataset.

### Backup file

The repository also contains DataWarehouseAnalytics.bak, which can be used to restore the database if a backup is needed.

## Prerequisites

To run this project successfully, you need:

- Microsoft SQL Server (preferably SQL Server 2019 or newer)
- SQL Server Management Studio (SSMS) or Azure Data Studio
- access to create/drop databases and schemas
- local file access for BULK INSERT operations
- enough permissions to read CSV files from the configured path

## Setup and Execution

### 1. Open the project in SQL Server tools

Open SQL Server Management Studio and connect to your SQL Server instance.

### 2. Update file paths in the database initialization script

The initialization script uses a fixed BULK INSERT path:

```sql
C:\sql\sql-data-analytics-project\datasets\csv-files\gold.dim_customers.csv
```

In this workspace, the actual folder is named datasets/csv_files, not csv-files. You should update the paths in 00_init_database.sql to match your local path before executing the script.

Example adjustment:

```sql
FROM 'C:\path\to\SQL_Data_Analytics\datasets\csv_files\gold.dim_customers.csv'
```

This is an important setup step because SQL Server BULK INSERT requires a valid local filesystem path.

### 3. Run the database creation script

Execute the scripts in the following order:

1. 00_init_database.sql
2. 01_database_exploration.sql
3. 02_dimensions_exploration.sql
4. 03_date_range_exploration.sql
5. 04_measures_exploration.sql
6. 05_magnitude_analysis.sql
7. 06_ranking_analysis.sql
8. 07_change_over_time_analysis.sql
9. 08_cumulative_analysis.sql
10. 09_performance_analysis.sql
11. 10_data_segmentation.sql
12. 11_part_to_whole_analysis.sql
13. 12_report_customers.sql
14. 13_report_products.sql

## Script Breakdown

### 00_init_database.sql

Creates the DataWarehouseAnalytics database, creates the gold schema, defines the main tables, and loads the gold CSV files into the warehouse.

### 01_database_exploration.sql

Inspects table metadata and schema details using INFORMATION_SCHEMA. This is useful for understanding the database structure and validating columns.

### 02_dimensions_exploration.sql

Explores the dimensions by extracting unique customer countries and product categories/subcategories.

### 03_date_range_exploration.sql

Looks at the earliest and latest order dates and calculates the data coverage window.

### 04_measures_exploration.sql

Calculates high-level business KPIs such as:

- total sales,
- total quantity,
- average price,
- total orders,
- total products,
- total customers.

### 05_magnitude_analysis.sql

Measures distribution across categories and customer groups, including:

- customers by country,
- customers by gender,
- products by category,
- average product cost by category,
- revenue by category,
- revenue by customer,
- quantity sold by country.

### 06_ranking_analysis.sql

Ranks products and customers by revenue and order counts to surface top and weakest performers.

### 07_change_over_time_analysis.sql

Analyzes sales behavior over time using year/month aggregations and SQL date functions.

### 08_cumulative_analysis.sql

Calculates cumulative totals and moving average values to understand long-term trends.

### 09_performance_analysis.sql

Measures year-over-year and product-level performance using LAG and window functions.

### 10_data_segmentation.sql

Segments products and customers using conditional logic, including cost ranges and customer value tiers such as VIP, Regular, and New.

### 11_part_to_whole_analysis.sql

Shows how categories contribute to the total sales mix, providing a part-to-whole perspective.

### 12_report_customers.sql

Creates a customer reporting view called gold.report_customers. It consolidates metrics such as:

- customer age,
- age groups,
- customer segments,
- recency,
- total orders,
- total sales,
- total quantity,
- total products,
- average order value,
- average monthly spend.

### 13_report_products.sql

Creates a product reporting view called gold.report_products. It consolidates product-level metrics such as:

- total sales,
- total quantity,
- total customers,
- recency,
- product segments,
- average selling price,
- average order revenue,
- average monthly revenue.

## Analytics Topics Covered

This project demonstrates a broad set of SQL analytics skills, including:

- database creation and schema setup,
- schema discovery and metadata inspection,
- grouping and aggregation,
- date and time analysis,
- customer and product segmentation,
- ranking and top-N analysis,
- part-to-whole analysis,
- cumulative metrics,
- window functions,
- KPI reporting through views.

## Typical Business Questions Answered

This project is designed to answer questions such as:

- Which countries have the most customers?
- Which product categories generate the most revenue?
- Who are the top revenue-generating customers?
- Which products rank highest in sales?
- How do sales trends evolve over time?
- Which customer segments are most valuable?
- What share of total sales comes from each category?
- How do monthly and yearly sales compare?

## Notes for Learning and Customization

This repository is intended as an educational SQL analytics project. The scripts are designed to be readable and practical, with a focus on demonstrating common analytical patterns in T-SQL.

A few considerations:

- path configuration for BULK INSERT must be adjusted per environment,
- some scripts are structured as demonstration examples and may require minor verification before use in production,
- if you are adapting the project to a different SQL Server setup, review file paths, database naming, and schema ownership first.

## Recommended Workflow

For a beginner-friendly progression, use the project in this order:

1. load the database,
2. inspect schema and dimension values,
3. compute basic KPIs,
4. explore trends and distributions,
5. apply ranking and segmentation,
6. review the final customer/product reporting views.

This sequence makes it easier to understand how a simple analytical warehouse evolves from raw data to business insight.

## Summary

The SQL_Data_Analytics project is a practical, end-to-end exercise in SQL-based business intelligence. It combines schema creation, data loading, exploratory analysis, KPI calculation, segmentation, time-series analysis, and reporting in a compact and accessible format.

It is especially well suited for:

- learning SQL analytics,
- understanding fact and dimension tables,
- practicing aggregation and window functions,
- creating business reports from a sample data warehouse.

---

This project is a strong foundation for extending into more advanced SQL analytics, dashboarding, or data warehouse design work.
