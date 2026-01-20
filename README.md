# 🚀 End-to-End Data Engineering Pipeline on Azure Databricks

![Azure](https://img.shields.io/badge/azure-%230072C6.svg?style=for-the-badge&logo=microsoftazure&logoColor=white) ![Databricks](https://img.shields.io/badge/Databricks-FF3621?style=for-the-badge&logo=databricks&logoColor=white) ![Apache Spark](https://img.shields.io/badge/Apache%20Spark-FDEE21?style=for-the-badge&logo=apachespark&logoColor=black) ![Python](https://img.shields.io/badge/python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54)

## 📌 Project Overview
This project demonstrates a production-grade Data Engineering solution built on **Microsoft Azure** and **Databricks**. It implements a Lakehouse architecture to ingest, process, and analyze large-scale datasets (e.g., Netflix/Spotify data) using modern Data Engineering practices.

The pipeline handles **incremental data loading**, **schema evolution**, and **real-time transformations** using Databricks Auto Loader and Delta Live Tables (DLT).

---

## 🏗️ Architecture & Data Flow

**Architecture Pattern:** Medallion Architecture (Bronze $\rightarrow$ Silver $\rightarrow$ Gold)

1.  **Ingestion (Raw):** Data is ingested from external sources (SQL DB/API) into **Azure Data Lake Gen2 (ADLS)** using **Azure Data Factory (ADF)**.
2.  **Bronze Layer (Ingestion):** Databricks **Auto Loader (`cloudFiles`)** incrementally processes raw JSON/CSV files and stores them in Delta format.
3.  **Silver Layer (Transformation):** * Data cleaning and deduplication.
    * Schema enforcement.
    * Handling complex transformations using **PySpark**.
4.  **Gold Layer (Aggregation):** Business-level aggregates ready for reporting and analytics.
5.  **Orchestration:** Managed via **Databricks Workflows** and **ADF Pipelines**.
6.  **Governance:** **Unity Catalog** is used for centralized data governance and access control.

---

## 🛠️ Tech Stack

* **Cloud Platform:** Microsoft Azure
* **Storage:** Azure Data Lake Storage (ADLS) Gen2
* **ETL & Orchestration:** Azure Data Factory (ADF), Databricks Workflows
* **Processing:** Azure Databricks (Apache Spark / PySpark)
* **Formats:** Delta Lake, Parquet, JSON, CSV
* **Advanced Features:** * Databricks Auto Loader
    * Delta Live Tables (DLT)
    * Unity Catalog
    * Spark Structured Streaming

---

## 📂 Repository Structure

The project logic is divided into the following notebooks:

| Notebook | Description |
| :--- | :--- |
| `1_Autoloader` | Handles incremental ingestion from ADLS (Raw) to Bronze layer using Spark Structured Streaming and Auto Loader. Handles schema evolution automatically. |
| `2_silver` / `4_Silver` | Performs data cleaning, deduplication, and transformation to create the Silver layer tables. |
| `3_lookupNotebook` | Utility notebook used to fetch dynamic parameters and metadata for orchestration loops. |
| `7_DLT_Notebook` | Implementation of **Delta Live Tables** pipeline to define declarative ETL with built-in data quality expectations. |
| `6_falsenotebook` | Used for error handling and testing pipeline failure scenarios. |

---

## 🚀 Key Features Implemented

### 1. Incremental Loading with Auto Loader
Instead of listing all files in the storage account (which is expensive), I utilized **Databricks Auto Loader**.
* **Benefit:** Efficiently detects new files as they arrive in ADLS.
* **Schema Evolution:** Automatically handles changes in source data structure without breaking the pipeline.

### 2. Delta Live Tables (DLT)
Implemented a declarative pipeline using DLT.
* Defined **Data Quality Expectations** (e.g., `@expect_or_drop("valid_id", "id IS NOT NULL")`).
* Visualized data lineage and dependencies automatically.

### 3. Metadata-Driven Pipeline
* Used **Databricks Utilities (`dbutils.widgets`)** to parameterize notebooks.
* This allows the same notebook to process different datasets (Users, Movies, Credits) by simply passing different parameters, reducing code redundancy.

### 4. Unity Catalog Integration
* Migrated from legacy Hive Metastore to **Unity Catalog**.
* Enabled 3-level namespace (`catalog.schema.table`) for better data organization and security.

---

## 📈 Key Learnings
* **Spark Optimization:** Learned to manage cluster configurations and optimize shuffle partitions for streaming jobs.
* **State Management:** Handled streaming state using Checkpointing in ADLS.
* **Governance:** Understood the importance of Unity Catalog for managing external locations and volumes secure credential passthrough.

---

## 🤝 Connect
Feel free to reach out if you have questions about this project or Data Engineering on Azure!

* **GitHub:** https://github.com/Mayurkumbhar456
* **LinkedIn:** www.linkedin.com/in/mayur-kumbhar-91836218a
