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

## The E-commerce dataset spanning 2016-2018 comprises:

1. Customers Dataset: Contains customer details and locations, essential for identifying unique customers and delivery addresses in the orders dataset.
2. Geolocation Dataset: Provides Brazilian zip codes with latitude and longitude coordinates, used for spatial mapping and calculating distances between sellers and customers.
3. Order Items Dataset: Includes specifics on purchased items per order, such as product IDs, prices, quantities, and seller information.
4. Payments Dataset: Records payment methods used for orders, detailing payment types, installment plans, and transaction amounts.
5. Order Reviews Dataset: Gathers customer feedback and satisfaction ratings via post-purchase surveys.
6. Order Dataset: Central dataset linking all others, encompassing comprehensive information on each order, including customer, product, payment, and review details.
7. Products Dataset: Offers details about products sold by Olist, featuring product IDs, categories, names, and prices.
8. Sellers Dataset: Provides seller information critical for identifying seller locations and associating them with products fulfilled by Olist.
9. Category Name Translation: Translates product_category_name into English, ensuring clarity and consistency across datasets.





## The ER Diagram for the following tables is as follows: 
![image](https://github.com/rohanshah611/e-commerce_analytics_datawarehouse/assets/47087825/d1d4990e-a048-4a13-a3c1-1a7a77d3d4a6)
 

## The Dimensional Model for the is as follows: 
![Untitled Diagram](https://github.com/rohanshah611/e-commerce_analytics_datawarehouse/assets/47087825/5868789b-d119-4610-9c89-1b557d83d00a)


# Part 2 - Load and enrich data in S3 based Data lake: 

Creating a data lake on Amazon Web Services (AWS) using Simple Storage Service (S3) as the foundation is a strategic approach to managing vast amounts of data. S3 is renowned for its scalability, durability, and security, making it capable of storing diverse data formats, including text, images, videos, and binary files.

A well-designed data lake goes beyond mere storage. It categorizes and processes data efficiently, ensuring it is readily available for analysis and insights. Leveraging the power of S3, businesses can harness the flexibility to store data in various formats—from structured data in relational databases to unstructured data from log files and social media feeds.

This repository will guide you through designing your data lake on AWS S3 using the Medallion architecture. We'll split the data lake into staging  and analytics layers (bronze, silver, and gold S3 buckets) and highlight the use of AWS Glue for efficient ETL processes, creating a robust and scalable solution for your data management and analysis needs.

 ## Step 1: Create S3 Buckets and Load Data

Begin by creating the bronze, silver, and gold S3 buckets.
Load the CSV data into the bronze bucket named ecommerce-bronze.
<img width="1416" alt="Screenshot 2024-06-17 at 7 49 45 AM" src="https://github.com/rohanshah611/e-commerce_analytics_datawarehouse/assets/47087825/01ff6c32-e868-4065-84fd-13e45627a589">
 ## Step 2: Configure IAM Role

Navigate to IAM and create a role that grants access to Glue, S3, and Redshift.
![image](https://github.com/rohanshah611/e-commerce_analytics_datawarehouse/assets/47087825/9f2d7690-6755-431a-911e-13aa93a770ac)

 ## Step 3: Set Up AWS Glue Crawler

In AWS Glue, create a Glue Crawler to scan the data in the bronze S3 bucket.
This will determine the input schema and load the CSV data into a staging Glue database for further processing.

 ## Step 4: Design the ETL Job Using AWS Glue

Proceed to the Visual ETL pipeline in AWS Glue to create the ETL job.
Select the appropriate source Glue crawler dataset and destination (silver bucket) locations.
Provide the transformation logic in the script section, including deduplication, datatype changes, and column renaming.
![image](https://github.com/rohanshah611/e-commerce_analytics_datawarehouse/assets/47087825/ad48ab6c-1871-44da-825d-7b12aea5ed04)

 ## Step 5: Execute ETL from Silver to Gold Bucket

Repeat the ETL process to move data from the silver bucket to the gold bucket.
Transform the data to fit the dimensional model as outlined in Part 1.

## Additional Notes:

AWS Glue pipelines can be configured to run on-demand, on a schedule using cron expressions in Glue Studio, or triggered by events using AWS Lambda.
Each run can incrementally load data using Job bookmarks; however, for this guide, we will perform a bulk upload rather than incremental uploads.
For additional information refer to [this](https://towardsdatascience.com/aws-glue-101-all-you-need-to-know-with-a-real-world-example-f34af17b782f) article. 


# Part 3: Loading Data from S3 Datalake's Gold layer to Redshift cluster

Before proceeding with the data loading process, ensure the following:

## Redshift Cluster:

- You have an existing Amazon Redshift cluster set up and running.(To create a Redshift cluster refer [this](https://medium.com/analytics-vidhya/getting-started-with-aws-redshift-43450cd6286c))
- The cluster configuration meets your data warehousing needs (storage, compute resources).

## AWS Glue Permissions:

- An IAM role is assigned to your AWS Glue service with appropriate permissions.
- This role should allow Glue to access and interact with your Redshift cluster. This includes:
  - Reading and writing data in the Redshift cluster.
  -  Accessing any necessary resources (e.g., S3 buckets) involved in the data transfer.
 
 ## Allow Access to Redshift Clusters by appropriaelty setting up VPC/subnet Security groups:
  - Ensure that the security group associated with Redshift cluster has correct inbound rules. 

## Process Steps: Loading Data into Redshift Glue Database with Delta Handling
1.  Define Redshift Tables:

Design and create tables in Amazon Redshift based on the dimensional model established in Part 1.

2.  Generate Redshift Schema (Optional):

(This step can be skipped if the schema is already known)
Create a crawler in AWS Glue to crawl the existing Redshift tables.
This crawler will automatically discover and define the schema of your Redshift tables within the Glue Data Catalog.

3.  Build ETL Pipeline for Each Table:

Develop separate ETL (Extract, Transform, Load) pipelines in AWS Glue for each of the 5 tables.
Each pipeline will:
Extract data from its designated source (S3 buckets).
Perform any necessary data transformations (cleaning, filtering, etc.).
Load the processed data into the corresponding Redshift table within the Glue database.

4. Manage Delta Loading (New Rows):

Within the Glue ETL job's load step, configure mode to handle delta loading.
This allows you to specify how new data should be integrated with the existing table:
Append: Add new rows to the existing table without modifying existing data.
Update: Identify and update existing rows based on specific criteria (requires a unique identifier).

5.  Repeat for All Tables:

Follow steps 3 and 4 to create and execute ETL pipelines for each of the remaining 4 tables.
By following these steps, you can efficiently load data into your Redshift Glue database, ensuring only new data is added while maintaining the integrity of your existing data.



# Part 4 - Connect the Redshift Datawarehouse to Quicksight for Business Intelligence and reporting:

![image](https://github.com/rohanshah611/e-commerce_analytics_datawarehouse/assets/47087825/a06c7961-5510-473f-9dcb-fe8367edbb50)


# Project Conclusion:
This project successfully established a comprehensive data engineering pipeline for e-commerce transaction data analysis using AWS. By leveraging S3 for a data lake, AWS Glue for ETL, Redshift for data warehousing, and Quicksight for business intelligence, we achieved a scalable, resilient, and secure system capable of providing actionable insights.

 ## AWS Services Used:
 - Amazon S3: For data lake storage.
 
 - AWS Glue: For ETL operations and data cataloging.

 - Amazon Redshift: For data warehousing.
 
 - Amazon QuickSight: For business intelligence and reporting.
 
 - AWS IAM: For managing access and permissions.






