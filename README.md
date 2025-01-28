

# E-commerce Data Pipeline using Databricks

## Project Overview
This project builds an end-to-end **E-commerce Data Pipeline** using **Azure Databricks** to process and transform data from an open-source dataset available on **data.world**: [E-commerce Users of a French C2C Fashion Store](https://data.world/jfreex/e-commerce-users-of-a-french-c2c-fashion-store). 

## Data Sources
The dataset consists of the following four CSV files:
- **Users**
- **Countries**
- **Sellers**
- **Buyers**

## Project Workflow
### **Step 1: Data Ingestion & Storage in ADLS**
- Extract raw **CSV files** from data.world.
- Store raw CSV files in **Azure Data Lake Storage (ADLS)** under the **Landing Zone 1 (Raw Data in CSV)**.
- Use **Azure Data Factory (ADF)** to convert CSV to **Parquet format**.
- Store transformed Parquet files in **Landing Zone 2 (Raw Data in Parquet)** in ADLS.

### **Step 2: Data Transformation in Azure Databricks (Medallion Architecture)**
The project follows the **Medallion Architecture** with **three layers**:
1. **Bronze Layer**: 
   - Read raw **Parquet files** from **ADLS**.
   - Create **Delta tables** to store raw data in Databricks.
   - Store raw data without transformations.

2. **Silver Layer**:
   - Perform **data cleansing**, **filtering**, and **deduplication**.
   - Implement necessary **data transformations** using **PySpark**.
   - Store the cleaned and processed data in new **Delta tables**.

3. **Gold Layer**:
   - Perform **aggregations** and **business transformations**.
   - Store refined data for **reporting and analytics**.

### **Step 3: Data Integration & Analytics**
- Load **processed Gold Layer data** into **Azure Synapse Analytics**.
- Connect **Power BI** to Synapse for **interactive visualizations & reporting**.

## **Technologies Used**
- **Azure Data Lake Storage (ADLS)** – Storage for raw and processed data.
- **Azure Data Factory (ADF)** – Data ingestion and transformation (CSV to Parquet).
- **Azure Databricks** – Data transformation using PySpark & Medallion Architecture.
- **Delta Lake** – Storage format for optimized data processing.
- **Azure Synapse Analytics** – Data warehouse for analytics.
- **Power BI** – Data visualization and reporting.

## **Directory Structure**
```
Ecommerce-Data-Pipeline/
│── data/
│   ├── raw_csv/            # Landing Zone 1 (Raw CSV Data)
│   ├── raw_parquet/        # Landing Zone 2 (Raw Parquet Data)
│── notebooks/
│   ├── bronze_layer.py     # Script for Bronze Layer (Raw Data Ingestion)
│   ├── silver_layer.py     # Script for Silver Layer (Data Cleaning & Transformation)
│   ├── gold_layer.py       # Script for Gold Layer (Aggregations & Business Logic)
│── scripts/
│   ├── adf_pipeline.json   # Azure Data Factory Pipeline JSON
│   ├── mount_adls.py       # Databricks ADLS Mount Script
│── reports/
│   ├── powerbi_dashboard.pbix # Power BI Dashboard File
│── README.md
```

## **How to Run the Project**
### **1. Setup Azure Services**
- Create **Azure Data Lake Storage (ADLS)** and upload raw CSV files.
- Set up **Azure Data Factory (ADF)** pipeline to convert CSV to Parquet.
- Deploy **Azure Databricks Workspace** and mount ADLS.

### **2. Run Databricks Notebooks**
- Run **bronze_layer.py** to ingest raw Parquet data into Delta tables.
- Run **silver_layer.py** to clean and transform data.
- Run **gold_layer.py** to apply business transformations and aggregations.

### **3. Load Data into Synapse and Visualize with Power BI**
- Connect **Azure Synapse** to the Gold Layer Delta Tables.
- Use **Power BI** to create dashboards based on Synapse data.

## **Next Steps**
- Optimize Databricks workflows for better performance.
- Implement **CI/CD pipeline** using **Azure DevOps & GitHub Actions**.
- Enhance data quality monitoring and anomaly detection.

## **Contributing**
Contributions are welcome! Feel free to open issues and submit pull requests.

## **License**
This project is licensed under the **MIT License**.
