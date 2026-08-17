# Dataco-supply-chain-sql-analysis
A SQL Server portfolio project that transforms a single flat operational dataset into a normalized relational database, then uses SQL from basic aggregation to CTEs, subqueries, and window functions to answer real business questions around revenue, customer behaviour, product performance, shipping operations, and profitability.

---

## Table of Contents
1. [Project Overview](#project-overview)
2. [Business Problem](#business-problem)
3. [Objectives](#objectives)
4. [Dataset](#dataset)
5. [Database Design](#database-design)
6. [Data Preparation & Validation](#data-preparation--validation)
7. [SQL Analysis](#sql-analysis)
8. [Key Findings](#key-findings)
9. [Business Insights](#business-insights)
10. [Recommendations](#recommendations)
11. [Tools Used](#tools-used)
12. [Repository Structure](#repository-structure)
13. [Documentation](#documentation)
14. [Conclusion](#conclusion)


## Project Overview

This project analyses the **DataCo Supply Chain dataset** using Microsoft SQL Server to examine sales performance, customer spending, profitability and shipping operations.

The project started with a raw dataset containing **180,519 records and 53 columns**, covering transactions from **1 January 2015 to 31 January 2018**. Rather than analysing the raw data as one large table, I first examined its structure and separated the information into seven related tables: **Customers, Products, Categories, Departments, Orders, Order_Details and Shipping**.

The database was then structured using primary and foreign keys to establish relationships between the tables. This made it possible to analyse information at the appropriate level, such as linking customers to their orders, orders to individual order details, and products to their respective categories and departments.

After the database was created, I carried out data validation checks to confirm that the tables, records and relationships were working as expected. The validated database was then used to answer business questions around revenue, customer performance, profitability and delivery operations.

The analysis also includes advanced SQL techniques such as **Common Table Expressions (CTEs), window functions, ranking, subqueries, aggregate functions and date functions**. These were used to investigate areas such as the highest-revenue customers, cumulative revenue over time, customers spending above the average and changes in monthly revenue.

The purpose of the project was not simply to demonstrate SQL syntax. The focus was on using SQL to turn a large supply chain dataset into structured information that can be interpreted in a business context and used to identify areas requiring further attention.


## Business Problem

The DataCo Supply Chain dataset contains detailed information on customers, orders, products, departments and shipping activity, but the raw structure makes it difficult to assess business performance directly.

The main challenge was to determine where revenue was being generated, how customer spending was distributed, which products and departments were contributing to revenue and profit, and where delivery performance required attention.

The analysis therefore focused on turning the raw transactional data into a structured SQL database and using that database to answer specific business questions. These included identifying high-revenue customers, examining revenue and profitability across different business areas, assessing shipping performance and understanding how revenue changed over time.

A further consideration was the reliability of the analysis. Customer names, for example, were not sufficient to identify individual customers because the dataset contained multiple records with the same name. CustomerID was therefore used as the customer-level identifier when analysing individual customer spending.

The overall business problem was to move from a large and difficult-to-analyse raw dataset to reliable, business-focused information that could help identify performance patterns, operational issues and areas requiring further investigation.


## Objectives

The main objectives of the project were to:

1. **Transform the raw dataset into a structured relational database** by separating the data into appropriate tables and establishing relationships between related entities.

2. **Establish and validate primary and foreign key relationships** to ensure that records could be connected correctly across customers, orders, products, departments and shipping information.

3. **Validate the transformed data** by checking record counts, null values, key relationships and other data-quality issues before carrying out the analysis.

4. **Analyse revenue and profitability** to identify the departments, categories, products and customers contributing to business performance.

5. **Evaluate customer spending patterns** by identifying the highest-revenue customers and determining how many customers spend above the average customer spend.

6. **Assess shipping and delivery performance** by comparing delivery outcomes across shipping modes and identifying areas with high late-delivery rates.

7. **Apply advanced SQL techniques** including CTEs, window functions, ranking, subqueries and date functions to answer more detailed business questions.

8. **Translate the SQL results into business insights and recommendations** that distinguish between what the data directly shows and areas that require further investigation.


## Dataset

The project uses the **DataCo Supply Chain dataset**, which contains transactional information covering customers, orders, products, departments, categories and shipping activity.

The original dataset contained **180,519 records across 53 columns**, with transaction dates ranging from **1 January 2015 to 31 January 2018**.

The raw data included information such as:

* Customer details and customer segments
* Order and order-item information
* Product names, prices and categories
* Department and category information
* Sales and profit-related fields
* Order locations and markets
* Shipping modes and delivery status
* Scheduled and actual shipping information

For the project, the raw dataset was reorganised into a relational database containing **seven tables**:

| Table         | Purpose                                                            |
| ------------- | ------------------------------------------------------------------ |
| Customers     | Stores customer information                                        |
| Products      | Stores product information and category relationships              |
| Categories    | Stores product category information                                |
| Departments   | Stores department information                                      |
| Orders        | Stores order-level information and customer relationships          |
| Order_Details | Stores individual products and financial details within each order |
| Shipping      | Stores shipping and delivery information                           |

The dataset was used as the foundation for both the database design and the subsequent SQL analysis. The original raw structure was retained for reference, while the seven-table relational structure was used for the business analysis.


## Database Design

The original dataset was reorganised into a relational database to make the data easier to manage, query and analyse. Instead of keeping all information in one large table, related fields were separated into seven tables based on the entities they represented.

The final database consists of:

* **Customers** — stores customer information and identifies each customer using `CustomerID`.
* **Products** — stores product details, including product name, price, status and category.
* **Categories** — stores product categories and links them to their respective departments.
* **Departments** — stores the department structure used to group product categories.
* **Orders** — stores order-level information, including the customer, order date, location, market and order status.
* **Order_Details** — stores the individual products within each order, including quantity, unit price, discounts, line revenue and profit.
* **Shipping** — stores shipping and delivery information, including shipping date, shipping mode, scheduled shipping days, actual shipping days and delivery status.

Primary keys were established to uniquely identify records within the tables, while foreign keys were used to connect related entities. For example, `CustomerID` links customers to their orders, `OrderID` links orders to their order details and shipping records, and `ProductID` links order details to the relevant product.

This structure allowed the analysis to be performed at different levels, from individual order items and products to customers, departments and shipping operations, while maintaining the relationships between the underlying records.

### Entity Relationship Diagram

The final database structure is represented in the ERD below, showing the tables and the relationships established between them.

![DataCo Supply Chain Database ERD](Images/DataCo_ERD.png)


## Data Preparation & Validation

The raw dataset was prepared before the business analysis was carried out. The main focus was to organise the data into appropriate entities, remove fields that were not required for the analysis and create a structure that could be queried reliably.

Customer information was separated from order, product and shipping information, while related fields were moved into their appropriate tables. Column names were also standardised to make the database easier to understand and query. Fields that were not required for the project, such as customer passwords and unnecessary personal details, were excluded from the final database structure.

The transformed data was then loaded into the seven relational tables. Primary keys were created to identify individual records, and foreign keys were established to maintain relationships between the tables.

### Data Validation

Validation was carried out before the business analysis to ensure that the database was producing reliable results. This included checking:

* Record counts across the created tables.
* Null values in important fields.
* Primary key uniqueness.
* Foreign key relationships.
* Referential integrity between related tables.
* Date fields and the overall date range.
* Whether records could be correctly joined across the database.

These checks also helped identify and resolve issues encountered during the database creation and loading process, including duplicate records, null values in required fields and incorrect or repeated insert operations.

The final validated database contained **seven related tables**, which were then used for the business and advanced SQL analysis.


## SQL Analysis

The SQL analysis was divided into two main areas: **business analysis** and **advanced SQL analysis**.

### Business Analysis

The business analysis focused on answering practical questions about the performance of the supply chain business. The analysis covered areas including:

* Revenue performance across departments and categories.
* Product revenue and profitability.
* Customer revenue and spending patterns.
* Regional and geographical performance.
* Shipping mode and delivery performance.
* Late-delivery risk.
* Monthly and yearly revenue trends.

These analyses were designed to move beyond simply retrieving data and instead identify patterns that could be interpreted in a business context.

### Advanced SQL Analysis

Advanced SQL techniques were then used to answer more detailed questions and examine patterns over time and across customers.

The analysis included:

* **Top 10 customers by revenue** — identifying individual customers with the highest revenue contribution using `CustomerID` as the customer-level identifier.
* **Cumulative revenue over time** — using a CTE and window function to calculate monthly revenue and cumulative revenue from the beginning of the dataset.
* **Customers spending above average** — calculating the average customer spend and identifying customers whose total spending exceeded that benchmark.
* **Monthly revenue movement** — comparing revenue across months to understand changes in performance over time.
* **Revenue and profitability analysis** — comparing performance across relevant business entities to understand where revenue and profit were being generated.

### SQL Techniques Used

The project applied a range of SQL techniques, including:

* `INNER JOIN` and table relationships
* `GROUP BY` and aggregate functions
* Common Table Expressions (CTEs)
* Subqueries
* Window functions
* `DENSE_RANK()`
* Date functions such as `YEAR()` and `MONTH()`
* Conditional filtering
* Revenue and percentage calculations
* Currency formatting using `FORMAT()`

The complete SQL scripts are included in the repository so that the analysis can be reviewed and reproduced.
