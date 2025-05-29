# BigData_pipeline_earthquake

Implementation Overview:

This project focuses on building a modern data pipeline on Microsoft Azure to collect and process daily earthquake data from a public API. The pipeline follows the medallion architecture, consisting of Bronze, Silver, and Gold layers, and is primarily implemented using Azure Databricks with Python.

![image](https://github.com/user-attachments/assets/cb82836d-bca9-49ff-9164-f2c6bf14e537)

**Bronze Layer – Raw Data Ingestion**
In this layer, raw data is ingested directly from the Earthquake API without any transformations. The goal of the Bronze layer is to preserve the original source data as-is for traceability and auditing purposes. Data is stored in a raw format in Azure Data Lake (or mounted storage), and ingestion scripts are written in Python using Databricks notebooks.

**Silver Layer – Data Cleaning and Transformation**
The Silver layer focuses on transforming and cleaning the data for analysis. Key processing steps include:
Parsing and selecting relevant fields needed for downstream analytics.
Converting timestamp fields from epoch format to human-readable datetime.
Handling missing values and standardizing column formats.
Preparing structured data that aligns with business and analytical requirements.
This stage ensures that the data is well-organized, clean, and ready for enrichment and modeling.

**Gold Layer – Data Enrichment and Business Logic**
The Gold layer applies business rules and logic to prepare the data for reporting and advanced analytics. In this project, for example, we introduce a categorization logic for earthquake severity based on the sig (significance) value:

If sig < 100, label as Low
If 100 ≤ sig < 500, label as Moderate
If sig ≥ 500, label as High
This enriched dataset is then stored in a format optimized for querying and visualization.

**Pipeline Orchestration with Azure Data Factory**
To automate the entire data pipeline, Azure Data Factory is used to:
Schedule data ingestion to run daily or at custom intervals.
Trigger Databricks notebooks to execute each processing stage (Bronze → Silver → Gold).
Manage dependencies and monitor pipeline execution status.
This provides an end-to-end automation flow for data processing in production-like scenarios.

**Data Querying and Visualization with Azure Synapse & Power BI**
Once the data reaches the Gold layer:
Azure Synapse Analytics is used to create external tables, views, and query-ready datasets.
These curated datasets are then connected to Power BI for interactive dashboards and analytical reporting.
This allows stakeholders to explore earthquake trends, severity levels, and regional insights visually.


**Vietnamese Version**
quick description!
| **Tầng (Layer)**          | **Mục đích**                                                                  | **Công việc chính**                                                                                            | **Công cụ / Công nghệ**                            |
| ------------------------- | ----------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------- | -------------------------------------------------- |
| **Bronze (Raw Layer)**    | Thu thập và lưu trữ dữ liệu thô, nguyên bản từ Earthquake API                 | - Lấy dữ liệu thô hàng ngày từ API<br>- Lưu trữ dữ liệu chưa qua xử lý                                         | Azure Databricks (Python), Azure Data Lake Storage |
| **Silver (Clean Layer)**  | Làm sạch và chuẩn hóa dữ liệu, chọn lọc các cột cần thiết để phân tích        | - Chuyển đổi định dạng thời gian từ epoch sang datetime<br>- Lọc và chuẩn hóa dữ liệu<br>- Xử lý giá trị thiếu | Azure Databricks (Python)                          |
| **Gold (Curated Layer)**  | Áp dụng các quy tắc nghiệp vụ, phân loại dữ liệu phục vụ phân tích và báo cáo | - Phân loại mức độ động đất theo trường `sig` (Low, Moderate, High)<br>- Chuẩn bị dữ liệu cho báo cáo          | Azure Databricks (Python)                          |
| **Orchestration**         | Tự động hóa việc thu thập và xử lý dữ liệu theo lịch trình                    | - Tạo pipeline chạy định kỳ lấy dữ liệu<br>- Điều phối các bước xử lý (bronze → silver → gold)                 | Azure Data Factory                                 |
| **Phân tích & Trực quan** | Tạo các bảng, view để truy vấn dữ liệu và tạo báo cáo trực quan bằng Power BI | - Tạo database, bảng và view phục vụ phân tích<br>- Kết nối Power BI để làm dashboard và báo cáo               | Azure Synapse Analytics, Power BI                  |

