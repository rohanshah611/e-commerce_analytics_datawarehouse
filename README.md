# E-Commerce Data Analysis with S3 Data Lake and Redshift Data Warehouse

## Project overview: This project focuses on building a robust data engineering pipeline on AWS for analyzing e-commerce transaction data. The pipeline is logically divided into four parts:

### Part 1: Converting Data Model

- Transform transactional data into a dimensional model optimized for analytics, employing a star schema for efficient querying and reporting.

### Part 2: Data Lake on S3

- Load the Kaggle [Brazilian E-Commerce Public Dataset](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce?select=product_category_name_translation.csv) by Olist into an S3 bucket as CSV files.
- Utilize S3 as a data lake with a Medalian architecture, where data is processed through Bronze (raw), Silver (cleaned), and Gold (analytics-ready) layers using AWS Glue for all 
 ETL operations, aligning the data with the dimensional model from Part 1.

### Part 3: Redshift Data Warehouse

- Create a Redshift cluster and load the processed data from the S3 Gold layer into the data warehouse using AWS Glue.
- Redshift is scalable, handling varying workloads seamlessly, and fault-tolerant with automated backups and replication. It ensures data security with encryption at rest and in transit, alongside robust access controls.
  
### Part 4: Business Intelligence with Quicksight

- Load the analytics-ready data from the Gold layer into Quicksight.
- Create interactive dashboards and reports for business intelligence and actionable insights.
  
This project demonstrates a comprehensive data engineering workflow, leveraging AWS services like S3, Glue, Redshift, and Quicksight for scalable, resilient, and secure data analytics.




# Part 1 - ER Model to Dimensional Model 

Converting data from an ER model to a dimensional model, using Kimball's star schema, enhances data analysis. ER models, with their focus on detailed relationships, are complex and slow analysis. Dimensional models simplify data into categories and measures, speeding up retrieval and boosting performance for insights. Kimball's star schema organizes data around dimensions and a central fact table, accelerating analysis and enhancing decision-making with improved computing efficiency. For more detail on Kimball's star schema, [click here](https://www.holistics.io/books/setup-analytics/kimball-s-dimensional-data-modeling/).

The E-commerce dataset spanning 2016-2018 comprises:

1. Customers Dataset: Contains customer details and locations, essential for identifying unique customers and delivery addresses in the orders dataset.
2. Geolocation Dataset: Provides Brazilian zip codes with latitude and longitude coordinates, used for spatial mapping and calculating distances between sellers and customers.
3. Order Items Dataset: Includes specifics on purchased items per order, such as product IDs, prices, quantities, and seller information.
4. Payments Dataset: Records payment methods used for orders, detailing payment types, installment plans, and transaction amounts.
5. Order Reviews Dataset: Gathers customer feedback and satisfaction ratings via post-purchase surveys.
6. Order Dataset: Central dataset linking all others, encompassing comprehensive information on each order, including customer, product, payment, and review details.
7. Products Dataset: Offers details about products sold by Olist, featuring product IDs, categories, names, and prices.
8. Sellers Dataset: Provides seller information critical for identifying seller locations and associating them with products fulfilled by Olist.
9. Category Name Translation: Translates product_category_name into English, ensuring clarity and consistency across datasets.





