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
