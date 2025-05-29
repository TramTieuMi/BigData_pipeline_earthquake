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

------------
| **Tầng (Layer)**          | **Mục đích**                                                                  | **Công việc chính**                                                                                            | **Công cụ / Công nghệ**                            |
| ------------------------- | ----------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------- | -------------------------------------------------- |
| **Bronze (Raw Layer)**    | Thu thập và lưu trữ dữ liệu thô, nguyên bản từ Earthquake API                 | - Lấy dữ liệu thô hàng ngày từ API<br>- Lưu trữ dữ liệu chưa qua xử lý                                         | Azure Databricks (Python), Azure Data Lake Storage |
| **Silver (Clean Layer)**  | Làm sạch và chuẩn hóa dữ liệu, chọn lọc các cột cần thiết để phân tích        | - Chuyển đổi định dạng thời gian từ epoch sang datetime<br>- Lọc và chuẩn hóa dữ liệu<br>- Xử lý giá trị thiếu | Azure Databricks (Python)                          |
| **Gold (Curated Layer)**  | Áp dụng các quy tắc nghiệp vụ, phân loại dữ liệu phục vụ phân tích và báo cáo | - Phân loại mức độ động đất theo trường `sig` (Low, Moderate, High)<br>- Chuẩn bị dữ liệu cho báo cáo          | Azure Databricks (Python)                          |
| **Orchestration**         | Tự động hóa việc thu thập và xử lý dữ liệu theo lịch trình                    | - Tạo pipeline chạy định kỳ lấy dữ liệu<br>- Điều phối các bước xử lý (bronze → silver → gold)                 | Azure Data Factory                                 |
| **Phân tích & Trực quan** | Tạo các bảng, view để truy vấn dữ liệu và tạo báo cáo trực quan bằng Power BI | - Tạo database, bảng và view phục vụ phân tích<br>- Kết nối Power BI để làm dashboard và báo cáo               | Azure Synapse Analytics, Power BI                  |

