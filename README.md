# **Big Data Analytics Capstone Project: Talent Pool Intelligence Pipeline**

## **Project Overview**

This project implements a scalable **Big Data Analytics pipeline** on the **Databricks Lakehouse Platform** to transform unstructured resume text into five distinct, actionable business insights for strategic talent management (HR and Education).

The solution utilizes **PySpark**, **Delta Lake**, **User-Defined Functions (UDFs)**, and **Machine Learning (K-Means Clustering)** to process resumes at scale and generate high-value reports, including skill gap identification and candidate scoring.

## **🎯 5 Business Use Cases Implemented**

| \# | Use Case | Business Value | Pipeline Component |
| :---- | :---- | :---- | :---- |
| **1** | **Skill Demand Analytics** | Identifies the top N most frequent skills required by the market. | Gold Layer |
| **2** | **Resume Clustering** | Segments the candidate pool into human-readable skill profiles (e.g., 'Data Analyst', 'ML Specialist'). | PySpark MLlib |
| **3** | **Job-Readiness Scoring** | Assigns an objective **ATS-like quality score (0-100)** to every applicant. | PySpark UDF |
| **4** | **Market Intelligence** | Compares the average readiness score across all talent segments for strategic hiring focus. | Gold Layer |
| **5** | **Skill Gap Analysis** | Pinpoints the exact technical skills critically **missing** in the entry-level talent pool, guiding curriculum development. | Gold Layer |

## **📐 Project Architecture (Medallion Lakehouse)**

The project adheres to the **Medallion Architecture** to ensure data quality, governance, and scalability. The entire pipeline is orchestrated via the Master\_Pipeline\_Runner.

| Layer | Notebook | Function | Key Technology |
| :---- | :---- | :---- | :---- |
| **BRONZE** | Bronze\_Layer.ipynb | **Ingestion:** Reads raw .txt files from the Volume and stores them in Delta Lake as the "Source of Truth." | Delta Lake |
| **SILVER** | Silver\_Layer.ipynb | **Feature Engineering:** Cleans text, normalizes data, and uses custom **PySpark UDFs** for core skill extraction. | PySpark UDFs, Regex |
| **GOLD** | Gold\_Layer.ipynb | **Reporting:** Executes ML models (K-Means), applies scoring logic, and generates all 5 final analytical reports/tables. | PySpark MLlib, Spark SQL |

## **🚀 How to Run the Project**

This project requires a functional Databricks workspace with an attached compute resource.

### **1\. Data Setup**

1. **Create Volume:** In the Databricks Catalog Explorer, ensure a Unity Catalog Volume exists (e.g., /Volumes/workspace/default/raw\_resumes/).  
2. **Upload Data:** Upload the provided sample resume text files (resume\*.txt) into this Volume.

### **2\. Notebook Execution**

All core logic resides within the pipeline/ folder. The entire workflow can be executed using a single command:

1. Open the Master\_Pipeline\_Runner.ipynb notebook.  
2. Run the single cell. This uses dbutils.notebook.run() to execute the layers sequentially, guaranteeing dependencies are met:  
   Bronze\_Layer.ipynb  \# Creates bronze\_resumes  
   ⬇️  
   Silver\_Layer.ipynb  \# Reads bronze, creates silver\_features  
   ⬇️  
   Gold\_Layer.ipynb    \# Reads silver, creates all final reports

### **3\. Viewing Results**

* **Final Data Products:** All five business reports are saved as Delta tables in the Gold Layer (e.g., gold\_skill\_demand, gold\_market\_intelligence).  
* **Dashboard:** The final comprehensive dashboard visualization is assembled from these Gold tables in the Databricks SQL Persona.

## **📦 Repository Contents**

* pipeline/: Contains the three architectural notebooks (Bronze\_Layer.ipynb, Silver\_Layer.ipynb, Gold\_Layer.ipynb) and the orchestrator (Master\_Pipeline\_Runner.ipynb).  
* data/: Contains the raw resume text files used for ingestion.  
* docs/: Contains the project report document (PDF/Markdown).  
* screenshots/: Contains the final dashboard visualization images (due to platform export limitations).