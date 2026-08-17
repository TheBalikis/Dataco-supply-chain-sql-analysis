# Dataco-supply-chain-sql-analysis
A SQL Server portfolio project that transforms a single flat operational dataset into a normalized relational database, then uses SQL from basic aggregation to CTEs, subqueries, and window functions to answer real business questions around revenue, customer behaviour, product performance, shipping operations, and profitability.

---

## Table of Contents
- [Project Overview](#project-overview)
- [Business Problem](#business-problem)
- [Objectives](#objectives)
- [Dataset](#dataset)
- [Database Design](#database-design)
- [Data Preparation & Validation](#data-preparation--validation)
- [SQL Analysis](#sql-analysis)
- [Key Findings](#key-findings)
- [Business Insights](#business-insights)
- [Conclusion](#conclusion)
- [Recommendations](#recommendations)
- [Limitations](#limitations)
- [Future-Analysis](#future-analysis)
- [Tools Used](#tools-used)

---

## Project Overview
This project analyses the **DataCo Supply Chain dataset** using Microsoft SQL Server to examine sales performance, customer spending, profitability and shipping operations.

The project started with a raw dataset containing **180,519 records and 53 columns**, covering transactions from **1 January 2015 to 31 January 2018**. Rather than analysing the raw data as one large table, I first examined its structure and separated the information into seven related tables: **Customers, Products, Categories, Departments, Orders, Order_Details and Shipping**.

The database was then structured using primary and foreign keys to establish relationships between the tables. This made it possible to analyse information at the appropriate level, such as linking customers to their orders, orders to individual order details, and products to their respective categories and departments.

After the database was created, I carried out data validation checks to confirm that the tables, records and relationships were working as expected. The validated database was then used to answer business questions around revenue, customer performance, profitability and delivery operations.

The analysis also includes advanced SQL techniques such as **Common Table Expressions (CTEs), window functions, ranking, subqueries, aggregate functions and date functions**. These were used to investigate areas such as the highest-revenue customers, cumulative revenue over time, customers spending above the average and changes in monthly revenue.

The purpose of the project was not simply to demonstrate SQL syntax. The focus was on using SQL to turn a large supply chain dataset into structured information that can be interpreted in a business context and used to identify areas requiring further attention.


---

## Business Problem

The DataCo Supply Chain dataset contains detailed information on customers, orders, products, departments and shipping activity, but the raw structure makes it difficult to assess business performance directly.

The main challenge was to determine where revenue was being generated, how customer spending was distributed, which products and departments were contributing to revenue and profit, and where delivery performance required attention.

The analysis therefore focused on turning the raw transactional data into a structured SQL database and using that database to answer specific business questions. These included identifying high-revenue customers, examining revenue and profitability across different business areas, assessing shipping performance and understanding how revenue changed over time.

A further consideration was the reliability of the analysis. Customer names, for example, were not sufficient to identify individual customers because the dataset contained multiple records with the same name. CustomerID was therefore used as the customer-level identifier when analysing individual customer spending.

The overall business problem was to move from a large and difficult-to-analyse raw dataset to reliable, business-focused information that could help identify performance patterns, operational issues and areas requiring further investigation.


---

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


---

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


---

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


---

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


---

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


---

## Key Findings

The analysis identified several patterns across customer spending, revenue performance, profitability and delivery operations.

### Customer Performance

* **Mary Smith (CustomerID 791)** ranked first among the top 10 customers by revenue, generating **$9,436.61**.
* Revenue across the top 10 customers was relatively evenly distributed, ranging from **$9,436.61 to $7,869.02**, with no major gap between the highest-ranking customers.
* **8,983 of 20,652 purchasing customers (43.5%)** spent above the average customer spend of **$1,600.54**.

### Revenue and Profitability

* Revenue and profitability varied across departments, categories and products, highlighting differences between sales performance and actual profit contribution.
* The analysis showed the importance of considering **profit and profit margin alongside revenue** when evaluating product and category performance.

### Shipping and Delivery

* **First Class recorded a 95.27% late-delivery rate**, making it a notable area for further operational investigation.
* Delivery performance varied across shipping-related segments, indicating that shipping outcomes should be assessed alongside other factors such as destination and scheduled delivery requirements rather than by shipping mode alone.

### Revenue Trends

* Monthly revenue was analysed alongside cumulative revenue to show how overall revenue developed throughout the period.
* The cumulative revenue analysis provided a clearer view of long-term growth, while month-to-month analysis highlighted changes that could be hidden by the cumulative total.

Overall, the findings show that the dataset contains meaningful differences across customers, products, profitability and delivery performance, while also highlighting areas where further analysis would be required before making causal conclusions.


---

## Business Insights

The analysis identified several findings relevant to revenue performance, customer value, profitability and operational efficiency. Rather than simply reporting the results, the findings were considered in terms of what they could mean for business decision-making.

### 1. Revenue Distribution Across Departments and Regions

Revenue performance was not evenly distributed across departments, regions and customers. **Fan Shop** generated the highest departmental revenue, while **Western Europe** was the strongest region by revenue.

This indicates that some areas of the business contribute more substantially to overall sales than others. Understanding the factors behind this performance could help management identify practices, products or market conditions that may be relevant to weaker-performing areas.

However, the results show differences in revenue contribution rather than proving that revenue is highly concentrated. A more detailed concentration analysis would be required to determine how much of total company revenue is generated by the highest-performing entities.

### 2. Customer Dependency and Retention Strategy

The top-spending customers showed a relatively balanced revenue contribution, with no single customer standing significantly above the others. This suggests that, within the top 10 customers, the business is not heavily dependent on one high-value customer.

The wider customer analysis also found that **8,983 of 20,652 purchasing customers (43.5%)** spent above the average customer spend of **$1,600.54**. This indicates that above-average spending is not limited to a small group of customers.

From a management perspective, this supports a broader customer retention and value-building approach rather than focusing exclusively on a small VIP segment. However, the top-10 analysis alone is not enough to establish overall customer concentration. Comparing the combined revenue of the top 1%, 5% or 10% of customers with total company revenue would provide a stronger measure of customer dependency and potential revenue risk.

### 3. Profitability Does Not Always Follow Revenue

The profitability analysis showed that **Fishing** generated the highest profit among the categories analysed.

This highlights why revenue should not be used as the only measure of business performance. A product or category can generate substantial sales without necessarily producing the highest profit. Management should therefore consider revenue alongside **profit, profit margin and average order value** when evaluating product and category performance.

### 4. First Class Delivery Performance Requires Attention

**First Class recorded a 95.27% late-delivery rate**, making it the most significant delivery-performance concern identified in the analysis.

The result does not by itself explain why deliveries were late or establish that shipping mode was the cause. However, it provides a clear area for further investigation. Management could examine factors such as shipping schedules, destinations, order volumes and fulfilment processes to determine what may be contributing to the high rate.

### 5. Revenue Growth Was Positive but Not Consistent

Cumulative revenue increased over the period analysed, indicating overall growth across the dataset. However, the monthly analysis showed that revenue could increase or decrease from one month to the next.

Overall growth should therefore not be interpreted as consistent month-to-month performance. Monitoring monthly changes alongside cumulative revenue would help management identify periods of weaker performance and investigate the factors behind those changes.

### Overall Business Insight

The overall business problem was to convert a large, unstructured dataset into reliable, business-focused information — capable of surfacing performance patterns, operational issues and areas needing further investigation.

The most important areas for further attention are **customer retention and value development, product profitability, revenue concentration and delivery performance**, particularly the unusually high late-delivery rate associated with First Class shipments.


---

## Conclusion

This project analysed the DataCo Supply Chain dataset using SQL Server, beginning with the preparation and restructuring of the raw dataset into a relational database and progressing through data validation, business analysis and advanced SQL analysis.

The analysis identified differences in revenue performance across customers, departments and regions, alongside important findings relating to profitability and delivery performance. The advanced SQL analysis provided further insight into customer revenue rankings, cumulative revenue growth, above-average customer spending and month-to-month revenue movement.

One of the most significant operational findings was the **95.27% late-delivery rate recorded for First Class shipments**. While this is a notable finding, the analysis is descriptive and does not establish that shipping mode itself causes delivery delays. Further statistical analysis would be required to determine which factors are associated with late delivery and whether the observed differences remain significant after accounting for other variables.

The customer analysis also showed that revenue among the highest-spending customers was relatively evenly distributed, while **43.5% of purchasing customers spent above the average customer spend of $1,600.54**. These findings suggest that customer value extends across a broad portion of the customer base rather than being limited to a small group of standout accounts. However, a more detailed customer concentration analysis would be required to determine the proportion of total company revenue generated by the highest-value customers.

Overall, the project demonstrates how SQL can be used to move from a large and unstructured dataset to a relational database and then translate that data into business-focused analysis. The results provide a foundation for further investigation into customer concentration, profitability drivers and delivery performance, while ensuring that business decisions are based on evidence rather than assumptions.


---

## Recommendations

### 1. Review First Class Delivery Performance

First Class recorded a **95.27% late-delivery rate** in the dataset. This is a strong descriptive finding, but the analysis does not establish whether shipping mode itself is responsible for the delays.

Management should investigate delivery performance across shipping modes while considering factors such as destination, scheduled shipping days, order volume and order characteristics. This would help determine whether the high late-delivery rate is associated with the shipping mode itself or with other operational factors.

### 2. Monitor Customer Value and Concentration

The top 10 customers showed relatively similar revenue levels, with no single customer generating substantially more revenue than the others. In addition, **43.5% of purchasing customers spent above the average customer spend of $1,600.54**.

Rather than focusing only on individual high-value customers, management should monitor customer value across the wider customer base. Comparing the revenue contribution of the top 1%, 5% and 10% of customers against total company revenue would also provide a clearer measure of customer concentration and potential revenue risk.

### 3. Investigate the Drivers of Regional and Departmental Performance

**Western Europe** generated the highest regional revenue, while **Fan Shop** was the strongest department by revenue. These results identify strong-performing areas, but the analysis does not establish why they are performing better than other regions or departments.

Management should compare order volume, product mix, customer demand and purchasing patterns across regions and departments. This would help determine whether the observed differences are driven by sustained demand, product composition or a smaller number of high-value transactions.

### 4. Establish Regular Revenue Performance Monitoring

The analysis showed overall cumulative revenue growth alongside month-to-month fluctuations. Monitoring cumulative revenue alone could therefore hide periods of weaker performance.

A regular monthly performance review should track revenue, month-on-month growth and significant changes against previous periods. Where a material decline occurs, management can investigate the underlying product, regional or customer-level drivers and respond accordingly.


---

---

## Limitations

1. **Non-unique customer names.** The dataset contains a large number of duplicate `CustomerName` values (1,721 customers are named "Mary Smith" alone). Any analysis grouping by name rather than `CustomerID` will produce materially incorrect results. This was identified and corrected during the analysis, but it highlights a broader data quality characteristic of the dataset that should be accounted for in any further work.

2. **Descriptive, not causal, analysis.** The project uses descriptive SQL analysis (aggregation, ranking, window functions) rather than statistical or causal modelling. Findings such as the 95.27% First Class late-delivery rate describe a pattern in the data but do not establish that shipping mode itself causes delays — other factors (destination, order volume, scheduling) were not controlled for.

3. **Limited scope of customer concentration analysis.** The customer revenue analysis was based on the top 10 customers and an above/below-average split. This gives a useful directional picture but doesn't fully quantify revenue concentration — a proper concentration measure (e.g., revenue share held by the top 1%, 5%, and 10% of customers) would give a more precise answer.

4. **No time-based customer segmentation.** The analysis treats customer spending as a static, all-time total. It doesn't account for customer tenure, recency, or changes in spending behaviour over time.

5. **No predictive or machine learning component**, as stated in the original project scope — the work is limited to descriptive and diagnostic SQL analysis.

---

## Future Analysis

1. Quantify true revenue concentration by calculating the % of total revenue held by the top 1%, 5%, and 10% of customers.
2. Investigate the drivers of the First Class late-delivery rate using a controlled comparison (e.g., delivery performance by shipping mode within the same region or order size).
3. Build a customer segmentation model (RFM — recency, frequency, monetary value) to move beyond a static above/below-average split.
4. Extend the monthly revenue trend analysis with year-over-year comparisons and seasonality decomposition.

---

## Tools Used

* **Microsoft SQL Server** — Database creation, table design, relationships, data validation and SQL analysis.
* **SQL Server Management Studio (SSMS)** — Writing, executing and testing SQL queries and managing the database.
* **Microsoft Excel** — Initial inspection and preparation of the raw dataset before importing it into SQL Server.



