### Store Project

## Requirement

## Project Requirement: Store Analytics Pipeline

## Business Context

Getitech Store is an e-commerce and physical store chain that sells consumer electronics and accesories. The business has two main data sources:

Transactional Data stored in Azure SQL Database

External API Data – a third-party vendor provides daily product pricing and customer comparison in JSON format.

The company wants to centralize, clean, and analyze this data in their Azure Data Lakehouse. Executives want Power BI dashboards for insights into sales, customer behavior, and competitor pricing.

## Data Sources ---> Check the folder "datasets"

# Azure SQL Database (OLTP)

# Tables
Transactions
Shop
products

 
API (JSON, REST endpoint)
products
Customer


Multiple competitor records for each product are returned daily.

## Data Engineering Workflow

# Solutioning 
# Study the requirements
# Check Data Availability and ask relevant questions
# Create the Architecture Diagram

# 1. Ingestion (Bronze Layer)

Use Azure Data Factory (ADF) pipelines to:

Extract data from Azure SQL Database and land as Parquet/Delta in ADLS (Azure Data Lake Storage) Bronze layer.

Call the customer API, store the raw JSON response into ADLS Bronze.

# 2. Processing & Transformation (Silver Layer)

Use Azure Databricks with PySpark + SQL to:

Clean and normalize raw data.

Parse JSON competitor data into structured tables (CompetitorPrices).

Apply schema to SQL tables and enforce data types.

Deduplicate, handle missing values, and join related tables.

Create curated Silver tables.

# 3. Aggregation & Business Models (Gold Layer)

Use Databricks SQL / PySpark to:

Create aggregated views for business consumption. 

Store Gold tables in Delta Lake for easy querying.

# 4. Visualization

Connect Power BI to the Gold Layer in Databricks SQL endpoint.

Build dashboards:

Executive Sales Overview – KPIs: Total Sales, Revenue Growth, Store vs. Online.

Product Performance – Best/Worst performers, category-level trends.

Customer Analytics – High-value customers, churn risk, regional distribution.

# Deliverables

ADF Pipelines for ingestion (SQL + API).

Databricks Notebooks for Silver processing (PySpark + SQL).

Gold-level Aggregations (PySpark/SQL jobs).

Power BI Dashboard connected to Databricks SQL endpoint.
