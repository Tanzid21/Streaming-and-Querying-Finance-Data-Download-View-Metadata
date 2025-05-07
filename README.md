## Project 2: Stock Volatility Analysis using AWS Athena, Glue, and Lambda
Project Overview
This project implements a complete data pipeline to analyze stock price volatility using AWS services. The pipeline covers data ingestion, storage, cataloging, querying, and optional visualization. The goal is to compute daily stock volatility metrics such as average, maximum, and minimum values for multiple companies in a scalable and automated manner.

## Technologies Used
Amazon S3
Stores raw stock price data in JSON format. This is the main storage location for all ingested data.

# AWS Lambda
Simulates real-time data ingestion by fetching stock price data and writing it to S3 at regular intervals.

# AWS Glue
Crawlers scan the S3 bucket to detect data schema and create catalog tables in the AWS Data Catalog for querying.

# Amazon Athena
SQL-based queries are used to analyze the structured data and compute the required volatility metrics.

# Pandas and Jupyter Notebook
For local analysis, exported query results can be loaded and visualized using Python.

## Volatility Metrics Computed
Avg_Volatility: Average volatility per company per day, typically calculated from price fluctuations.

Max_Volatility: Highest volatility observed per day.

Min_Volatility: Lowest volatility observed per day.

These metrics help understand how much stock prices fluctuate over a given time frame.

## Reproducibility Steps
Upload Raw Data to S3
Upload the stock price data in JSON format to the specified S3 bucket:
s3://cis4130-kinesis-data-storage-<your-id>

Run AWS Glue Crawler

Create and configure a crawler in AWS Glue.

Set the data source to your S3 bucket path.

Choose or create a database (e.g., db2).

Run the crawler to catalog the data into a table (e.g., project2_fixed).

Query Data in Amazon Athena

Open Athena and select the appropriate database.

Run a SQL query to compute the volatility metrics. Example:

## SQL

SELECT 
  name AS Company,
  
  SUBSTRING(ts, 1, 10) AS Date,
  
  ROUND(AVG(volatility), 3) AS Avg_Volatility,
  
  MAX(volatility) AS Max_Volatility,
  
  MIN(volatility) AS Min_Volatility
  
FROM project2_fixed

GROUP BY name, SUBSTRING(ts, 1, 10)

ORDER BY Date;

Export Results for Local Use

Export the results of the Athena query as a CSV file.

Load the CSV file into a Jupyter Notebook for further analysis using Pandas:


## Project Outcome
This project demonstrates the use of cloud-based services to build an automated and scalable pipeline for analyzing stock market volatility. It enables efficient data processing and analysis using serverless tools, while also supporting local exploration and visualization.

