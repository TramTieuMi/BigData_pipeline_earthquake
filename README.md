# BigData_pipeline_earthquake

Implementation Overview:

In this project, I utilize Azure Databricks to build a data pipeline following the medallion architecture with three layers: Bronze, Silver, and Gold, all implemented using Python (source code available in the repository).

![image](https://github.com/user-attachments/assets/cb82836d-bca9-49ff-9164-f2c6bf14e537)

Bronze Layer: Ingests raw data directly from the Earthquake API and stores it without any transformation.

Silver Layer: Cleans the data, selects relevant columns for analysis, and handles data type conversions — such as converting timestamps from epoch to readable datetime formats.

Gold Layer: Transforms the cleaned data into meaningful features for analysis. For instance, earthquake severity is classified based on the sig value:

sig < 100: Low

100 ≤ sig < 500: Moderate

sig ≥ 500: High

Additionally, Azure Data Factory is used to create a scheduled pipeline that automates daily data ingestion. After processing, Azure Synapse Analytics is used to create databases, tables, and views, which are then connected to Power BI for deeper analysis and visualization.

