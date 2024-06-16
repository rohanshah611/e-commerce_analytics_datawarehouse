# E-Commerce_analytics_datawarehouse

Project Scope: Sales Data Insights for E-Commerce
This GitHub project aims to demonstrate expertise in constructing a scalable, resilient, and secure data analytics pipeline using the following AWS services: S3 (data lake), Glue (ETL), Redshift (data warehouse), and Quicksight (business intelligence). The project is designed to generate actionable executive insights from sales data of an e-commerce website, using best architecture principles.

Data Source:
Dataset: Kaggle's Brazilian E-Commerce Public Dataset by Olist
Format: CSV
Architecture:
  Data Lake on S3:
  
  1)Bronze Layer: Raw data is ingested into the Bronze bucket.
  
  2)Silver Layer: Data is cleaned, transformed, and stored in the Silver bucket.
  
  3)Gold Layer: Analytics-ready data is stored in the Gold bucket.

  ETL Pipelines Using Glue:

  1)Extract raw data from the S3 Bronze layer.
  
  2)Transform and clean data, then load it into the S3 Silver layer.
  
  3)Further refine and process data, loading the final analytics-ready data into the S3 Gold layer.
    
Data Warehouse Using Redshift:

  Load the analytics-ready data from the S3 Gold layer into Redshift.
  Ensure data is optimized for query performance and scalability.
Business Intelligence Using Quicksight:

  Connect Quicksight to Redshift.
  Create interactive dashboards and visualizations to generate actionable executive insights.
Goals:
  Scalability: The architecture should handle varying data volumes efficiently.
  Resilience: Ensure data processing and storage solutions are robust and fault-tolerant.
  Security: Implement strong security measures to protect data at rest.
Deliverables:
Code Repository: Well-documented codebase showcasing the implementation of the data lake, ETL pipelines, data warehouse, and business intelligence dashboards.
Architecture Diagrams: Visual representations of the data flow and architecture.
Documentation: Comprehensive guide on how to set up and run the project, including prerequisites, configuration steps, and usage instructions.
Sample Dashboards: Quicksight dashboards demonstrating key sales insights and metrics.
